---
layout: post
title: Jenkins startup performance
summary: Investigating and improving Jenkins startup performance
---
# Problem
Jenkins startup time is primarily bottlenecked by the number of jobs on the cluster, assuming you have a reasonable value set for [jenkins.InitReactorRunner.concurrency](https://wiki.jenkins-ci.org/display/JENKINS/Features+controlled+by+system+properties). However, you'll take another hit if those jobs aren't stored locally, such as on an NFS filer. It hurts, really bad.

# Job loading
With `strace` you can figure out that Jenkins reads 2 types of files when loading a job: `nextBuildNumber` and `config.xml`. If the job is a matrix job, the children jobs' `nextBuildNumber`s and `config.xml`s will also be read. Having these files on an NFS filer incurs additional time overhead due to the read latency when Jenkins loads jobs, _assuming_ the files haven't been read before. You can determine this for yourself by clearing the host's filesystem cache with `echo 3 > /proc/sys/vm/drop_caches` and restarting Jenkins, noting the startup time, restarting Jenkins again, and then noting a significantly faster startup time.

# A Possible Solution
So, one way to improve Jenkins startup time when you have jobs on a storage medium with slow reads is to prime the filesystem cache. I ran this experiment with 2 caching techniques and different sets of files (`nextBuildNumber` and `config.xml` of the top level job, `nextBuildNumber` and `config.xml` of the top and children level jobs, `config.xml` only, etc...). The first technique was to prime the cache with `cat FILE > /dev/null` - that didn't seem to work. What did work, but only temperamentally, was caching using `vmtouch`. [`vmtouch`](https://hoytech.com/vmtouch/) is super handy for playing around with the filesystem cache, and, in my experiments, I used `vmtouch -ft` to bring files into memory. I noticed a significant startup improvement with just `vmtouch -ft`ing top level `config.xml`. To give numbers, Jenkins takes 5 mins to restart with 60K jobs on a host with a fully warm cache, 20 minutes cold, and 10 minutes after caching top level `config.xml`s with `vmtouch -ft`.

# Lessons learned
After all of my experimentation, I realized that the easiest solution for a faster startup time is to keep the number of jobs on a cluster low. If you know there are a lot of ephemeral jobs (pull request jobs), you can automate their cleanup. If your shop really does require a ridiculous number of jobs to be maintained, you should probably spawn more clusters. I would not suggest playing around with the filesystem cache because you can't easily prevent evictions; there was variation between runs of my 'winning' caching technique.

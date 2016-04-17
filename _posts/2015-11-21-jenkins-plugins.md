---
layout: post
title: Jenkins plugins are user friendly
summary: If the user isn't managing Jenkins
---
## Black box testing
I was working on automating Jenkins plugin management when I encountered a mystery. I wanted the Jenkins cluster to have v1.22 of the `credentials` plugin but after a `chef-client` run, the cluster would have v1.18. I verified that the v1.22 plugin `.jpi` was downloaded to the plugins folder and that the older, extracted `credentials` plugin folder was deleted, so Chef was doing its job. Maybe I forgot to install `credentials`'s dependencies? No, that wasn't it. Maybe the `credentials.jpi` was corrupted? Nope. It had to be a Jenkins magic show.

## Reading the source
Black box testing by trying random things and running `chef-client` wasn't worth it anymore so I took to the source code. After perusing plugins and startup related code, I fell upon [what I was looking for](https://github.com/jenkinsci/jenkins/blob/jenkins-1.642.2/core/src/main/java/hudson/init/InitStrategy.java#L56). This clearly explained the issue. Because I wanted a version of a core plugin (1.22) that didn't ship with Jenkins v1.642 by [default](https://github.com/jenkinsci/jenkins/blob/jenkins-1.642.2/war/pom.xml#L277) (1.18), I needed to also create a `PLUGIN.pinned` file to tell Jenkins not to overwrite it with the bundled version of the plugin.

## Lessons learned
Jenkins was built to be user friendly so it's supposed to be opinionated and self-managed. Infrastructure management is inherently hard for systems that perform a lot of magic. It's well worth the time investment to learn at least the basic internals of such a system if you want to go behind its back and manage it forcefully. I was pretty lucky that I was dealing with an [open source](https://github.com/jenkinsci/jenkins) project. 

Because Jenkins is actively developed, my problem might not be a problem anymore (I was playing with v1.642), but it's still a good example of how Jenkins is full of gotchas if you want to automate its infrastructure. Also, be careful if you manage plugins manually because you'll have to resolve dependencies on your own as well. 

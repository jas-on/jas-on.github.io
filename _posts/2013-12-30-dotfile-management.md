---
layout: post
title: Managing dotfiles
summary: Bring your home wherever you go
---
## Bring a suitcase
I've used many different OSes, sometimes concurrently on a day to day basis. I have quite a few custom configurations and it'd be impractical for me to 1. reconfigure my environment and tooling every time I set-up a new workspace and 2. manually copy over changes to my configurations into my various workspaces to keep them up-to-date. You'll encounter these issues regardless of how many dotfiles you have (1 vs my ~30). A convenient solution I discovered for this problem is to use a dotfile manager which pulls and stores your configurations from a hosted location (think GitHub or Bitbucket).

## [homesick](https://github.com/technicalpickles/homesick)
There are a few dotfile managers in the wild, and I've only played with `homesick` but I highly recommend it. `homesick` keeps track of your dotfiles with Git so if you want to change your configs and pull them onto another machine, it's as simple as a `homesick commit` and `homesick push` in your current workspace, and a `homesick pull` in your other workspace. `homesick` sets up symlinks in your home directory which point to those stored in the `homesick`-managed Git repo. It's nice that `homesick` allows you to keep track of multiple sets of configs (called "castles") so you don't have to pollute your home directory with non-OS-related configs such as `.minttyrc` which I'd only care about on a Windows box, or `.Xresources` on my Linux box.

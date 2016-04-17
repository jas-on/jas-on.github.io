---
layout: post
title: Backgrounding with zsh-notify
summary: I'm left with a graveyard of shells
---
I'm an avid user of `zsh` plugins, some of them from [`oh-my-zsh`](https://github.com/robbyrussell/oh-my-zsh/), some of them from the hidden caches of GitHub. For the past few months I've run into an issue once every few days where `zsh` becomes completely unusable and I can't spawn any more shells. I ran `ps` and found hundreds of zombied `-zsh` processes laying around. It had to be a plugin that creates subshells.

I use different `tmux` windows for different parts of my development process so I almost always have `vim` open in one window. Sometimes it's just convenient to `ctrl-z` to the command line from `vim`, check something quickly, and `ctrl-z` back (with [fancy `ctrl-z`](https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/fancy-ctrl-z/fancy-ctrl-z.plugin.zsh)) to `vim`. However, I learned that this workflow doesn't play so nicely with the [`zsh-notify`](https://github.com/marzocchi/zsh-notify) plugin. If I happen to background `vim` for more than 30 seconds, `zsh-notify` will queue up a notification for [when the process finishes](https://github.com/marzocchi/zsh-notify/blob/a5836ddcd8a4f901597ed22fbd1339b2398a3f76/notify.plugin.zsh#L30) in another shell, and it doesn't get destroyed when I foreground `vim`. The end result: I'm left with a graveyard of zombie `zsh`s and I get `/Users/myuser/.zshrc.local:53: fork failed: resource temporarily unavailable` when I try to spawn any more shells.

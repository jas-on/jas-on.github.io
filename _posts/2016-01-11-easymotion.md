---
layout: post
title: Faster navigation in vim
summary: Navigation through visualization
---
# Navigation in `vim`
`vim` provides a huge speedup in text editing because of its features for fast navigation. However, there can be some non-trivial cognitive load when trying to combo your motions. For example, your cursor might be at the beginning of a paragraph and you want to move it to the middle. You might go down some rows with `j` and then hit a few `w`s to jump over words to get to your destination. Or, for that final stretch, you might want to optimize for the least amount of keystrokes by counting how many words away you are from your destination and prepending a number in front of your `w`. There's a lot of effort either way.

# easymotion
[`easymotion`](https://github.com/easymotion/vim-easymotion) aims to make navigation easier by making it visual. The idea is that you have a location you want your cursor to be at in mind, you trigger `easymotion`, you type a short string which corresponds to where you want to jump, and you're there. There are definitely times when using a navigation primitive is more efficient, so the plugin accounts for at least the edge cases. It's a lot easier to understand it by [seeing it in action](https://github.com/easymotion/vim-easymotion) (and trying it yourself!) rather than having me explain it.

# In Chrome
I enjoy using [Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en) to get my `vim` fix when browsing the web. It comes with a bunch of goodies, including an `easymotion`-like way of navigating links. I don't find myself using that feature very often, though; perhaps it's because webpages are a lot more interactive than code blocks.

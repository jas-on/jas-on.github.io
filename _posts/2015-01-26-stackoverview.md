---
layout: post
title: StackOverview
summary: View quick StackOverflow result stats from Google search
---
Tonight was a slow night in the CSE basement, and I guess it's because the students are catching up on sleep after turning in their first compiler project. My idle mind came up with a silly idea: [StackOverview](https://chrome.google.com/webstore/detail/stackoverview/oihjaeffdklalbagimogdhokoaidmain)!

When you google something code related and expect to get StackOverflow results, wouldn't it be nice to know about the "quality" of a result before spending time looking at it? That's the itch I want to scratch with StackOverview. The Chrome extension is pretty simple: for each StackOverflow result, it fetches the corresponding page, checks how many answers are on it and if there is an accepted answer, and reports the findings in the form of a colored number icon embedded within the Google result. The icon is green if there is an accepted answer, yellow if there isn't, and red if there are no answers. In the future, I might have it show more information like question and answer quality; however, I don't want to inflict too much cognitive load.

This was my first experience with creating a Chrome extension, and it wasn't too bad. The main annoyance came with creating the extension's icons. In general, I see too many bulky plugins these days, mainly because they pull in jQuery for a trivial utility function. I made a conscious effort to keep the size to a minimum, and it wasn't too hard to roll my own AJAX.

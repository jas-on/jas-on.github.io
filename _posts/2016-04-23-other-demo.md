---
layout: post
title: Someone else should demo
summary: Reveal holes and share knowledge
---
## Calling it done
A few months ago my (then newly formed) team incorporated an unorthodox clause into the typical definition of done for a story.

> The story should be demoed to the product owner by someone who did not work on it as part of the verification process.

We hoped that this would reveal holes in the story's implementation and facilitate knowledge sharing.

## Reveal holes
You, as the story's implementer, will be biased when demoing the story. You will take the happy paths that you know are supported. You will take the paths that you believe to be the only unhappy paths. You will tell the product owner, "See, I accounted for all of the possible paths this story touches." The product owner trusts you and hits the final nail into the coffin by calling the story done.

A few days later, a customer files a ticket. Your teammate, who didn't work on the story, reads this ticket and empathizes with the customer. She believes that the steps he took to trigger the bug should have resulted in a good response from the product. Heck, she probably would have interacted with the product in the same way as the customer. If she demoed your work on the story, she might have tread on this unhappy path.

Harness your teammates' creativity.

## Share knowledge
You work on a team of ten engineers who specialize in different areas. One teammate is armed with monitoring and alerting skills; another, with infrastructure automation chops. This team is diverse in backgrounds but rallies around a similar enough mission that each member should care about what the others are doing to drive it.

A teammate just finished a story about adding monitoring for a new metric to measure the product's health. The team doesn't receive false alarms about the product too often, so everyone is confident in the current monitoring set-up. You check your work mail the next day and you notice an inundation of alerts related to the story your teammate recently finished. He's now on PTO for a week. Your team determines that the alerts are invalid after manually checking the health of the product but is anxious to disable the faulty monitoring because they know [alert fatigue](https://en.wikipedia.org/wiki/Alarm_fatigue) is dangerous. If anyone else on the team demoed your teammate's work on the story, someone might have learned where the alerts are coming from and how to disable them.

Knowledge should _not_ be tribal.

## How it's worked out
My team has improved its effectiveness and morale after upholding this definition of done constraint for a few months. It's important to note the effect that it has on our customers too. We have higher confidence in what we ship because our vetting process is more likely to catch bugs. This means delivering delight to our customers quicker. We have stronger cohesion amongst the team because we've vanquished fear-of-missing-out. This means lower mean time to resolution for our incidents and less customer impact.

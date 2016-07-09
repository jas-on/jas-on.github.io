---
layout: post
title: Unblocking customers
summary: Excuses are easy when responsibilities are decoupled
---

I build the CI/CD infrastructure at my company, and last week was pretty shitty.

It was my team's turn to be on-call, and throughout the week I noticed an increasing amount of support requests about onboarding onto our "turnkey deployment solution". This service integrates with our main build tool and one of its most popular use cases is for deploying to a provided host for functional testing during a pull request build. This microservice solves the problem of collaboration in one repo in conjunction with another microservice. The second microservice concerns itself with allocating a pool of hosts for a project, from which a PR build utilizes one of the hosts for the duration of its existence. Due to a large-organization-tech-decision-issue the pools of hosts managed by the microservice have to be manually provisioned. Customers were blocked for two weeks because we ran out of hosts, which are provided by another team, and it is apparently a bureaucratic process to get more.

I brought this issue up during my team's retrospective, and it was hard not to show frustration.

It's easy to play the blame game when your product isn't delivering the best experience because of issues with its dependencies that you don't support.
> Yeah, we filed a ticket with X team, and they said they would get to it when they get to it
> Aw, dang it. Better update the customer with that info. Hey, at least we're being transparent!

No, that is not acceptable. Your team made the decision to take the risk of depending on something, and you all have to take ownership for its degradation as if it were a feature you pushed out.

Now, after you've told yourself the victim story, ask yourself a simple question.
> What can I do right now to get my customers unblocked (think Crucial Conversations)

You'll find that there are viable (sometimes hacky) answers to that question when you accept that your dependencies are failing you and that you need to sever them, albeit temporarily. Perhaps, in the process of brainstorming, a longer term solution will spark up that renders the current blocker a non-issue.

> No we shouldn't do that because it'll just be tech debt for us later on

If you feel this way, you are sorely mistaken about what it means to be a part of the larger organization's team, and, even, why you're a software engineer. We create products to help others: if your customers aren't having a good time, do everything you can to unblock them as soon as possible - you can be disciplined in paying off the tech debt later.

TL;DR: Even though this problem seems to occur far more frequently in large organizations where all major internal services are siloed, stay vigilant and refrain from adopting a defeatist attitude to blocked dependencies.

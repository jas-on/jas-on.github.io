---
layout: post
title: knife hosts list
summary: How to handle partial fleet maintenance
---

`knife` is an essential tool amongst Chef gourmands - managing Chef is inconceivable without it. In my past half-year of using the swiss-army knife, I ran into an issue twice with its usability.

Most generally, you manage your fleet by putting nodes in environments and giving them roles. When you want to do maintenance, you might tag them. Tags are supposed to be used ephemerally.

Consider this situation: you have a bunch of hosts that need maintenance ASAP, how do you apply your fix?

Do you:

1. Write a recipe that detects when your host is in a bad state and recovers it.

2. Run some commands over SSH and manually put them into a good state.

Sure, after your incident you might create some long-term remediation items to understand how the state got into the bad state to begin with and if it can be avoided. In the interest of time, I jump to option 2 more often and I use `knife ssh`.

I only want to run the command on some hosts so I can't target them with role or environment (this is assuming that it's not idiomatic to move hosts around into different roles and environments ephemerally). Sure, I can query by FQDN, but I might have 20 hosts that I want to touch. So is the right way to solve my problem to use `knife tag` on the affected hosts and then target the tag? It could be.

Okay, now let's say that we have our hosts auto-converge. `knife tag` won't stick if a host is in the middle of a convergence.

Given the constraints, an obvious solution is to write a script that feeds a list of FQDNs to `knife ssh 'fqdn:'`. If this were the only solution, it would be useful to have `knife ssh` support taking in a list of hosts. Of course, I have the problems I bring up because (1) I assume that it's not idiomatic to reassign roles and environments for the sole purpose of maintenance and (2) my hosts auto-converge.

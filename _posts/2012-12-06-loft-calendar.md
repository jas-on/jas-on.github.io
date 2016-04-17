---
layout: post
title: Calendar for The Loft at UCSD
summary: Convenient events calendar
---
## New feature
The Loft's [events page](http://theloft.ucsd.edu/index.php/calendar) now has a calendar (if you scroll down a little bit, you can see it) on the side to make it more convenient for people to see which days have an event. Click on it! You won't lose your current page.

## Details
I used the oh-so-popular jQuery `Datepicker` widget. I wonder if it's the most popular jQuery plugin. Integrating the plugin into the site was a matter of specifying a function for [`beforeShowDay`](https://api.jqueryui.com/datepicker/#option-beforeShowDay) which 'is called for each day in the datepicker before it is displayed'. I created an endpoint to tell me dates that have an event on it (it accepted multiple ranges), and I eagerly query it for the current month, the month before, and two months in the future. The other months are lazy loaded. This data is used as a lookup table in the `beforeShowDay` function and decides whether a given date would be grayed out or hyperlinked on the calendar. If it's hyperlinked, a user can click on it to see all of the events listed for that date on another page.

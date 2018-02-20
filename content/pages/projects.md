---
title: Projects
modified: 2018-02-19
---

Here's a partial list of things I've worked on or contributed to.

## Venture

I did a few semesters of research with the MIT Probabilistic Computing Project, primarily working on [Venture](http://probcomp.csail.mit.edu/). I'm not sure I can describe it with justice here[^thesis], but working with the group definitely expanded my mind in terms of thinking about probability, modeling, and abstraction, and also the process of research and science more generally.

## Randometer

Humans have a tendency to see false patterns in random data. I wrote a [webapp version](https://luanthe.github.io/randometer/) of Nate Soares' [Randometer](http://mindingourway.com/randometer/), a set of games for training intuition for what true randomness looks like. Try it yourself and test how well you can distinguish patterns from random noise.

## ESP Website

The website of the [MIT Educational Studies Program](https://esp.mit.edu) handles class scheduling, student registration, and many other logistical aspects of running our educational programs. It's [open source](https://github.com/learning-unlimited/ESP-Website) and also used by its [sister organizations at universities across the country](http://learningu.org/). I was involved with the organization for several years in various program director/admin capacities, and during that time I made several major and minor contributions to the website, including a new module for managing student admissions for our summer program and a new UI for students to browse and choose classes.

## ArgCache

Originally a submodule of the ESP website, [ArgCache](https://github.com/luanthe/django-argcache) is a caching framework for Django projects which I inherited and refactored into a reusable package.
It provides a unique approach to cache invalidation: you declare how your cached functions depend on your database tables, and the framework takes care of expiring cache entries automatically when it determines they've gone stale.

Unfortunately, the documentation is ancient and the code is mildly terrifying, and I never really got around to cleaning it up. It still powers the original website, but I wouldn't seriously recommend using it for anything else in its current state.

## zScore

While I was in undergrad, some friends and I wrote [zScore](https://github.com/sleepers-anonymous/zscore), a <del>social quantified sleep</del> webapp that lets you track how much sleep you're getting and compare with your friends.

[^thesis]: You could try my [M.Eng. thesis](https://dspace.mit.edu/handle/1721.1/113160), but I'm not sure it's great reading material (sorry).

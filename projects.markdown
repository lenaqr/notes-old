---
title: Projects
---

Here's a partial list of things I've worked on or contributed to.

## ESP Website

The website of the [MIT Educational Studies Program](https://esp.mit.edu) handles class scheduling, student registration, and many other logistical aspects of running our educational programs. It's [open source](https://github.com/learning-unlimited/ESP-Website) and also used by our [sister organizations at universities across the country](http://learningu.org/). Over the years I've made several major and minor contributions to the website, including a new module for managing student admissions for our summer program and a new UI for students to browse and choose classes.

## ArgCache

Originally a submodule of the ESP website, [ArgCache](https://github.com/luanthe/django-argcache) is a caching framework for Django projects which I recently (2015) inherited and refactored into a reusable package.
It provides a unique approach to cache invalidation: you declare how your cached functions depend on your database tables, and the framework takes care of expiring cache entries automatically when it determines they've gone stale.

Unfortunately, the documentation is ancient and the code is mildly terrifying, but I'm working on cleaning it up.

## Randometer

Humans have a tendency to see false patterns in random data. I wrote a [webapp version](https://luanthe.github.io/randometer/) of Nate Soares' [Randometer](http://mindingourway.com/randometer/), a set of games for training intuition for what true randomness looks like. Try it yourself and test how well you can distinguish patterns from random noise.

## zScore

My friends and I wrote [zScore](https://zscore.mit.edu), a ~~social quantified sleep~~ webapp that lets you track how much sleep you're getting and compare with your friends.

## This website

I wrote this website using [Hakyll](http://jaspervdj.be/hakyll/), a Haskell static site generator. I also made a [post](/posts/2015-01-06-site-setup.html) documenting how I set it up.

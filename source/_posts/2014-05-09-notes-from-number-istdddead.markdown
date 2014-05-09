---
layout: post
title: "Notes from #isTDDDead?"
date: 2014-05-09 17:04
comments: true
categories: 
---

I worried that I was going to find the discussion between [DHH](http://twitter.com/dhh), [Kent Beck](http://twitter.com/kentbeck) and [Martin Fowler](http://twitter.com/martinfowler) annoying but I actually really enjoyed it. Well worth [watching](https://plus.google.com/events/ci2g23mk0lh9too9bgbp3rbut0k).

Kent & Martin's responses seemed quite surprising to DHH who appears to have had a very dogmatic experience of TDD. The daily use of the guys that were influential in the popularisation of the techniques were more pragmatic than many people will have imagined.

I look forward to the next discussion where I think we'll get into the meat of TDD.

I wrote a number of headline points for your enjoyment!

## Kent Beck

* If an idea is bad, find a cheap way to try it
* Programmers have a right to feel confident about their code
* TDD is one way to achieve confidence
* Mixing techniques - some TDD, some not is totally fine - it's powerful tool
* TDD is often about trade offs
* Don't twist design to make it testable
* Generally doesn't mock anything
  - Mocking can couple you to implementation which too high a price
  - Repeatable feedback loop is far more important

## DHH
* Dogma in TDD circles is big problem (i.e. you *must* TDD 100% to be a 'professional')
* Mocking forces unnatural structure, supporting tests instead of code
* "Easy to test == better design" is a fallacy
* Understandability is often compromised

## Martin Fowler
* TDD does not imply isolation or mocking
* Self-testing code is one of the most important things to deliver - TDD is one approach and it has other benefits

---
layout: post
title: "Dev Diary - 1st March 2015"
date: 2015-03-01 18:49
comments: true
categories: 
---

## Understanding Games

I don't play many games but [Alto's Adventure](http://altosadventure.com) sparked my curiosity in games programming again.

Games programming is quite a bit different from the programming I do day to day. I started taking a look at the amazing tutorials on [Unity's website](http://unity3d.com/learn/tutorials/modules) but I'd really like to get a grounding in the core concepts of what makes a game engine.

In order to work through this, I started writing a basic games engine in Javascript. It handles rendering of basic game entities (i.e. boxes), very basic collision detection & poorly implemented physics.

I've put it on github: [Platformer](https://github.com/stevebartholomew/platformer).


## Podcast App

Seeing the designs come together has been really exciting. Most of the basic feed syncing, episode display/details/play views and I'm now refining that core functionality.  Handling all the different states that episodes and related assets can be in has been challenging.  Spending some time getting good test coverage has helped though. I've made some fairly large refactors of various parts of the code base without much breakage.

I'm starting to see areas that could be turned into libraries although I'm not really sure on the best way to do this in the Java/Android world. [Maven Central](http://search.maven.org) seems to be the [Rubygems](https://rubygems.org)/[npm](https://www.npmjs.com) equivilent but it all seems to be way more complicated.  I'll be doing some research on this in the near future.

In particular, I'll be looking to outsource the podcast feed parsing library. I consider it to have a reasonably easy-to-use API which might benefit others but I'm also keen to get input from a community for handling feed formats. Feed formatting is a constant pain as many differ and are often just plain wrong.

## Hirgana Practice

This app came out of nowhere on a Sunday morning when I was considering the Hiragan practice app I'd been using. Many apps use the 'flash card' style, showing you a character and asking you to choose from a list of Roman sounds - for example, for "ち" you would tap "chi". This is problematic because it encourages you to "map" sounds to known English equivilents instead of internalising the sound itself.

In classic programmer style, instead of just practicing, I wrote an app that plays the sound and you then write the character on screen. You then tap when you're done and compare your character to the actual one.

I lifted most of the drawing code from [here](http://www.raywenderlich.com/18840/how-to-make-a-simple-drawing-app-with-uikit) and translated to Swift.  I'm going to have a go at improving this using actual Bezier paths instead - I've been reading [this](http://code.tutsplus.com/tutorials/smooth-freehand-drawing-on-ios--mobile-13164) to understand more.

With a basic design in place I may release it in the coming weeks.

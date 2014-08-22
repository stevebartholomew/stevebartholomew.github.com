---
layout: post
title: "Dev Diary - 22nd August 2014"
date: 2014-08-22 12:33
comments: true
categories: 
---

Work on the [Reallyenglish](http://www.reallyenglish.com) mobile app is going well as the team prepares for the upcoming official release on Android. After working through bugs on the platform I'm actually really preferring a lot of the toolset that comes with Android over iOS.

Aside from the day job, things have been rather Go-focused.

## Podcast app: Adding subscriptions

I'm keeping the subscriptions/directory side of things on the server at the moment.  Initially I wrote the directory search API in node but on [Ali](http://twitter.com/alinajaf)'s suggestion I tried out [Go](http://www.golang.org). Turns out, I _really_ like it.

Go is super powerful while taking care of some of the more house-keepy parts of something like C. A more concurrent style of programming is actively encouraged in the language through nice abstractions. You can let Go deal with stuff like load balancing between CPUs but it doesn't feel like you're being protected from reality.

I also built a basic version of the podcast search UI for the Android app. Starting to get a feel for how activities and fragments fit together. When I hooked up the UI to the directory service I was pleasantly surprised that Android threw an exception when I tried accessing the network on the main thread on my first pass. Quite a change for the platform.

## Crypto Challenges

I had a really good time Wednesday when I attended [Ali](http://twitter.com/alinajaf)'s workshop/coplay working through [the matasano crypto challenges](http://cryptopals.com/).  A few of us hooked up in a chat room and chatted as we worked through the challenges, sharing ideas as we went. We all chose to use Go which proved really good for the task.

Ali also doubled the earnings from the ticket price and donated the lot to [Eaves](http://www.eavesforwomen.org.uk/) - what a great guy!

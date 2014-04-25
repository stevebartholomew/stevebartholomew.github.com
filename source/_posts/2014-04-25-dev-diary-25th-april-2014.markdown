---
layout: post
title: "Dev Diary - 25th April 2014"
date: 2014-04-25 07:32
comments: true
categories: 
---

## This week

The app store wait continues while we work on promo sites and continued Android fixes.

## Spending time with Android

I've spend the week using a Nexus 5 as my carry phone to get a feel for the subtle differences in the platform. It's been a good learning exercise as I now have a better understanding of Android.

On the whole it's what I expected: great service integration & some interesting features but way lower quality of hardware and software. I've always thought the UI looked messy but it's actually just a bad user experience in many places.

### Third-party apps

I'm a heavy podcast user - I listen to multiple podcasts during the day. My week on Android was made worse but a complete lack of decent podcast clients. Every one of them was awful - confusing, overblown interfaces, even the 'basic' features were impossible to use and understand. I tried many - both paid and free - from 'the best of' lists and none of them made any sense.

## Xamerin

Like many programmers my reaction to the lack of a decent podcast client was to think 'hey - I could write my own!'. This lead me to the [Xamerin Project](http://xamarin.com/). I remember Xamerin & Mono from the early 2000s when I was primarily working in .NET.

After working on a PhoneGap-based project it was interesting to see another approach to the problem of cross-device development. So far I'm impressed. The main idea is to write your core code in shared libraries then create platform-specific UI code that hooks up to it. The whole thing is then compiled down and run on a platform-specific runtime shipped with the app.

## DHH vs TDD

I was a die-hard, London-school TDDer and boy did I talk about it. My approach has softened a lot recently. I broadly agree with DHH's issue with being so prescriptive. Many things that we treat as process should actually be tools for getting the job done. Pair programming, TDD, Agile etc are all susceptible to 'silver-bullet' syndrome.

It is however, important to remember that skepticism is about applying critical thinking - not just dismissing out of hand. The urge to argue against the doctrine can blind you to the good stuff. For example, you're missing out if you've *never* used tests as a way to drive design. A lot of the time it just makes the feedback cycle quicker.

Ultimately we're all just trying to write good code and get good results. I can't say it better than Zed Shaw: [Programming, Motherfucker](http://programming-motherfucker.com/).

## Listening

The ongoing debates and issues surrounding sexism in tech have no doubt been on everyone's minds recent. The [Debug podcast](http://www.imore.com/debug-34-sexism-tech) had a great discussion with a panel of women in the tech industry.

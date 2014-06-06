---
layout: post
title: "Dev Diary - 6th June 2014"
date: 2014-06-06 07:33
comments: true
categories: 
---

## In-app Purchase

Turns out that we need to implement some form of in-app purchase on our app in order to get into the app store. It can be frustrating with Apple because, despite giving us this guidance, they cannot give us a clear 'yes' or 'no' in principal until we submit. Because of this we focused on a minimal implementation and have almost complete the work with a week left in our current sprint.

We used the [iOS In-App Purchase](https://github.com/j3k0/PhoneGap-InAppPurchase-iOS) plugin for Cordova/PhoneGap which works with both old and new receipt styles. Because we're targeting iOS 7, we don't need to have any server side components. Overall I've enjoyed digging into the IAP side of iOS dev - in particular the "Using Store Kit for In-App Purchases" video from [WWDC 2013](https://developer.apple.com/videos/wwdc/2013/) really solidified my understanding.

## I18n with gettext

Internationalization is a big deal for us as we largely target Japanese & Chinese users. We've had a few ways approaching this in the past and all have become difficult to work with.

[Tim](https://twitter.com/timpeat) did some research and suggested we try out the old standard [gettext](http://www.gnu.org/software/gettext/). The benefit here is that the toolchain is highly advanced but the actual usage is very straight forward. It also uses standards that our translators are familiar with. I'm also impressed how simple the integration with code is. Having base keys of actual text means that code makes more sense to read:

```javascript
var heading = I18n.gettext('Welcome to my site');
```

I wrapped up the [jsxgettext](https://github.com/zaach/jsxgettext) npm module in a singleton that we could `require` through out the code where needed. Handlebars integration was very simple:

```javascript
Handlebars.registerHelper('tr', function(text) {
  var translation = I18n.gettext(text);

   return translation;
}, this);
```

We can then extract translations into `.pot` files and use gettext's `msgmerge` to handle merging & building of locale `.po` files.

## Appium

Our apps automated UI specs have been pretty flaky for a while. Many times a day we'd get failures from [Travis](https://travis-ci.com/) because the simulator was just hanging or didn't even boot. Thankfully [Appium 1.0](http://appium.io/) dropped a few of weeks ago and the improvements looked promising. [Randy](https://twitter.com/morgan_randy) set out getting our cucumber steps inline with the new API and so far everything has been running very smoothly.

## Swift

Like many, many developers I was super excited after the [Apple keynote](http://www.apple.com/apple-events/june-2014/) on Monday. As well as taking a look at the new APIs I've been working through the [Swift language guide](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/TheBasics.html). Just getting familiar with the syntax and approach for now but I'm looking forward to writing some actual code in it soon. It's great to see Apple moving on something like this and exciting to see another platform going in a functional programming direction.

## Reading

I've read Ilya Grigorik's [Minimum Viable Block Chain](https://www.igvita.com/2014/05/05/minimum-viable-block-chain/) post multiple times this week - really interesting tech explained clearly. It's made me think about ways to apply the concepts behind crypto currencies to other areas that have similar problem sets. Establishing validity and history is not limited to financial transactions.

## Listening

I loved Radiolabs episode ["Things"](http://www.radiolab.org/story/things/). As always, interesting stories with lots to think about afterwards. I used to be very attached to "things" in the past and while I've improved, this episode really made me think about how more I could let go of.

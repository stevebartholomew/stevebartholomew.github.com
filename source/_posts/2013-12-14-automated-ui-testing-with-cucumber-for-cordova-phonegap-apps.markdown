---
layout: post
title: "Automated UI Testing with Cucumber for Cordova/Phonegap apps"
date: 2013-12-14 20:45
comments: true
categories: 
---

Both iOS and Android have UI automation frameworks for driving the UI which is great for integration/acceptance testing for your app.  However, when you're using a web/native hybrid framework like Cordova, this can get tricky.

If you come from the Ruby world, you may also be used to using Cucumber for integration testing. While the testing landscape for hybrid apps is a little rocky, a lot of smart people are working on some great tools to improve things. With some effort, you can have Cucumber-based integration spec suite up and running for your hybrid app with relative ease.

<!-- more -->

<p><em><strong>Updated 1st March 2015:</strong> fixed typos</em></p>

## The Main Players

### Appium

[Appium](http://appium.io) can launch your app and interact with it via the platform's automation framework. It provides a Selenium remote compatible interface to your app that you can use with an driver that supports it.

### Selenium WebDriver JS

We're going to use [WebDriver JS](https://code.google.com/p/selenium/wiki/WebDriverJs) - the official Javascript driver for the Selenium project.  The documentation is a little thin on examples but once you get the hang of it

The web driver talks to any Seleinum-compatible REST-style API over HTTP. For our purposes this will be Appium but you can also point it at services like Browser stack which support a compatible API.

### cucumberjs

[Cucumberjs](https://github.com/cucumber/cucumber-js) is an active and reasonably featured Javascript port of the [Cucumber toolset](http://cukes.info).

### Your app

I'm assuming you're working on a hybrid app using the latest Cordova (4.x at the time of last review). 

## Setting up

Appium is available as an npm package:

```
npm install appium
```

There's also an [OSX app](https://bitbucket.org/appium/appium.app/downloads/) available.

There are a few platform specific steps you'll need to carry out to get up and running which you can find in the [Appium Getting Started guide](http://appium.io/getting-started.html).

On iOS for example, you need to run:

```
sudo authorize_ios
```

to allow Appium to use UI Automation and the simulator.

Next, you'll need to install a few node modules:

```
npm install -g cucumber selenium-webdriver
```

You can also use [Grunt](http://gruntjs.com) to manage these modules. The `grunt-cucumber` has various tasks for running your specs.

You'll need to setup a few directories in your app yourself:

```
features/
    step_definitions/
    support/
```

## Creating the World

The World class gives common setup and configuration to your cucumber environment.  Create `features/support/world.js`:

```javascript
require('path')
var appPath = __dirname + '/../../relative/path/to/my/cordova/built/app/MyApp.app';
var webdriver = require("selenium-webdriver");

var driver = new webdriver.Builder().
  withCapabilities({
    browserName: 'iOS',
    platform:    'Mac',
    version:     '8.1',
    app:         appPath
  }).
  usingServer('http://localhost:4723/wd/hub').
  build();

var World = function World(callback) {
    this.driver = driver;

    callback();
};

exports.World = World;
```

As you can see, the webdriver is setup to send configuration details to the Appium interface. We pass in versioning information along with the path to the app we'd like to launch.

## First Steps

Create `features/step_definitions/app_steps.js`:

```javascript
var appSteps = function () {
  this.World = require("../support/world.js").World;

  this.Given(/^I load the app$/, function(callback) {
    var driver = this.driver;

    driver.getAllWindowHandles().then(function(handles) {
      driver.switchTo().window(handles[0]).then(function() {
        callback();
      });
    });
  });

  this.Then(/^I should see "([^"]*)"$/, function(text, callback) {
    this.driver.getPageSource().then(function(source) {
      if(source.match(new RegExp(text)) {
        callback();
      else {
        callback.failure();
      }
    });
  });
};

module.exports = appSteps;
```

Take particular note of the 'I load the app' step. This code selects the `UIWebView` that contains your hybrid app as the main window to drive. Without this, you'll be running against the native app.

One gotcha here is the webdriver syntax. It uses promises which can be a little strange to work with if you're coming from other platforms. I'll be digging deeper on this syntax in a future post.

With these steps we can build a basic cucumber feature:

```cucumber
Feature: App load
  As a user
  I want to load the app
  So that I can experience great joy

  Scenario: Loading the app successfully
    Given I load the app
    Then I should see "Hello"
```

Save this as `features/app_load.feature`. Replace 'Hello' with some text that appears on the first screen of your app.

## Running

Try this all out by running cucumberjs:

```
cucumber.js
```

You should see the simulator start up at this point, hopefully followed by some pleasing pass messages:


```
..

1 scenario (1 passed)
2 steps (2 passed)
```

By this point I hope you're up and running with the stack. Next time, we'll dig a little further into the Selenium webdriver.

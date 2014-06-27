---
layout: post
title: "Localized Javascript with gettext"
date: 2014-06-06 17:05
comments: true
categories:
---

Today I'm going to give you a brief overview of some tools you can use to do localization in Javascript. [gettext]() has been around since the mid 90s and while it started in C, it has implementations in most popular languages. gettext uses natural language messages as keys in your code to look up translations in a message catalog.

Once you've added the messages to your code, you'll build a base message catalog. From that base, you'll generate translation files that can be given to translators.

The good thing about such a mature standard is that the tooling is quite stable. At the end I'll discuss how your translators can use a friendly GUI to do the translation work.

## Getting started

We'll be using a few libraries modules for this:

* [Jed]() for loading translations and outputting text
* [jsxgettext]() for extracting messages
* [gettext]() for working with message & translation catalogs.

Jed and jsxgettext are npm modules while gettext is avilable via [homebrew]() (if it's not already on your machine).

## In the code

```javascript
var i18n = new Jed({});
```

Using messages in code is easy and readable:

```javascript
var welcomeMessage = i18n.gettext('Welcome to my website!");
```

If you [create a simple handlebars helper](link to github sample) your templates can also contain keys:

```javascript
{{ tr 'Welcome to my website!'}}
```

## Extracting gettext keys

Once you've added the keys to your code, you can extract them out into a `.po` file which serves as the base catalog for the text:

```shell
jsxgettext -o translations/base.po
```

You'll end up with something that looks like this:

## Translation files

With the base catalog in place, you can generate translation `.po` files for different languages:

```shell
msginit --locale=js --input=translations/base.pot -o translations/ja.po'
```

Take a look at the `.po` file and you'll see some of what makes gettext so powerful:

Notice that the `.po` files track language teams and translators

If you add more keys to your code, you can update:

```shell
jsxgettext -o translations/base.po
msgmerge translations/ja.po translations/base.pot --update
```

## Translation workflow

POedit

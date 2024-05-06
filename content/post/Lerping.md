---
title: "Lerping"
date: 2024-05-03T22:52:30+05:30
# weight: 1
# aliases: ["/first"]
tags: ["Lerping"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Lerping"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

## What is Lerping?

Lerp, or Linear Interpolation, is a mathematical function in Unity that returns a value between two others at a point on a linear scale.

Most commonly it’s used for moving or changing values over a period of time.

So when you are doing "Linear Interpolation" you are Linearly inserting a new point between 2 points. Linear Interpolation is inserting a new point between 2 points on a straight line.

```
float a = 10;
float b = 50;
float t = 1;

lerpValue = Mathf.Lerp(a, b, t);

// Returns 50
```

## Use Cases

A common use for Lerp is to produce an effect over a fixed period of time.

For example, to animate a button, fade the screen to black or move an object to a new position in a fixed amount of time.

## Is it worth it?

For writing simple scripts lerp is useful. Otherwise I would recommend to buy assets such as Dot Tween which has more features.
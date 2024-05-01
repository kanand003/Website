---
title: "Caching"
date: 2024-04-22T22:03:31+05:30
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["Caching"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Caching"
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

# Caching

### What is Caching?

A cache is a high speed data storage which stores a subset of data, typically transient in nature, so that future requests for that data are served up faster than is possible by accessing the data’s primary storage location. Caching allows you to efficiently reuse previously retrieved or computed data.

### How does Caching work?
The data in a cache is generally stored in fast access hardware such as RAM (Random-access memory) and may also be used in correlation with a software component. A cache's primary purpose is to increase data retrieval performance by reducing the need to access the underlying slower storage layer.

Trading off capacity for speed, a cache typically stores a subset of data transiently, in contrast to databases whose data is usually complete and durable.

### Why is Caching Important?
Caching is important because it improves application and system performance by reducing the need to access slower storage layers. Caching stores multiple copies of data in a temporary storage location called a cache, which speeds up data retrieval. 

For example, when a user visits a website, their browser downloads data to load and display the page. Caching stores most of the content on the page on the device's hard drive, so the next time the user loads the page, most of the content is already stored locally and the page will load much more quickly.

https://newsletter.techworld-with-milan.com/p/caching-the-single-most-helpful-strategy?utm_source=profile&utm_medium=reader2
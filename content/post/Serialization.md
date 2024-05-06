---
title: "Serilization"
date: 2024-05-03T22:52:30+05:30
# weight: 1
# aliases: ["/first"]
tags: ["Serialization"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Serialization"
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

## What is Serialization?

Serialization is the process of converting a data object which is a combination of code and data into a series of bytes which is saved as transmissible object. The data can then be transferred to another destination.

## Why do we need to Serialize?

Serialization enables us to save the state of an object and recreate the object in a new location.Serialization encompasses both the storage of the object and exchange of data. Since objects are composed of several components, saving or delivering all the parts typically requires significant coding effort, so serialization is a standard way to capture the object into a sharable format.

With serialisation we can transfer objects:
- Over the wire for messaging use cases
- From application to application via web services such as REST APIs
- Through firewalls (as JSON or XML strings)
- Across domains
- To other data stores
- To identify changes in data over time
- While honoring security and user-specific details across applications

## What is Deserialization?

Deserialization is the process of reconstructing a data structure or object from a series of bytes or a string in order to instantiate the object for consumption. This is the reverse process of serialization, i.e., converting a data structure or object into a series of bytes for storage or transmission across devices.
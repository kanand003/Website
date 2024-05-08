---
title: "Structs_VS_Classes"
date: 2024-05-08T21:57:34+05:30
# weight: 1
# aliases: ["/first"]
tags: ["Structs"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
#description: ""
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: true
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
## What are Structs?

Structs are similar to classes in that they represent data structures that can contain data members and function members. Structs are best used when you need to represent simple data types, such as integers, strings, or other basic data types.

A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.

## What are Classes?

Classes are typically used to model real-world objects, such as cars or people in a program.

## Difference Between Structs and Classes

One major difference between structs and classes is that structs are value types, while classes are reference types. This means that structs are copied by value when they are passed around, while classes are copied by reference.

-When you pass a struct to a method, you’re passing a copy of the data. This can cause performance issues if you’re working with large structs.
-Another difference is that structs cannot inherit from other structs, while classes can inherit from other classes. This allows you to create more complex object hierarchies with classes.

-Additionally, structs are typically used for smaller, simpler data structures, while classes are used for more complex objects that require methods and properties.

-Structs are often used for basic data types like integers, floats, and booleans, while classes are used for objects like cars, animals, and people.

## Memory Allocation for Structs vs Class

When you create a struct, its memory is allocated on the stack. This makes structs more efficient than classes, which are allocated on the heap. This means that structs are more suitable for functions that require high performance and low memory usage.

One drawback of using structs is that they have a size limit of 16 bytes. If your struct’s size exceeds this limit, it will be allocated on the heap instead of the stack. This can cause performance issues if you’re working with large structs.

On the other hand, classes are allocated on the heap, which means they have no size limit. This makes them more suitable for complex data structures that require a large amount of memory.

However, this also means that classes are less efficient than structs and can cause performance issues if used in functions that require high performance and low memory usage.

## Example

```
struct Location
{
    public int x, y;

    public Location(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Location a = new Location(20, 20);
        Location b = a;
        a.x = 100;

        // Print the value of b.x
        Console.WriteLine(b.x);

        // Output: 20
    }
}
```
---
title: "Singleton"
date: 2024-04-22T22:03:31+05:30
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["Singleton"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Singleton Pattern"
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
# Singleton Pattern in Unity

## 1. Introductory Overview
- **Pattern Name**: Singleton Pattern
- **One-Sentence Summary**: The Singleton pattern ensures that a class has only one instance and provides a global point of access to it, making it ideal for managing game-wide services in Unity.
<!-- - **Visual/GIF**: ![Singleton Pattern Diagram](path/to/your/singleton-diagram.png)  
  *(Replace with the actual path to your visual aid)* -->
## 2. Problem Context
- **Practical Scenario**: In many games, you need a centralized manager for handling game states, audio, or settings. For example, a GameManager that persists across scenes to track player progress and game state.
- **Relatable Context**: Managing multiple instances of a game manager can lead to inconsistent game states and bugs, making the Singleton pattern a practical solution.

## 3. Implementation Guide
- **Code Snippets**: 
    ```csharp
    // SingletonExample.cs
    using UnityEngine;

    public class SingletonExample : MonoBehaviour
    {
        private static SingletonExample _instance;

        public static SingletonExample Instance
        {
            get
            {
                if (_instance == null)
                {
                    _instance = FindObjectOfType<SingletonExample>();
                    if (_instance == null)
                    {
                        GameObject singletonObject = new GameObject();
                        _instance = singletonObject.AddComponent<SingletonExample>();
                        singletonObject.name = typeof(SingletonExample).ToString() + " (Singleton)";
                    }
                }
                return _instance;
            }
        }

        private void Awake()
        {
            if (_instance != null && _instance != this)
            {
                Destroy(gameObject);
            }
            else
            {
                _instance = this;
                DontDestroyOnLoad(gameObject);
            }
        }

        public void ExampleMethod()
        {
            Debug.Log("Singleton method called!");
        }
    }
    ```
- **Annotated Comments**: 
    - Add comments in the code snippets to explain the purpose of each section, such as:
        ```csharp
        // Static instance of the class
        private static SingletonExample _instance;
        ```

## 4. Pros and Cons
- **Pros**:
    - Ensures a single instance, preventing conflicts.
    - Easy global access to the instance.
    - Useful for managing game-wide services.
- **Cons**:
    - Can lead to tight coupling if overused.
    - Difficult to test due to global state.
- **Alternatives**: Discuss alternatives like Dependency Injection for more complex scenarios.

## 5. Conclusion
- **Key Takeaways**: The Singleton pattern is a powerful tool for managing global state in Unity, but it should be used judiciously to avoid potential pitfalls.
- **Tips for Extension**: Consider combining the Singleton pattern with other design patterns, like the Observer pattern, to create a more flexible architecture.

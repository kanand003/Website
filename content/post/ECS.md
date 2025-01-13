---
title: "Simple Entity Component System Implementation in C++"
date: 2025-01-13T22:54:51+05:30
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["ECS","C++"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: "A practical guide to implementing a simple Entity Component System (ECS) in C++"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: false
disableShare: false
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

Entity Component System (ECS) is a software architectural pattern commonly used in game development that follows composition over inheritance. In this post, we'll implement a simple but functional ECS in C++.

## What is ECS?

ECS consists of three main parts:
- **Entities**: Simple IDs that serve as containers for components
- **Components**: Pure data structures that hold state
- **Systems**: Logic that operates on entities with specific components

## Basic Implementation

Let's start with a simple implementation that demonstrates the core concepts.

### 1. Entity Manager

First, we'll create an entity manager to handle entity creation and destruction:

```cpp
#include <set>
#include <queue>

class EntityManager {
private:
    std::queue<uint32_t> availableIds;
    std::set<uint32_t> livingEntities;
    uint32_t nextId = 0;

public:
    uint32_t createEntity() {
        uint32_t id;
        if (availableIds.empty()) {
            id = nextId++;
        } else {
            id = availableIds.front();
            availableIds.pop();
        }
        livingEntities.insert(id);
        return id;
    }

    void destroyEntity(uint32_t entity) {
        livingEntities.erase(entity);
        availableIds.push(entity);
    }

    bool isAlive(uint32_t entity) const {
        return livingEntities.find(entity) != livingEntities.end();
    }
};
```

### 2. Component Storage

Next, we'll implement component storage using a simple sparse set approach:

```cpp
#include <unordered_map>
#include <any>
#include <memory>

class ComponentStorage {
private:
    std::unordered_map<uint32_t, std::any> components;

public:
    template<typename T>
    void addComponent(uint32_t entity, T component) {
        components[entity] = component;
    }

    template<typename T>
    T* getComponent(uint32_t entity) {
        auto it = components.find(entity);
        if (it != components.end()) {
            return std::any_cast<T>(&it->second);
        }
        return nullptr;
    }

    void removeComponent(uint32_t entity) {
        components.erase(entity);
    }
};
```

### 3. Example Components

Here are some example components we might use in a game:

```cpp
struct Position {
    float x, y;
};

struct Velocity {
    float dx, dy;
};

struct Renderable {
    std::string sprite;
    float scale;
};
```

### 4. System Implementation

Now let's implement a simple movement system:

```cpp
class MovementSystem {
private:
    ComponentStorage& positionStorage;
    ComponentStorage& velocityStorage;

public:
    MovementSystem(ComponentStorage& pos, ComponentStorage& vel)
        : positionStorage(pos), velocityStorage(vel) {}

    void update(float deltaTime) {
        // In a real implementation, you'd want to iterate only over entities
        // that have both Position and Velocity components
        for (uint32_t entity = 0; entity < MAX_ENTITIES; ++entity) {
            auto pos = positionStorage.getComponent<Position>(entity);
            auto vel = velocityStorage.getComponent<Velocity>(entity);

            if (pos && vel) {
                pos->x += vel->dx * deltaTime;
                pos->y += vel->dy * deltaTime;
            }
        }
    }
};
```

## Usage Example

Here's how to use our simple ECS:

```cpp
int main() {
    EntityManager entityManager;
    ComponentStorage positionStorage;
    ComponentStorage velocityStorage;
    
    // Create an entity
    uint32_t player = entityManager.createEntity();
    
    // Add components
    positionStorage.addComponent(player, Position{0.0f, 0.0f});
    velocityStorage.addComponent(player, Velocity{1.0f, 2.0f});
    
    // Create and update system
    MovementSystem movementSystem(positionStorage, velocityStorage);
    movementSystem.update(1.0f);
    
    // Get updated position
    auto* pos = positionStorage.getComponent<Position>(player);
    if (pos) {
        std::cout << "Player position: " << pos->x << ", " << pos->y << std::endl;
    }
    
    return 0;
}
```

## Advantages of ECS

1. **Flexibility**: Easy to add or remove components at runtime
2. **Performance**: Data-oriented design leads to better cache utilization
3. **Modularity**: Systems are isolated and can be easily added or modified
4. **Reusability**: Components can be mixed and matched to create different entity types

## Improvements

This is a basic implementation that can be enhanced in several ways:

1. Use a proper component type ID system
2. Implement archetype-based storage for better performance
3. Add system dependencies and execution order
4. Implement component pools for better memory management
5. Add event system for entity/component changes

## Conclusion

This simple ECS implementation demonstrates the basic concepts while remaining easy to understand. For production use, you might want to consider using established ECS libraries like EnTT or build upon this foundation with the improvements mentioned above.

Remember that ECS is just one of many architectural patterns, and it's important to choose the right tool for your specific needs. ECS shines in scenarios with many entities sharing similar components and behaviors, making it particularly well-suited for games and simulations.


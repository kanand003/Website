---
title: "Tower Defense Game"
date: 2023-08-01T22:37:32+05:30
draft: false
cover:
    image: "/images/Capture.png"
description: ""
summary: ""
tags: []
ShowReadingTime: true
ShowWordCount: true    
---

## Introduction

A Tower Defense game prototype implemented in Unity, featuring pathfinding algorithms for enemy movement and strategic tower placement mechanics. The game demonstrates core tower defense gameplay elements while showcasing efficient pathfinding implementation.

## Features

### Enemy Pathfinding
- Implemented A* pathfinding algorithm for intelligent enemy movement
- Dynamic path recalculation when towers block paths
- Efficient path caching to optimize performance

### Tower Mechanics
- Multiple tower types with different attack patterns
- Strategic tower placement affecting enemy paths
- Tower upgrade system with enhanced capabilities

### Wave System
- Progressive difficulty scaling
- Dynamic enemy spawning patterns
- Wave completion rewards

## Technical Implementation

### Pathfinding Algorithm
```csharp
public class PathFinder : MonoBehaviour
{
    private Grid grid;
    private List<Node> openSet;
    private HashSet<Node> closedSet;

    public List<Node> FindPath(Vector3 startPos, Vector3 targetPos)
    {
        Node startNode = grid.NodeFromWorldPoint(startPos);
        Node targetNode = grid.NodeFromWorldPoint(targetPos);

        openSet = new List<Node> { startNode };
        closedSet = new HashSet<Node>();

        while (openSet.Count > 0)
        {
            Node currentNode = openSet[0];
            // A* algorithm implementation
            // Path finding logic
        }

        return RetracePath(startNode, targetNode);
    }
}
```

### Tower System
```csharp
public class Tower : MonoBehaviour
{
    [SerializeField] private float range = 5f;
    [SerializeField] private float fireRate = 1f;
    private Transform target;

    void UpdateTarget()
    {
        // Find nearest enemy
        // Attack logic
        // Damage calculation
    }

    void Upgrade()
    {
        // Upgrade stats
        // Visual updates
    }
}
```

## Future Improvements

1. Additional tower types and enemy variants
2. Advanced wave patterns and boss enemies
3. Power-up system
4. Enhanced visual effects
5. Level progression system

## Resources

- [Project Repository](https://github.com/kanand003/Tower)
- [Unity Documentation](https://docs.unity3d.com/)
- [A* Pathfinding Tutorial](https://www.redblobgames.com/pathfinding/a-star/introduction.html)

<!--Add photo -->
---
title: "Draw Calls in Unity"
date: 2025-03-22T20:20:12+05:30
draft: false
tags: ["Unity", "Performance", "Graphics"]
author: "Me"
# weight: 1 // To Pin a Post
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: ""
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
---

## Introduction

A draw call in Unity refers to the process where the game engine sends a request to the GPU to render objects in the scene. It involves setting up the necessary state for rendering (e.g., material, shaders, textures, meshes) and issuing the command to render a particular object or group of objects. Each time an object requires a unique material, shader, or other rendering properties, a new draw call is made.

## Impact on Performance

More draw calls lead to greater overhead because the CPU must manage and send more commands to the GPU, leading to increased latency and reduced frame rate.

### Mobile Performance Targets

Mobile devices are more resource-constrained than desktop systems, and therefore managing draw calls is crucial for achieving optimal performance.

- **Lower-end mobile devices**: Aim for below 100 draw calls per frame
- **Mid-range devices**: Target 100-200 draw calls per frame
- **Higher-end devices**: Can handle up to 200 or slightly more draw calls per frame

## Optimizing Draw Calls

### 1. Static Batching
- Combine meshes where possible
- Each static batch can include up to 64000 vertices
- If vertex count exceeds 64000, Unity creates another batch

### 2. Dynamic Batching
Requirements for dynamic batching to work:
- Objects must share the same material and shader
- Meshes must have a vertex count of 900 or fewer
- No skinned meshes or objects with different shadow settings
- Objects should not have drastically different transform positions
- Does not work on objects with the SkinnedMeshRenderer component

### 3. Material Optimization
- Use texture atlases to reduce material switches
- For batching to work, objects must use the exact same material asset
- Making a copy of a material and changing values prevents batching
- Use GPU instancing to render many copies of the same object in a single draw call

### 4. Additional Optimization Techniques
- Optimize shaders and materials: Reduce the number of unique materials
- Efficient lighting: Use baked lighting where appropriate
- Avoid per-frame lighting calculations

## References

- Unity Documentation: Draw Call Batching
- Unity Performance Optimization Guide


---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
url: "/projects/{{ .Name }}"
image: "/Website/images/{{ .Name }}.jpg"  # Main project image
description: ""
summary: ""
tags: []
ShowReadingTime: true
ShowWordCount: true
---

## Introduction

[Brief project introduction]

## Project Preview

<!-- Main project image with styling -->
<div style="max-width: 800px; margin: 20px auto;">
    <img src="/Website/images/{{ .Name }}.jpg" alt="{{ replace .Name "-" " " | title }} Preview" style="width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
</div>

## Demo Video

<!-- YouTube video embed with responsive container -->
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; border-radius: 8px; margin: 20px auto;">
    <!-- Replace VIDEO_ID with your YouTube video ID -->
    <iframe 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);" 
        src="https://www.youtube.com/embed/VIDEO_ID" 
        title="{{ replace .Name "-" " " | title }} Demo"
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
    </iframe>
</div>

## Features

- Feature 1
- Feature 2
- Feature 3

## Technologies Used

- Tech 1
- Tech 2
- Tech 3

## Implementation Details

[Describe the technical implementation]

## Challenges and Solutions

[Discuss interesting problems solved]

## GitHub Repository

[Add link to GitHub repository]

## Additional Screenshots

<!-- Additional screenshots with grid layout -->
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin: 20px 0;">
    <!-- Add more screenshots as needed -->
    <!-- Example:
    <div style="border-radius: 8px; overflow: hidden; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
        <img src="/Website/images/screenshot1.jpg" alt="Feature 1" style="width: 100%; height: auto;">
    </div>
    -->
</div> 
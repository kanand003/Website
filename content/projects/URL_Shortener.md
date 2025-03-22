---
title: "URL Shortener Service using Go"
date: 2024-09-02T22:25:12+05:30
draft: false
url: "/projects/URL_Shortener"
image: "/Website/images/URL_Shortener.jpg"  # Main project image
description: "A simple and efficient URL shortening service built with Go"
summary: "Lightweight URL shortener with in-memory storage and fast redirection"
tags: ["Web Development", "Go", "HTTP", "Regex"]
ShowReadingTime: true
ShowWordCount: true
---

## Introduction

A URL shortener is a tool that takes a long URL and converts it into a shorter, more manageable link. This project implements a lightweight and efficient URL shortening service using Go's standard library, featuring in-memory storage and fast URL redirection.

## Features

- Fast URL shortening with random string generation
- URL validation using regex
- In-memory storage for quick access
- Simple HTTP server implementation
- Automatic redirection to original URLs
- List view of all shortened links
- Duplicate URL handling

## Technologies Used

- Go (Programming Language)
- net/http (Standard HTTP package)
- regexp (Regular expressions)
- math/rand (Random string generation)

## Implementation Details

The URL shortener is built using Go's standard library components. Here are the key code snippets showing the core functionality:

### URL Storage and Initialization
```go
var (
    linkList map[string]string
)

func init() {
    rand.Seed(time.Now().UnixNano())
}
```
The application uses an in-memory map to store URL mappings and initializes the random number generator for creating unique short codes.

### URL Validation
```go
func validLink(link string) bool {
    r, err := regexp.Compile("^(http|https)://")
    if err != nil {
        return false
    }
    link = strings.TrimSpace(link)
    return r.MatchString(link)
}
```
URLs are validated using regex to ensure they start with http:// or https://.

### Short URL Generation
```go
const letterBytes = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

func randStringBytes(n int) string {
    b := make([]byte, n)
    for i := range b {
        b[i] = letterBytes[rand.Intn(len(letterBytes))]
    }
    return string(b)
}
```
Generates random 10-character strings using alphanumeric characters for short URLs.

### URL Redirection
```go
func getLink(w http.ResponseWriter, r *http.Request) {
    path := r.URL.Path
    pathArgs := strings.Split(path, "/")
    if len(pathArgs[2]) < 1 {
        w.WriteHeader(http.StatusNotFound)
        http.Redirect(w, r, "http://localhost:9000/", http.StatusTemporaryRedirect)
        return
    }
    http.Redirect(w, r, linkList[pathArgs[2]], http.StatusTemporaryRedirect)
}
```
Handles redirection from short URLs to their original destinations.

Key components include:
- In-memory storage using map[string]string
- URL validation using regex
- Random string generation for short URLs
- HTTP handlers for different endpoints
- Automatic redirection to original URLs
- Simple HTML response for the home page

## Challenges and Solutions

1. **URL Validation**: Implemented regex-based validation to ensure only valid HTTP/HTTPS URLs are accepted
2. **Storage**: Used in-memory map for fast access and simple implementation
3. **Random Generation**: Created efficient random string generation for unique short URLs
4. **Error Handling**: Implemented proper HTTP status codes and error messages

## GitHub Repository

[View the project on GitHub](https://github.com/kanand003/URL_Shortener)

## Future Improvements

### Enhanced Features
1. **Persistence Layer**
   - Database integration (PostgreSQL/MongoDB) for permanent storage
   - URL expiration and automatic cleanup
   - Backup and restore functionality

2. **Analytics and Tracking**
   - Click count tracking
   - Geographic location tracking
   - Referrer tracking
   - Analytics dashboard

3. **User Management**
   - User authentication and authorization
   - Custom URL aliases
   - URL categorization and tagging
   - User-specific URL management

4. **Advanced URL Features**
   - QR code generation for shortened URLs
   - URL preview with title and description
   - Password protection for sensitive links
   - Link expiration dates
   - Click limits per URL

5. **API Enhancements**
   - RESTful API with authentication
   - Rate limiting
   - Bulk URL shortening
   - API documentation (Swagger/OpenAPI)
   - Webhook support for click events

6. **Security Improvements**
   - HTTPS enforcement
   - Malware scanning for URLs
   - Rate limiting per IP
   - CAPTCHA for bulk operations
   - URL blacklisting

7. **UI/UX Improvements**
   - Modern web interface
   - Mobile-responsive design
   - Dark/Light theme
   - Copy-to-clipboard functionality
   - URL validation feedback
   - Loading states and animations

8. **Performance Optimizations**
   - Caching layer (Redis)
   - CDN integration
   - Load balancing
   - Database indexing
   - Connection pooling

9. **Monitoring and Maintenance**
   - Health check endpoints
   - Performance metrics
   - Error logging and monitoring
   - Automated testing
   - CI/CD pipeline

10. **Additional Features**
    - Link preview cards
    - Social media sharing buttons
    - Custom domain support
    - URL statistics and reports
    - Bulk import/export functionality

These improvements would transform the project from a basic URL shortener into a full-featured URL management platform suitable for production use.




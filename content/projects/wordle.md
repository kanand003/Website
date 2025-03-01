---
title: "Wordle"
date: true
draft: false
url: "/projects/wordle"
description: "A clone of Wordle made in C++"
summary: ""
tags: []
ShowReadingTime: true
ShowWordCount: true
---

## Introduction

A desktop implementation of the popular word game Wordle, built using C++ and SFML framework. The game features a clean user interface, word validation, and visual feedback similar to the original web version.

## Features

- Daily word challenges
- Keyboard input handling
- Real-time visual feedback
- Word validation system
- Score tracking
- Animated tile reveals

## Implementation Details

### Game Core
```cpp
class WordleGame {
public:
    WordleGame();
    void processInput(char letter);
    void checkWord();
    bool isGameOver() const;
    
private:
    std::string targetWord;
    std::vector<std::string> attempts;
    int currentRow;
    int currentCol;
    bool gameWon;
    
    void loadWordList();
    bool isValidWord(const std::string& word);
    std::vector<LetterState> evaluateGuess(const std::string& guess);
};
```

### UI System
```cpp
class GameUI {
public:
    GameUI(sf::RenderWindow& window);
    void draw();
    void updateTile(int row, int col, char letter, TileState state);
    void updateKeyboard(char key, KeyState state);
    
private:
    sf::RenderWindow& window;
    std::array<std::array<Tile, 5>, 6> tiles;
    std::map<char, Key> keyboard;
    
    void initializeTiles();
    void initializeKeyboard();
    void animateTileReveal(int row);
};

class Tile {
public:
    void setLetter(char letter);
    void setState(TileState state);
    void animate();
    void draw(sf::RenderWindow& window);
    
private:
    sf::RectangleShape background;
    sf::Text text;
    TileState state;
    float animationProgress;
};
```

### Word Validation
```cpp
class WordValidator {
public:
    WordValidator();
    bool isValid(const std::string& word);
    std::string getRandomWord();
    
private:
    std::unordered_set<std::string> wordList;
    std::vector<std::string> dailyWords;
    
    void loadWordList(const std::string& filename);
    void loadDailyWords(const std::string& filename);
};
```

## Technical Features

### Graphics
- Custom UI components
- Smooth animations
- Color-coded feedback
- Responsive keyboard display

### Game Logic
- Word validation against dictionary
- Letter position checking
- Multiple attempt tracking
- Win/lose state management

### Input System
- Keyboard input handling
- Virtual keyboard support
- Input validation
- Backspace and Enter key handling

## Development Challenges

1. **Word List Management**
   - Efficient storage and lookup of valid words
   - Daily word selection algorithm
   - Word difficulty balancing

2. **UI Design**
   - Responsive tile animations
   - Color state management
   - Keyboard layout implementation
   - Text rendering optimization

3. **Game State Handling**
   - Progress tracking
   - Game state persistence
   - Error handling
   - Input validation

## Future Improvements

1. Statistics tracking
2. Daily challenge mode
3. Custom word length options
4. Multiplayer support
5. Theme customization
6. Achievement system

## Resources

- [Project Repository](https://github.com/kanand003/WordleClone)
- [SFML Documentation](https://www.sfml-dev.org/documentation/2.5.1/)
- [Original Wordle](https://www.nytimes.com/games/wordle/index.html)

<!--Add photo -->
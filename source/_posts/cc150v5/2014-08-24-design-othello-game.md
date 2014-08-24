---
layout: post
title: "[CC150v5] 8.8 Design Othello Game "
comments: true
category: CC150v5
tags: [  ]
---

### Question

> Othello is played as follows: Each Othello piece is white on one side and black on the other. When a piece is surrounded by its opponents on both the left and right sides, or both the top and bottom, it is said to be captured and its color is flipped. 

> The win is assigned to the person with the most pieces. Implement the object-oriented design for Othello. 

### Class

1. Game
	1. Two Player objects
	1. a board object
	1. singleton class (unless otherwise specified, this needs to be discussed)
1. Board
	1. Keep the score (black/white count). Of course we can put score in Game Class as well, it seems logically related to the board a bit more. 
	1. Array of Piece objects
	1. getScore() method
1. Piece
	1. stores color info
	1. flip() function
1. Player
	1. stores color info
	1. playPiece() method
1. Color Enum
1. Direction Enum

### Functions 

1. placePiece() by the Player (which triggers the following 2 methods)
1. private flipSection(Position fromWhere, Color c, Direction up/down/left/right) by the board
1. private updateScore() by the board
1. getScore() by the board

#### Follow up: Do we need separate Board and Game classes?

Strictly speaking, no. The drawback is adding an extra layers. A function that calls Game class is immediately calling Board class. 

But keeping the objects separate allows us to have a logical separation between the board (which contains just logic involving placing pieces) and the game (which involves times, game flow, etc.). 

### Conclusion

This is an easy, and very standard OOD question. Keep the logic clear, design the layers and object hierarchy, and the rest of things will come naturally. 

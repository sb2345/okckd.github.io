---
layout: post
title: "[Google] Winner of tic-tac-toe"
comments: true
category: Google
tags: [  ]
---

### Question 

[link](http://www.glassdoor.com/Interview/How-would-you-determine-if-someone-has-won-a-game-of-tic-tac-toe-on-a-board-of-any-size-QTN_1104.htm)

> How would you determine if someone has won a game of tic-tac-toe on a board of any size? 

### Solution

First, confirm that when the number of pieces in a line equals to the dimension of the board, one person wins. Eg. for 10 * 10 board, 10 pieces need to be in 1 line. 

__[We can determine](http://www.glassdoor.com/Interview/How-would-you-determine-if-someone-has-won-a-game-of-tic-tac-toe-on-a-board-of-any-size-QTN_1104.htm) if someone has won during a game in real time, as in checking after every move. 

> Create an array of size 2n+2 at the beginning of the game and fill it with zeros. Each spot in the array will be a sum of X's or O's horizontally (the first n places in the array), vertically (the second n places in the array) and diagonally (the last 2 places). Then with every move, you add 1 to the 2 places (or 3 if on a diagnol) of the array if X, and subtract 1 if its an O. After adding you check and see if the value of the array is equal to n or -n, if it is, n mean X has won and -n means O has won.

### Code

__not written__

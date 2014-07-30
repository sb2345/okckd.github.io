---
layout: post
title: "[Question] Nth Fibonacci Number In O(LogN)"
comments: true
category: General
tags: [  ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2010/09/nth-fibbonacci-number-in-ologn.html)

> Find Nth fibonacci number in O(logN) time complexity.

### Analysis

{% img middle /assets/images/fibonacci_matrix.png %}

It's a recursive sequence, where we can get the following equation: 

	A* [ F(1) F(0) ] = [ F(2) F(1) ]
	A* [ F(2) F(1) ] = [ F(3) F(2) ] = A^2 * [ F(1) F(0) ]
	A* [ F(3) F(2) ] = [ F(4) F(3) ] = A^3 * [ F(1) F(0) ]
	..
	..
	..
	..
	A* [ F(n) F(n-1) ] = [ F(n+1) F(n) ] = A^n * [ F(1) F(0) ]

### Solution


### Code

__not written by me__



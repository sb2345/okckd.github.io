---
layout: post
title: "[CC150v4] 19.4 Get Max Number with >, < operator "
comments: true
category: CC150v4
tags: [  ]
---

### Question

> Write a method which finds the maximum of two numbers. You should not use if-else or any other comparison operator.

> EXAMPLE
>
> Input: 5, 10
>
> Output: 10

### Solution

We can't use >, < or if-else statement, but we can use mathematical operator like subtract and bit operators. 

Calculate (a-b) and do (a + K(a-b)) can help us (where K is either 0 or -1). 

### Code

	public static int getMax(int a, int b) {
		int c = a - b;
		int signBit = c >> 31 & 1;
		// if (a-b) is negative, sign = 1
		// otherwise, sign = 0
		return a - signBit * c;
	}

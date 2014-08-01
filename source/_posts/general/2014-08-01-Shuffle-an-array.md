---
layout: post
title: "[Question] Shuffle a given array"
comments: true
category: General
tags: [  ]
---

### Question 

[link](http://www.geeksforgeeks.org/shuffle-a-given-array/)

> Given an array, generate a random permutation of array elements. 

### Analysis

This is called __[Fisher–Yates shuffle](http://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)__. Proof can be seen at question post: 

> The probability that ith element goes to second last position can be proved to be 1/n by dividing it in two cases.

> Case 1: i = n-1 (index of last element):

> The probability of last element going to second last position is = (probability that last element doesn't stay at its original position) x (probability that the index picked in previous step is picked again so that the last element is swapped)

> So the probability = ((n-1)/n) x (1/(n-1)) = 1/n

> Case 2: 0 < i < n-1 (index of non-last):

> The probability of ith element going to second position = (probability that ith element is not picked in previous iteration) x (probability that ith element is picked in this iteration)

> So the probability = ((n-1)/n) x (1/(n-1)) = 1/n

> We can easily generalize above proof for any other position. 

### Solution

O(n) time complexity. 

	To shuffle an array a of n elements (indices 0..n-1):
	  for i from n − 1 downto 1 do
	       j ← random integer with 0 ≤ j ≤ i
	       exchange a[j] and a[i]

Note the RNG is having limit from 0 to i, and number i keeps decreasing. 

### Code

__not written by me__

	def sattoloCycle(items):
	    i = len(items)
	    while i > 1:
	        i = i - 1
	        j = randrange(i)  # 0 <= j <= i-1
	        items[j], items[i] = items[i], items[j]
	    return

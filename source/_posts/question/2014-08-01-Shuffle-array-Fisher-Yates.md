---
layout: post
title: "[Question] Shuffle An Array (Fisher–Yates) "
comments: true
category: Question
tags: [  ]
---

### Question 

[link](http://www.geeksforgeeks.org/shuffle-a-given-array/)

> Given an array, generate a random permutation of array elements. 

### Solution

O(n) time complexity. 

	To shuffle an array a of n elements (indices 0..n-1):
	  for i from n − 1 downto 1 do
	       j ← random integer with 0 ≤ j ≤ i
	       exchange a[j] and a[i]

Note the RNG is having limit from 0 to i, and number i keeps decreasing. 

### Proof

This is called __[Fisher–Yates shuffle](http://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)__. Proof can be seen at question post: 

> The probability that ith element goes to second last position can be proved to be 1/n by dividing it in two cases.

> Case 1: i = n-1 (index of last element):

> The probability of last element going to second last position is = (probability that last element doesn't stay at its original position) x (probability that the index picked in previous step is picked again so that the last element is swapped)

> So the probability = ((n-1)/n) x (1/(n-1)) = 1/n

> Case 2: 0 < i < n-1 (index of non-last):

> The probability of ith element going to second position = (probability that ith element is not picked in previous iteration) x (probability that ith element is picked in this iteration)

> So the probability = ((n-1)/n) x (1/(n-1)) = 1/n

> We can easily generalize above proof for any other position. 

__Updated on Sep 10th, 2014__: analysis of the approach. This question is on CC150v4 Q20.2. 

Note that when we generate a new number between 0 and i, we swap it (with the last 'alive' number (ith number). __After this, ith number is 'dead'__. 

By doing it this way, we get a perfect shuffle! Idea is from cc150. 

### Code

__not written by me__, [link](http://www.geeksforgeeks.org/shuffle-a-given-array/)

	def sattoloCycle(items):
	    i = len(items)
	    while i > 1:
	        i = i - 1
	        j = randrange(i)  # 0 <= j <= i-1
	        items[j], items[i] = items[i], items[j]
	    return

__code from cc150__

	public static void shuffleArray(int[] cards) {
		int temp;
		int index;
		for (int i = 0; i < cards.length; i++) {
			index = (int) (Math.random() * (cards.length - i)) + i;
			// number at position 'i' is swapped with position 'index' (which is
			// random)
			temp = cards[i];
			cards[i] = cards[index];
			cards[index] = temp;
		}
	}

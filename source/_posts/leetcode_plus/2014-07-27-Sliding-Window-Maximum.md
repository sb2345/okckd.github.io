---
layout: post
title: "[LeetCode Plus] Sliding Window Maximum "
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---

### Question 

[link](http://leetcode.com/2011/01/sliding-window-maximum.html)

> A long array A[] is given to you. There is a sliding window of size w which is moving from the very left of the array to the very right. You can only see the w numbers in the window. Each time the sliding window moves rightwards by one position. Following is an example:
The array is [1 3 -1 -3 5 3 6 7], and w is 3.

    Window position                Max
    ---------------               -----
    [1  3  -1] -3  5  3  6  7       3
     1 [3  -1  -3] 5  3  6  7       3
     1  3 [-1  -3  5] 3  6  7       5
     1  3  -1 [-3  5  3] 6  7       5
     1  3  -1  -3 [5  3  6] 7       6
     1  3  -1  -3  5 [3  6  7]      7

> Input: A long array A[], and a window width w

> Output: An array B[], B[i] is the maximum value of from A[i] to A[i+w-1]

### Analysis

__The  naive approach is using a Heap__. This time complexity is O(n*logn). However, there is a better way using a (double-ended) queue. 

__We do not need to [keep all numbers](http://n00tc0d3r.blogspot.sg/2013/04/sliding-window-maximum.html)__. For example, suppose numbers in a window of size 4 are (1, 3, -1, 2). Obviously, no matter what next numbers are, 1 and -1 are never going to be a maximal as the window moving. The queue should look like (3, 2) in this case.

### Solution

1. When moves to a new number, iterate through back of the queue, removes all numbers that are not greater than the new one, and then insert the new one to the back.
1. FindMax only need to take the first one of the queue.
1. To remove a number outside the window, only compare whether the current index is greater than the front of queue. If so, remove it.

[A natural way](http://leetcode.com/2011/01/sliding-window-maximum.html) most people would think is to try to maintain the queue size the same as the window’s size. Try to break away from this thought and think out of the box. 

### Code

Code by N00tc0d3r. 

	public int[] windowMax(int[] nums, int window) {
		int w = (nums.length < window) ? nums.length : window;
		// A deque allows insertion/deletion on both ends.
		// Maintain the first as the index of maximal of the window
		// and elements after it are all smaller and came later than the first.
		Deque<Integer> que = new ArrayDeque<Integer>();

		// initialize window
		int i = 0;
		while (i < w) {
			while (!que.isEmpty() && nums[que.getLast()] <= nums[i]) {
				que.removeLast();
			}
			que.addLast(i++);
		}

		// sliding window
		int[] max = new int[nums.length - w + 1];
		max[i - w] = que.getFirst();
		while (i < nums.length) {
			// add new element
			while (!que.isEmpty() && nums[que.getLast()] <= nums[i]) {
				que.removeLast();
			}
			que.addLast(i);
			// remove old element if still in que
			if (!que.isEmpty() && i - w >= que.getFirst()) {
				que.removeFirst();
			}
			// get maximal
			++i;
			max[i - w] = que.getFirst();
		}

		return max;
	}

---
layout: post
title: "[CC150v5] 2.7 Linked List Palindrome "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Implement a function to check if a linked list is a palindrome. 

### Solution

There are multiple solutions for this question. 

__First, maybe the simplest solution of all__, is to compare the list with the reversed list (compare first half would be enough). This is a very nice idea. 

__Second solution is iterative approach__. My code below is to first get the total length, then __use a Stack__. Alternatively, we can also use __fast/slow pointer__ to find the mid point. This solution is easiest to write. 

__Third solution is recursive__. We basically uses a public pointer to: 

1. get starting value
1. check middle parts
1. get ending value
1. if starting == ending and middle part is valid, then true.

This code is not easy to write, and hard to think. 

It's best to know both iterative and recursive solution. 

### Code

Iterative

	public static boolean isPalindrome1(LinkedListNode head) {
		int len = getListLength(head);
		int half = len / 2;
		Stack<Integer> stack = new Stack<Integer>();
		for (int i = 0; i < half; i++) {
			stack.push(head.data);
			head = head.next;
		}
		if (len % 2 == 1) {
			head = head.next;
		}
		for (int i = 0; i < half; i++) {
			if (head.data != stack.pop()) {
				return false;
			}
			head = head.next;
		}
		return true;
	}

Recursive

	private static LinkedListNode p;

	public static boolean isPalindrome2(LinkedListNode head) {
		p = head;
		int len = getListLength(head);
		return helper2(0, len - 1);
	}

	public static boolean helper2(int from, int to) {
		if (from > to) {
			return true;
		} else if (from == to) {
			p = p.next;
			return true;
		} else {
			// first get fromVal, then check middlep part, last, get toVal
			int fromVal = p.data;
			p = p.next;
			if (!helper2(from + 1, to - 1)) {
				return false;
			}
			int toVal = p.data;
			p = p.next;
			if (fromVal != toVal) {
				return false;
			}
		}
		return true;
	}

Shared method:

	private static int getListLength(LinkedListNode node) {
		int count = 0;
		while (node != null) {
			count++;
			node = node.next;
		}
		return count;
	}

---
layout: post
title: "[CC150v5] 2.2 Kth last element (recursive) "
comments: true
category: CC150v5

---

### Question

> Implement an algorithm to find the kth to last element of a singly linked list.

> Do it recursively.

### Solution

Iterative solution is easy, __recursive is not__. 

### Code

	private static int myAns = -1;

	public static int nthToLastMe(LinkedListNode head, int n) {
		if (head == null) {
			return 0;
		} else if (nthToLastMe(head.next, n) < n - 1) {
			return nthToLastMe(head.next, n) + 1;
		} else if (nthToLastMe(head.next, n) == n - 1) {
			myAns = head.data;
			return Integer.MAX_VALUE;
		}
		return Integer.MAX_VALUE;
	}

---
layout: post
title: "[CC150v4] 4.7 Check Subtree"
comments: true
category: CC150v4
tags: [  ]
---

### Question

> You have two very large binary trees: T1, with millions of nodes, and T2, with hundreds of nodes. Create an algorithm to decide if T2 is a subtree of T1. 

### Solution

__The best solution is to print inorder and preorder traversal__ of both trees. Find whether the 2 traversal string of T2 __is substring of the traversal of T1__. 

This is a very good idea of checking subtree of a Binary Tree. However, this solution is very __memory intensive__. 

__The alternative solution__ simply checks the tree similarity for each and every node. 

Time complexity:

If k is the number of occurrences of T2’s root in T1, the worst case runtime can be characterized as O(n + k * m). So it's slower. 

### Code

__written by me__

	public static boolean containsTree(TreeNode t1, TreeNode t2) {
		if (t1 == null) {
			return false;
		} else if (matchTree(t1, t2)) {
			return true;
		} else {
			return containsTree(t1.left, t2) || containsTree(t1.right, t2);
		}
	}

	private static boolean matchTree(TreeNode t1, TreeNode t2) {
		if (t2 == null) {
			return true;
		} else if (t1 == null) {
			return false;
		} else if (t1.data != t2.data) {
			return false;
		} else {
			return matchTree(t1.left, t2.left) && matchTree(t1.right, t2.right);
		}
	}

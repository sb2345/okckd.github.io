---
layout: post
title: "[LeetCode Plus] Convert BST to Circular Doubly-Linked List"
comments: true
category: leetcode_plus
tags: [ src ]
---

### Question 

[link](http://leetcode.com/2010/11/convert-binary-search-tree-bst-to.html)

> Convert a BST to a sorted circular doubly-linked list in-place. 

> Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.

### Inorder solution

This question can be solved with __inorder traversal with the help of a 'pre' pointer__. 

This solution is recommended by L33tcode, but not very intuitive, and difficult to write. The C++ code is attached below. [source](http://leetcode.com/2010/11/convert-binary-search-tree-bst-to.html). 

    void treeToDoublyList(Node *p, Node *& prev, Node *& head) {
      if (!p) return;
      treeToDoublyList(p->left, prev, head);
      // current node's left points to previous node
      p->left = prev;
      if (prev)
        prev->right = p;  // previous node's right points to current node
      else
        head = p; // current node (smallest element) is head of
                  // the list if previous node is not available
      // as soon as the recursion ends, the head's left pointer 
      // points to the last node, and the last node's right pointer
      // points to the head pointer.
      Node *right = p->right;
      head->left = p;
      p->right = head;
      // updates previous node
      prev = p;
      treeToDoublyList(right, prev, head);
    }

    // Given an ordered binary tree, returns a sorted circular
    // doubly-linked list. The conversion is done in-place.
    Node* treeToDoublyList(Node *root) {
      Node *prev = NULL;
      Node *head = NULL;
      treeToDoublyList(root, prev, head);
      return head;
    }

### Divide and conquer solution

The good and intuitive solution is to do D&C and __solve left and right recursively__. Do note how the circular linked lists are merged, and be careful when replacing the pointers. 

The Java code is posted below. [source](http://cslibrary.stanford.edu/109/TreeListRecursion.html)

	public static TreeNode treeToList(TreeNode root) {
		if (root == null)
			return (null);

		// Recursively do the subtrees (leap of faith!)
		TreeNode aList = treeToList(root.left);
		TreeNode bList = treeToList(root.right);

		// Make root a circular DLL
		root.left = root;
		root.right = root;

		// At this point we have three lists, merge them
		aList = append(aList, root);
		aList = append(aList, bList);

		return (aList);
	}

	/*
	 * given two circular doubly linked lists, append them and return the new
	 * list.
	 */
	public static TreeNode append(TreeNode a, TreeNode b) {
		if (a == null)
			return (b);
		if (b == null)
			return (a);

		TreeNode aLast = a.left;
		TreeNode bLast = b.left;

		aLast.right = b;
		b.left = aLast;
		bLast.right = a;
		a.left = bLast;

		return (a);
	}

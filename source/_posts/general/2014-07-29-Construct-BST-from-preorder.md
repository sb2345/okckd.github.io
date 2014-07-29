---
layout: post
title: "[Question] Construct a BST from preorder traversal"
comments: true
category: General
tags: [  ]
---

### Question 

[link](http://www.geeksforgeeks.org/g-fact-17/)

> Given preorder, construct the BST. 

### Solution

We can get __Inorder traversal__ by sorting the given Preorder traversal. So we have the required two traversals to construct the Binary Search Tree. 

A very similar approach would be __always spliting the array__ by the head value. Time complexity is O(nlgn) for a balanced BST, or O(n^2) for a screwed tree. 

__Howver, there's [O(n) solutions](http://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)__. 

> The trick is to set a range {min .. max} for every node. Initialize the range as {INT_MIN .. INT_MAX}. The first node will definitely be in range, so create root node. To construct the left subtree, set the range as {INT_MIN …root->data}. If a values is in the range {INT_MIN .. root->data}, the values is part part of left subtree. To construct the right subtree, set the range as {root->data..max .. INT_MAX}.

There's another __[O(n) solution](http://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversal-set-2/) using stack__. 

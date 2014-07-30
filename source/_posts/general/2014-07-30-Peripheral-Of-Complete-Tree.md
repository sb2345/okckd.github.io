---
layout: post
title: "[Question] Peripheral Of A Complete Tree"
comments: true
category: General
tags: [  ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2010/09/peripheral-boundary-of-complete-tree.html)

> Write a program to find the anti-clock-wise peripheral (boundary) of a complete tree. 

> For a complete tree peripheral (boundary) is defined as

    1. First the root
    1. Then nodes on left edge
    1. Then leaf nodes
    1. Then nodes on right edge

{% img left /assets/images/peripheral-of-tree.png %}

> For the above tree, peripheral will be: 0 1 3 7 8 9 10 11 12 13 14 6 2

### Solution

__It's a very tricky solution__. Very clever I would say. 

1. print root node
1. print left nodes and leafs of left subtree in same order
1. print leafs and right nodes of right subtree in same order

### Code



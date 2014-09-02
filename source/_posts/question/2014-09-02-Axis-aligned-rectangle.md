---
layout: post
title: "[Question] Axis Aligned Rectangles "
comments: true
category: Question
tags: [  ]
---

### Question

[link](http://ankitsambyal.blogspot.sg/2013/10/finding-overlapping-rectangles-in-given.html), MIT handouts Person_A

> Describe an algorithm that takes an unsorted array of axis-aligned rectangles and returns __any pair of__ rectangles that overlaps, if there is such a pair. 

> Axis-aligned means that all the rectangle sides are either parallel or perpendicular to the x- and y-axis. 

> Each rectangle object has two variables: the x-y coordinates of the upper-left corner and the bottom-right corner.

### Analysis

A lot of different solutions on the internet, [eg](http://www.quora.com/Algorithms/Given-a-set-of-n-axis-aligned-rectangles-in-the-plane-find-how-big-is-the-largest-subset-of-these-rectangles-that-contain-a-common-point-in-O-n-3-and-then-in-order-O-nlogn) [eg](http://ankitsambyal.blogspot.sg/2013/10/finding-overlapping-rectangles-in-given.html), and some questions asks you to return all overlapping pairs. For now, we just return __any pair__ that overlaps.

### Solution 

I concluded some solution and come up with this solution (the idea of BST comes from [this pdf](http://www.cs.princeton.edu/~rs/AlgsDS07/17GeometricSearch.pdf)). 

1. sort the input. 
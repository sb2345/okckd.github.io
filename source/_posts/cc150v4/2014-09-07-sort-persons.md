---
layout: post
title: "[CC150v4] Chap9 Example - Sort Persons "
comments: true
category: CC150v4
tags: [  ]
---

### Question

> You have a very large array of ‘Person’ objects. Sort the people in increasing order of age. 

### Solution

First we look at the nature of this question: 

1. large input array
1. sort based on age (__which is between 1 and 100__, this is important)

__This exactly matches the charasteristics of Bucket Sort__. Time complexity in average case is O(n + k) where k is the number of buckets. 
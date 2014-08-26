---
layout: post
title: "[Question] Duplicate Rows in Matrix (`)"
comments: true
category: Question
tags: [ src ]
---

### Question 1

[link](http://www.careercup.com/question?id=6488077455327232)

> Given a 2D array (n x m) of integers, find all duplicate rows and print their index.

### Solution

This is a [google question](http://get-that-job-at-google.blogspot.sg/2012/12/google-interview-experience.html).

__Use HashMap__ (but make your own). Computer hash value of each row and insert into HashMap as value pair of HashMap(hashValue, rowNumber). When there's a collision, just check the rowNumber stored in HashMap with current row. 

This requires O(n*m) time and O(n) space. Note that __we're not store the entire row into HashMap__ cuz it'll take up too much space. 

We (probably) can also use Trie. 

### Question 2

[link](http://www.careercup.com/question?id=9478119)

> Given a binary matrix of N X N of integers, you need to return only unique rows of binary arrays. 

    input: 
    0 1 0 0 1 
    1 0 1 1 0 
    0 1 0 0 1 
    1 1 1 0 0 
    
    ans: 
    0 1 0 0 1 
    1 0 1 1 0 
    1 1 1 0 0

### Solution

Different from __Question 1__, this input is only 0 and 1. 

__The solution is to use Trie__. 


---
layout: post
title: "[Question] Number of distinct sub-sequence "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://stackoverflow.com/questions/5151483/how-to-find-the-number-of-distinct-subsequences-of-a-string)

> Find the number of distinct subsequences of a string (include "" as a subsequence). 

> For example, Input 

    AAA 
    ABCDEFG 
    CODECRAFT 

> Output 

    4 
    128 
    496 

### Solution

In __[LeetCode 115] Distinct Subsequences__, we discuss finding occurence of a given subsequence. 

Now if we do not specify a subsequence, __we want the total number of distinct subsequence__. 

The solution is DP, with the following equation: 

    Let, 

    dp[i] = number of distinct subsequences ending with a[i]

    last[i] = last position of character i in the given string.

Equation: 

    __dp[i] = dp[last[i] - 1] + ... + dp[i - 1]__

The final result is: 

    Distinct Subsequences = dp[1] + ... dp[len - 1]

Example 1: 

    Input   : _ A B C
    dp array: 1 1 2 4
    Total = 8

Example 2: 

    Input   : _ A A C
    dp array: 1 1 1 3
    Total = 6

The code is posted below. 

### Optimize Solution

There is a good optimization of this DP solution, which is to __keep another dp array 'sum'__, which sum[i] = dp[1] + dp[2] + ... + dp[i]. The final answer would be sum[len - 1]. 

This nice idea is from [this post](http://stackoverflow.com/a/5152203). Credit goes to __IVlad__. 

### Code



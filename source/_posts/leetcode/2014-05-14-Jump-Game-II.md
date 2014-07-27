---
layout: post
title: "[LeetCode 45] Jump Game II"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/jump-game-ii/)

<div class="question-content">
            <p></p><p>
Given an array of non-negative integers, you are initially positioned at the first index of the array.
</p>
<p>
Each element in the array represents your maximum jump length at that position. 
</p>
<p>
Your goal is to reach the last index in the minimum number of jumps.
</p>

<p>
For example:<br>
Given array A = <code>[2,3,1,1,4]</code>
</p>
<p>
The minimum number of jumps to reach the last index is <code>2</code>. (Jump <code>1</code> step from index 0 to 1, then <code>3</code> steps to the last index.)
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a DP problem__. 

__This question looks eays, but__ after I write the code fast, I got "time limit exceed" for many times, until I found out a way to deal with the "cur" pointer more efficiently. 

### Solution

A analysis from [this blog](http://eric-yuan.me/leetcode-jump-game-ii/) explains it very well: 

> Search forward, and see for each node of array, what is the current maximum place we can reach, and every time we reach a local maximum, we add counter by 1, if we can reach the terminal, just return the counter.

### My code 

My code. This DP solution is the popular online solution.


    public int jump(int[] A) {
        int len = A.length;
        if (len <= 1) return 0;
        int[] dp = new int[len];
        if (A[0] == 0) return 0;
        int cur = 1;
        for (int i = 0; i < len; i ++) {
            if (i != 0 && dp[i] == 0) return 0;
            // array dp represent the steps to reach point i
            for (; cur < len && cur <= i + A[i]; cur ++) {
                dp[cur] = dp[i] + 1;
            }
            if (dp[len - 1] != 0) return dp[len - 1];
        }
        return 0;
    }

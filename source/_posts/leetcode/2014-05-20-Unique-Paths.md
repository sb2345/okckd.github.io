---
layout: post
title: "[LeetCode 62] Unique Paths"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/unique-paths/)

<div class="question-content">
            <p></p><p>A robot is located at the top-left corner of a <i>m</i> x <i>n</i> grid (marked 'Start' in the diagram below).</p>

<p>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).</p>

<p>How many possible unique paths are there?</p>

<p>
<img src="http://4.bp.blogspot.com/_UElib2WLeDE/TNJf8VtC2VI/AAAAAAAACXU/UyUa-9LKp4E/s400/robot_maze.png"><br>
</p><p style="font-size: 11px">Above is a 3 x 7 grid. How many possible unique paths are there?
</p>

<p><b>Note:</b> <i>m</i> and <i>n</i> will be at most 100.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an easy question__.

__My first idea is not the most classic solution, but the best solution I know of so far__. Basically to walk from (0,0) to (m,n), robot have to walk down (m-1) steps and rightward (n-1) steps. Then this problem simply becomes [Number of k-combinations](http://en.wikipedia.org/wiki/Combination#Number_of_k-combinations) (also known as choose m from n problem). The code is just concise and short. 

__My second solution is a DP solution__ making use of a 1-D array. This is very similar to the question "Minimum Path Sum". 

### Solution

The code is easy to read. 

### My code

__Number of k-combinations solution__


    public int uniquePaths(int m, int n) {
        if (m == 1 || n == 1) return 1;
        long sum = 1L;
        int a = Math.min(m - 1, n - 1);
        int b = Math.max(m - 1, n - 1);
        for (int i = 0; i < a; i ++) 
            sum = sum * (a + b - i);
        for (int i = 0; i < a; i ++) 
            sum = sum / (a - i);
        return (int)sum;
    }


__DP solution__


    public int uniquePaths(int m, int n) {
        if (m <= 0 || n <= 0) return 0;
        if (m == 1 || n == 1) return 1;
        int[] dp = new int[n];
        for (int i = 0; i < m; i ++) 
            for (int j = 0; j < n; j ++)
                if (i == 0 || j == 0) dp[j] = 1;
                else dp[j] += dp[j-1];
        return dp[n-1];
    }


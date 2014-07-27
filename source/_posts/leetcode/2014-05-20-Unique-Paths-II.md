---
layout: post
title: "[LeetCode 63] Unique Paths II"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/unique-paths-ii/)

<div class="question-content">
            <p></p><p>Follow up for "Unique Paths":</p>

<p>Now consider if some obstacles are added to the grids. How many unique paths would there be?</p>

<p>An obstacle and empty space is marked as <code>1</code> and <code>0</code> respectively in the grid.</p>

<p>For example,<br>
</p><p>There is one obstacle in the middle of a 3x3 grid as illustrated below.</p>
<pre>[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
</pre>
<p>The total number of unique paths is <code>2</code>.</p>

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
		<td bgcolor="yellow">3</td>
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

__This is same question as previous one, DP solution__. 

### Solution

The code need no explanation. 

### My code


    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        dp[0][0] = 1 - obstacleGrid[0][0];
        for (int i = 1; i < m + n - 1; i ++) {
            for (int j = 0; j <= i; j ++) {
                // dp[j][i-j] within the range of dp[m][n]
                if (j >= m || i-j >= n) continue;
                if (obstacleGrid[j][i-j] == 1){ 
                    dp[j][i-j] = 0;
                    continue;
                }
                if (j - 1 >= 0) dp[j][i-j] += dp[j-1][i-j];
                if (i-j-1 >= 0) dp[j][i-j] += dp[j][i-j-1];
            }
        }
        return dp[m-1][n-1];
    }

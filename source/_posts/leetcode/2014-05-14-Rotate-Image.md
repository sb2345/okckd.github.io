---
layout: post
title: "[LeetCode 48] Rotate Image"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/rotate-image/)

<div class="question-content">
            <p></p><p>You are given an <i>n</i> x <i>n</i> 2D matrix representing an image.</p>
<p>Rotate the image by 90 degrees (clockwise).</p>
<p>Follow up:<br>
Could you do this in-place?</p><p></p>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is easy, just swap numbers in place. 

### Solution

Code is easy.

### My code 

My solution


    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int a = 0; a <= n / 2 - 1; a ++) {
            for (int b = 0; b <= (n - 1) / 2; b ++){
                int temp = matrix[a][b];
                matrix[a][b] = matrix[n-1-b][a];
                matrix[n-1-b][a] = matrix[n-1-a][n-1-b];
                matrix[n-1-a][n-1-b] = matrix[b][n-1-a];
                matrix[b][n-1-a] = temp;
            }
        }
    }


A cleaner version from [this blog](http://blog.csdn.net/kenden23/article/details/17200067). 

This code is very concise and beautiful, but actually it just __added 2 more variables__ compared to my solution. 

> x = n-1-a

> y = n-1-b


    public void rotate(int[][] matrix) {
        for (int a = 0, x = matrix.length - 1; a < x; a++, x--) {
            for (int b = a, y = x; b < x; b++, y--) {
                int t = matrix[a][b];
                matrix[a][b] = matrix[y][a];
                matrix[y][a] = matrix[x][y];
                matrix[x][y] = matrix[b][x];
                matrix[b][x] = t;
            }
        }
    }

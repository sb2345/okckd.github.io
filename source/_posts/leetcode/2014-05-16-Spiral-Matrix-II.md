---
layout: post
title: "[LeetCode 59] Spiral Matrix II "
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/spiral-matrix-ii/)

<div class="question-content">
            <p></p><p>Given an integer <i>n</i>, generate a square matrix filled with elements from 1 to <i>n</i><sup>2</sup> in spiral order.</p>

<p>
For example,<br>
Given <i>n</i> = <code>3</code>,
</p>
You should return the following matrix:
<pre>[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
</pre><p></p>
          </div>
### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
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

__This question is basic mathematics__. There is another similar question __Spiral Matrix__. 

The difficult part is writing the code. 

### Solution

Code is easy to read. 

### My code

__My code, this is pure math__.

    public int[][] generateMatrix(int n) {
        int[][] ans = new int[n][n];
        int num = 1;
        for (int i = 0; i < n / 2; i ++) {
            for (int k = i; k <= n-2-i; k ++) ans[i][k] = num ++;
            for (int l = i; l <= n-2-i; l ++) ans[l][n-i-1] = num ++;
            for (int p = n-i-1; p >=i+1 ; p --) ans[n-i-1][p] = num ++;
            for (int q = n-i-1; q >=i+1 ; q --) ans[q][i] = num ++;
        }
        if (n % 2 == 1) ans[n/2][n/2] = num;
        return ans;
    }

__Updated on Oct 9th, 2014__, a better piece of code:

    public int[][] generateMatrix(int n) {
        int small = 0;
		int large = n - 1;
		int num = 1;
		
		int[][] ans = new int[n][n];
		while (small < large) {
			for (int i = small; i < large; i++) {
				ans[small][i] = num++;
			}
			for (int i = small; i < large; i++) {
				ans[i][large] = num++;
			}
			for (int i = large; i > small; i--) {
				ans[large][i] = num++;
			}
			for (int i = large; i > small; i--) {
				ans[i][small] = num++;
			}
			small++;
			large--;
		}
		if (small == large) {
			ans[small][small] = num;
		}
		return ans;
    }

---
layout: post
title: "[LeetCode 52] N-Queens II"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/n-queens-ii/)

<div class="question-content">
            <p></p><p>Follow up for N-Queens problem.</p>

<p>Now, instead outputting board configurations, return the total number of distinct solutions.</p>

<p><img src="http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png"></p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

I posted 2 solution by me. Second code is same as [this guy's code](https://github.com/rffffffff007/leetcode/blob/master/N-Queens%20II.java).

### My code

__Using global variable__

    int ans = 0;

    public int totalNQueens(int n) {
        solve(0, n, new int[n]);
        return ans;
    }

    private void solve(int cur, int n, int[] list) {
        if (cur == n) {
            ans ++;
            return;
        }
        for (int i = 0; i < n; i++) {
            // put a queen at position (cur, i), and check conflict
            boolean conflict = false;
            for (int j = 0; j < cur; j++)
                // check (cur, i) against (j, list[j])
                if (i == list[j] || cur - j == Math.abs(i - list[j]))
                    conflict = true;
            if (conflict) continue;
            list[cur] = i;
            solve(cur + 1, n, list);
        }
    }

__Without using global variable__

    public int totalNQueens(int n) {
        return solve(0, n, new int[n]);
    }

    private int solve(int cur, int n, int[] list) {
        if (cur == n) return 1;
        int ans = 0;
        for (int i = 0; i < n; i++) {
            boolean conflict = false;
            for (int j = 0; j < cur; j++)
                if (i == list[j] || cur - j == Math.abs(i - list[j]))
                    conflict = true;
            if (conflict) continue;
            list[cur] = i;
            ans += solve(cur + 1, n, list);
        }
        return ans;
    }

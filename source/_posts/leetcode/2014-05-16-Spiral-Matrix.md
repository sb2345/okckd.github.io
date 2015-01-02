---
layout: post
title: "[LeetCode 54] Spiral Matrix"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/spiral-matrix/)

<div class="question-content">
            <p></p><p>Given a matrix of <i>m</i> x <i>n</i> elements (<i>m</i> rows, <i>n</i> columns), return all elements of the matrix in spiral order.
</p>

<p>
For example,<br>
Given the following matrix:
</p>
<pre>[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
</pre>
<p>
You should return <code>[1,2,3,6,9,8,7,4,5]</code>.
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
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is basic mathematics__. There is another similar question __Spiral Matrix__. 

The difficult part is writing the code. 

### My code

    public ArrayList<Integer> spiralOrder(int[][] matrix) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        if (matrix.length == 0 || matrix[0].length == 0) ;
        else solve(ans, matrix, 0, matrix.length, matrix[0].length);
        return ans;
    }

    private void solve(ArrayList<Integer> ans, int[][] matrix, int cur, int m,
            int n) {
        if (cur >= m / 2) {
            // Take m=4, n=100, cur=2, no fill required
            // Take m=5, n=100, cur=2, fill in from (2,2) to (2,97) inclusive
            // which is (cur,cur) to (cur,n-cur-1)
            if (m % 2 == 0) return;
            for (int i = cur; i < n - cur; i++)
                ans.add(matrix[cur][i]);
        } else if (cur >= n / 2) {
            if (n % 2 == 0) return;
            for (int i = cur; i < m - cur; i++)
                ans.add(matrix[i][cur]);
        } else {
            for (int k = cur; k <= n - 2 - cur; k++)
                ans.add(matrix[cur][k]);
            for (int l = cur; l <= m - 2 - cur; l++)
                ans.add(matrix[l][n - cur - 1]);
            for (int p = n - cur - 1; p >= cur + 1; p--)
                ans.add(matrix[m - cur - 1][p]);
            for (int q = m - cur - 1; q >= cur + 1; q--)
                ans.add(matrix[q][cur]);
            solve(ans, matrix, cur + 1, m, n);
        }
    }

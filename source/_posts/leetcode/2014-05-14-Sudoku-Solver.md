---
layout: post
title: "[LeetCode 37] Sudoku Solver"
comments: true
category: Leetcode
tags: [  ]
---

### Question 
[link](http://oj.leetcode.com/problems/sudoku-solver/)

<div class="question-content">
            <p></p><p>Write a program to solve a Sudoku puzzle by filling the empty cells.</p>

<p>Empty cells are indicated by the character <code>'.'</code>.</p>

<p>You may assume that there will be only one unique solution.

</p><p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png"><br>
</p><p style="font-size: 11px">A sudoku puzzle...</p>
<p></p>

<p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png"><br>
</p><p style="font-size: 11px">...and its solution numbers marked in red.
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
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">Difficult</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very classic DFS search problem__, and it is not easy! 

### Solution

__The solution simply brute force DFS__. 

### My code 

The following solution is from [this blog](http://xixiaogualu.blogspot.sg/2013/09/leetcode-sudoku-solver.html)

    public void solveSudoku(char[][] board) {
        helper(board, 0, 0);
    }

    private boolean helper(char[][] board, int i, int j) {
        if (j >= 9)	return helper(board, i + 1, 0);
        if (i == 9) return true;
        if (board[i][j] == '.') {
            for (int k = 1; k <= 9; k++) {
                board[i][j] = (char) (k + '0');
                if (isValid(board, i, j)) 
                    if (helper(board, i, j + 1))
                        return true;
                board[i][j] = '.';
            }
        } else return helper(board, i, j + 1);
        return false;
    }

    private boolean isValid(char[][] board, int i, int j) {
        boolean[] map = new boolean[9];
        for (int k = 0; k < 9; k++) 
            if (k != j && board[i][k] == board[i][j])
                return false;
        for (int k = 0; k < 9; k++) 
            if (k != i && board[k][j] == board[i][j])
                return false;
        for (int row = i / 3 * 3; row < i / 3 * 3 + 3; row++) 
            for (int col = j / 3 * 3; col < j / 3 * 3 + 3; col++) 
                if ((row != i || col != j) && board[row][col] == board[i][j])
                    return false;
        return true;
    }

__Updated on July 7th__, code:

    public void solveSudoku(char[][] board) {
        helper(board, 0, 0);
    }
    
    private boolean helper(char[][] b, int m, int n) {
        if (n == 9) {
            m += 1;
            n = 0;
        }
        if (m == 9) {
            return true;
        }
        if (b[m][n] != '.') {
            return helper(b, m, n + 1);
        }
        for (int i = 1; i <= 9; i++) {
            b[m][n] = (char) ('0' + i);
            if (!validate(b, m, n)) {
                continue;
            }
            if (helper(b, m, n + 1)) {
                return true;
            }
        }
        b[m][n] = '.';
        return false;
    }
    
    private boolean validate(char[][] board, int i, int j) {
        for (int k = 0; k < 9; k++) 
            if (k != j && board[i][k] == board[i][j])
                return false;
        for (int k = 0; k < 9; k++) 
            if (k != i && board[k][j] == board[i][j])
                return false;
        for (int row = i / 3 * 3; row < i / 3 * 3 + 3; row++) 
            for (int col = j / 3 * 3; col < j / 3 * 3 + 3; col++) 
                if ((row != i || col != j) && board[row][col] == board[i][j])
                    return false;
        return true;
    }

---
layout: post
title: "[LeetCode 36] Valid Sudoku"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/valid-sudoku/)

<div class="question-content">
            <p></p><p>Determine if a Sudoku is valid, according to: <a href="http://sudoku.com.au/TheRules.aspx">Sudoku Puzzles - The Rules</a>.</p>

<p>The Sudoku board could be partially filled, where empty cells are filled with the character <code>'.'</code>.</p>

<p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png"><br>
</p><p style="font-size: 11px">A partially filled sudoku which is valid.</p>
<p></p>

<p><b>Note:</b><br>
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.
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

__This is not a difficult problem__. 

Most online solutions are same as mine, which make use of __three for-loops__ and __nine arrays of length 9__ (for each loop) to mark the status. 

However, __I also found a tricky solution__. See code for details. 

### Solution

Both code are straight-forward. 

### My code 

Below is my code.


    public boolean isValidSudoku(char[][] board) {
        // first, validate rows
        for (int i = 0; i < 9; i ++) {
            int[] mark = new int[9];
            for(char a: board[i]) 
                if (a != '.') mark[a-'1'] ++;
            for (int b: mark) if (b > 1) return false;
        }
        // second, validate columns
        for (int i = 0; i < 9; i ++) {
            int[] mark = new int[9];
            for(char[] a: board) 
                if (a[i] != '.') mark[a[i]-'1'] ++;
            for (int b: mark) if (b > 1) return false;
        }
        // third, validate box
        for (int a = 0; a <= 6; a += 3) {
            for (int b = 0; b <= 6; b += 3) {
                int[] mark = new int[9];
                for (int i = 0; i <= 2; i ++) 
                    for (int j = 0; j <= 2; j ++) 
                        // the 9 values are represented at (a+i, b+j)
                        if (board[a+i][b+j] != '.') mark[board[a+i][b+j]-'1'] ++;
                for (int c: mark) if (c > 1) return false;
            }
        }
        // finished validation. if still survives at this point of time, congratulations!
        return true;
    }


__The following solution__ is from [this blog](http://www.cnblogs.com/zhaolizhen/p/Sudoku.html). It's a very clever and tricky solution! 

__Note that default value of Java boolean type is false__, so no need to set value after declaration. 


    public boolean isValidSudoku(char[][] board) {
        boolean[][] rows = new boolean[9][9];
        boolean[][] cols = new boolean[9][9];
        boolean[][] blocks = new boolean[9][9];
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                int c = board[i][j] - '1';
                if (board[i][j] == '.') continue;
                if (rows[i][c] || cols[j][c] || blocks[i - i % 3 + j / 3][c])
                    return false;
                rows[i][c] = cols[j][c] = blocks[i - i % 3 + j / 3][c] = true;
            }
        }
        return true;
    }

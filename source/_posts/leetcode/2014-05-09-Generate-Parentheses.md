---
layout: post
title: "[LeetCode 22] Generate Parentheses"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/valid-parentheses/)

<div class="question-content">
            <p></p><p>
Given <i>n</i> pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
</p>

<p>
For example, given <i>n</i> = 3, a solution set is:
</p>
<p>
<code>"((()))", "(()())", "(())()", "()(())", "()()()"</code>
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
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

__Most popular solutions online are using recursive calls__. For example, [this blog](http://www.geeksforgeeks.org/print-all-combinations-of-balanced-parentheses/). I also used this method. 

### Solution

I kept 2 integers: __open__ (number of unclosed left parenthesis) and __remain__ (number of parenthesis that can be addded to the current string). I optimized my previous code and made it cleaner. 

### My code 


    public ArrayList<String> generateParenthesis(int n) {
            return helper(new ArrayList<String>(), 0, n, "");
    }

    private ArrayList<String> helper(ArrayList<String> ans, 
                    int open, int remain, String cur) {
            if (open == 0 && remain == 0) ans.add(cur);
            if (remain > 0) helper(ans, open + 1, remain - 1, cur + "(");
            if (open > 0) helper(ans, open - 1, remain, cur + ")");
            return ans;
    }


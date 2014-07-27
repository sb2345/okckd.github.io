---
layout: post
title: "[LeetCode 20] Valid Parentheses"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/valid-parentheses/)

<div class="question-content">
            <p></p><p>Given a string containing just the characters <code>'('</code>, <code>')'</code>, <code>'{'</code>, <code>'}'</code>, <code>'['</code> and <code>']'</code>, determine if the input string is valid.</p>

<p>The brackets must close in the correct order, <code>"()"</code> and <code>"()[]{}"</code> are all valid but <code>"(]"</code> and <code>"([)]"</code> are not.</p>
<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
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

__Standard solution around the internet is to use stack__. 

I though using String is also fine, so I tried it. I also works. 

### Solution

The code is easy. 

### My code 


    public boolean isValid(String s) {
            String p = "";
            for (int i = 0; i < s.length(); i ++) {
                char cur = s.charAt(i);
                if (cur == '(' || cur == '{' || cur == '[') {
                    p += cur;
                } else {
                    if (p.length() == 0) return false;
                    if (p.charAt(p.length()-1) - cur <= 2)
                        p = p.substring(0, p.length()-1);
                }
            }
            if (p.length() == 0) return true;
            return false;
    }


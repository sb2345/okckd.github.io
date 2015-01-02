---
layout: post
title: "[LeetCode 58] Length of Last Word"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/length-of-last-word/)

<div class="question-content">
            <p></p><p>Given a string <i>s</i> consists of upper/lower-case alphabets and empty space characters <code>' '</code>, return the length of last word in the string.</p>

<p>If the last word does not exist, return 0.</p>

<p><b>Note:</b> A word is defined as a character sequence consists of non-space characters only.</p>

<p>
For example, <br>
Given <i>s</i> = <code>"Hello World"</code>,<br>
return <code>5</code>.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

This is a easy question.

### My code


    public int lengthOfLastWord(String s) {
        s = s.trim();
        int l = s.length() - 1;
        while (l >= 0) 
            if (s.charAt(l--) == ' ') return s.length() - l - 2;
        return s.length();
    }


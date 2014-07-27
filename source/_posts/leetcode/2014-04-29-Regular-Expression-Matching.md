---
layout: post
title: "[LeetCode 10] Regular Expression Matching"
comments: true
category: Leetcode
tags: [  ]
---

### Question 
[link](http://oj.leetcode.com/problems/regular-expression-matching/)

<div class="question-content">
<p></p><p>Implement regular expression matching with support for <code>'.'</code> and <code>'*'</code>.</p>

<pre>'.' Matches any single character.
'*' Matches <b>zero or more of the preceding</b> element.

The matching should cover the <b>entire</b> input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
</pre><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">a very long time</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__There are only 2 cases to consider__. One, the next char is not a star sign, this requires simply char compare. __Two, the next char is a star sign__, this will requires a bit brute force. The program will enumerate all possible number of repetition of current char, and check validation one by one.

The code is very complex and, though I tried, I failed to implement the solution. 

Although looks like DP, __Do not solve it with DP, because there is no one doing that__. 

### My code 

This is [someone's code](http://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/), which I refactored a bit to make it easier to understand. 

	public boolean isMatch(String s, String p) {
		// s is normal string, and p is regex string
		if (p.length() == 0) {
			return s.length() == 0;
		} else if (p.length() < 2 || p.charAt(1) != '*') {
			// if 2nd char in p is not '*', then match character
			if (s.length() == 0) {
				return false;
			} else if (p.charAt(0) != '.' && s.charAt(0) != p.charAt(0)) {
				return false;
			} else {
				return isMatch(s.substring(1), p.substring(1));
			}
		} else {
			// if 2nd char in p is '*', then iterate all position repetitions
			char repeatLetter = p.charAt(0);
			for (int i = 0; i <= s.length(); i++) {
				// i is the number of repetition of repeatLetter, start from 0
				if (i > 0 && repeatLetter != s.charAt(i - 1) 
							&& repeatLetter != '.') {
					break;
				} else {
					if (isMatch(s.substring(i), p.substring(2))) {
						return true;
					}
				}
			}
			return false;
		}
	}

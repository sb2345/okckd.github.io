---
layout: post
title: "[Question] Longest Common Substring "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.geeksforgeeks.org/longest-common-substring/)

> Given two strings ‘X’ and ‘Y’, find the length of the longest common substring. 

> For example, if the given strings are “GeeksforGeeks” and “GeeksQuiz”, the output should be 5 as longest common substring is “Geeks”. 

### Solution

This question is to be distinguished from __[LintCode] Longest Common Subsequence__. 

The solution is DP, too. Even the code is similar. Read my code below. 

### Code

	public String LCSubstr(String s, String t) {
		int longest = 0;
		int tPos = -1;

		// dp[i][j] represents the LCSubstr ending at position i and j
		int[][] dp = new int[t.length() + 1][s.length() + 1];
		for (int i = 1; i <= t.length(); i++) {
			for (int j = 1; j <= s.length(); j++) {
				if (t.charAt(i - 1) == s.charAt(j - 1)) {
					dp[i][j] = dp[i - 1][j - 1] + 1;
					if (dp[i][j] > longest) {
						longest = dp[i][j];
						tPos = i;
					}
				}
			}
		}
		return t.substring(tPos - longest, tPos);
	}

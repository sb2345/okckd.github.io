---
layout: post
title: "[Question] Longest Common Contiguous Intersection (Longest common substring) "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.careercup.com/question?id=12862670)

> Write Program to find longest common contiguous intersection from 2 lists provided to the function. 

> Example: list1: abcrfghwetf 
>
> list2: abrfghwwetxyab 

> Ans: rfghw

### Solution

This is a classic [Longest common substring](http://en.wikipedia.org/wiki/Longest_common_substring_problem) problem.

Solution 1: __Suffix tree__. Building the tree is O(n) time and the whole program is O(n + m) time. 

Solution 2: __DP__, which takes O(nm) time and space. The code for DP is posted below. 

### Code

__dp__

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

---
layout: post
title: "[LeetCode 5] Longest Palindromic Substring"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/longest-palindromic-substring/)

<div class="question-content">
<p></p><p>Given a string <i>S</i>, find the longest palindromic substring in <i>S</i>. You may assume that the maximum length of <i>S</i> is 1000, and there exists one unique longest palindromic substring.</p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">20 min coding only</td>
	</tr>
</table>

### Analysis

There are 2 solutions for this question. One is __DP__ and another is __direct method__. Both is __O(n^2) time complexity__. However, DP requires __O(n^2) space__, while the direct method requires __constant space__ and a intelligent brain. 

### Solution

I will not cover [DP solution](http://leetcode.com/2011/11/longest-palindromic-substring-part-i.html) in this post because it's not simple, and it's a bit hard to implement in code, __especially the last nested for loop is quite difficult to think__. The DP solution and code can be a future task. 

__Direct solution__ is basically iterate through the entire string, and assume each char (or pair of char) as center of the palindrome. The code explains itself very well. 

### My code 

    public String longestPalindrome(String s) {
        if (s.length() <= 1)
            return s;
        String largest = s.substring(0, 1);
        for (int i = 0; i < s.length(); i++) {
            String first = this.searchAroundCenter(s, i, i);
            String second = this.searchAroundCenter(s, i, i + 1);
            if (first.length() < second.length())
                first = second;
            if (largest.length() < first.length())
                largest = first;
        }
        return largest;
    }

    private String searchAroundCenter(String s, int a, int b) {
        if (a < 0 || b > s.length() - 1)
            return "";
        while (s.charAt(a) == s.charAt(b)) {
            a--;
            b++;
            if (a < 0 || b > s.length() - 1)
                return s.substring(a + 1, b);
        }
        return s.substring(a + 1, b);
    }


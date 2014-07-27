---
layout: post
title: "[LeetCode 14] Longest Common Prefix"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/longest-common-prefix/)

<div class="question-content">
            <p></p><p>Write a function to find the longest common prefix string amongst an array of strings.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="white">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">10 minutes</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question have straight-forward solution.__ Every online solution is the same as my method, however, there's another more generalized [__LCP array__](http://en.wikipedia.org/wiki/LCP_array) which is solved by use of [Trie](http://en.wikipedia.org/wiki/Trie). I'm not interested in this topic right now.

### Solution

The code explains itself. 

### My code 

My original solution.


    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0)
            return "";
        int shortest = strs[0].length();
        for (String a : strs)
            shortest = Math.min(shortest, a.length());
        for (int i = 0; i < shortest; i++) {
            for (int j = 1; j < strs.length; j++) {
                // check strs[j].charAt(i)
                if (strs[j].charAt(i) != strs[j - 1].charAt(i)) {
                    return strs[0].substring(0, i);
                }
            }
        }
        return strs[0].substring(0, shortest);
    }


__Refactored code__. I do not really need 'shortest'. Increase execution time from 468ms to 456 ms.

This is the shortest code for this question, for my best knowledge :)


    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";
        for (int i = 0; i < strs[0].length(); i++)
            for (int j = 1; j < strs.length; j++)
                if (strs[j].length() == i
                        || strs[j].charAt(i) != strs[0].charAt(i))
                    return strs[0].substring(0, i);
        return strs[0];
    }


---
layout: post
title: "[LeetCode 3] Longest Substring Without Repeating Characters"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/longest-substring-without-repeating-characters/)

<div class="question-content">
<p></p><p>Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.</p>
<p></p></div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow"> > 1 hour</td>
	</tr>
</table>

### Analysis

This question looks easy, but it took me a while to figure out the algorithm. Small details of the implementation are easily omitted. **This definitely is a tough question**, and I spend half of the time with algorithm and another half trying to debug. 

The basic idea is to read char by char for just 1 iteration. In the meanwhile, an array of pointers are stored to keep track of the last occurance position of each char. Thus it's going to be something like __array = int\\\[256\\\]__, and we set value in this way __array\\\[char\\\] = 1__.

### Solution

As explain, read char by char and keep an array of size 256. 

__The tricky part is when a repeating char is found__. A pointer is kept to record this position 'k' (which is the last position where repeat happens). Later whenever a repeat happens before k, it shall be ignored. This is one mistake that might happen during coding.

{% img left /assets/images/20130901224716625.png %}

### My code 

    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0)
            return 0;
        int[] pos = new int[255];
        for (int j = 0; j < pos.length; j++) {
            pos[j] = -1;
        }
        int start = 0, max = 0;
        char[] ss = s.toCharArray();
        for (int i = 0; i < ss.length; i++) {
            char cur = ss[i];
            if (pos[cur] == -1 || pos[cur] < start) {
                pos[cur] = i;
            } else {
                max = Math.max(max, i - start);
                start = pos[cur] + 1;
                pos[cur] = i;
            }
        }
        return Math.max(max, ss.length - start);
    }


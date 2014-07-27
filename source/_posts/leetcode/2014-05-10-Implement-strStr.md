---
layout: post
title: "[LeetCode 28] Implement strStr"
comments: true
category: Leetcode
tags: [  ]
---

### Question 
[link](http://oj.leetcode.com/problems/implement-strstr/)

<div class="question-content">
            <p></p><p>
Implement strStr().
</p>
<p>
Returns a pointer to the first occurrence of needle in haystack, or <b>null</b> if needle is not part of haystack.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
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
		<td bgcolor="yellow">KMP is difficult</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are 2 ways to solve this problem. __The most easy and common way__ is to use nested loop (many online solutions use this method). 

However, __this question can also be solved by [KPM algorithm](http://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)__. 

### Solution

I post my standard solution below. This is the most standard solution online, for example it is in [this post](http://goo.gl/2MNOS2).

__I have yet to written KPM solution__. [This blog](http://discuss.leetcode.com/questions/76/implement-strstr) and [this blog](http://fisherlei.blogspot.sg/2012/12/leetcode-implement-strstr.html) have good KMP solution posted. 

### My code 

__Simple solution__

    public String strStr(String haystack, String needle) {
            if (needle.length() == 0) return haystack;
            for (int i = 0; i <= haystack.length() - needle.length(); i ++) {
                    if (haystack.charAt(i) != needle.charAt(0)) continue;
                    int j = 0;
                    for (; j < needle.length(); j ++) {
                            if (haystack.charAt(i + j) != needle.charAt(j)) break;
                    }
                    if (j == needle.length()) return haystack.substring(i);
            }
            return null;
    }

__KPM solution__

Only need to understand to principles. 

---
layout: post
title: "[LeetCode 140] Word Break II"
comments: true
category: Leetcode
tags: [  ]
---

### Question 
[link](https://oj.leetcode.com/problems/word-break-ii/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given a string <i>s</i> and a dictionary of words <i>dict</i>, add spaces in <i>s</i> to construct a sentence where each word is a valid dictionary word.
</p>

<p class="font-color">
Return all such possible sentences.
</p>

<p class="font-color">
For example, given<br>
<i>s</i> = <code>"catsanddog"</code>,<br>
<i>dict</i> = <code>["cat", "cats", "and", "sand", "dog"]</code>.
</p>

<p class="font-color">
A solution is <code>["cats and dog", "cat sand dog"]</code>.
</p>
<p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a tough question__. Standard DFS search would work, but we need to check 'breakable' first. Otherwise, I got TLE. 

__Check breakable is a easy DP__, and we do not need to remove any elements from the dictionary. (Word ladder needs remove elements from dictionary, don't confuse them). 

### Solution

__Updated on July 4th, 2014__. The DFS code actually standard, but keep in mind to check breakable first (using DP). 

### Code

__DFS with pruning and DP breakable check__

    public List<String> wordBreak(String s, Set<String> dict) {
        List<String> ans = new LinkedList<String>();
        if (s == null || s.length() == 0) {
            return null;
        }
        if (!canBreak(s, dict)) {
            return ans;
        }
        int maxLength = getMaxLength(dict);
        helper(ans, "", s, dict, 0, maxLength);
        return ans;
    }
    
    private void helper(List<String> ans, String path, String s, Set<String> dict, int pos, int maxLength) {
        if (pos == s.length()) {
            ans.add(path);
            return;
        }
        for (int i = pos + 1; i <= s.length() && i <= pos + maxLength; i++) {
            String temp = s.substring(pos, i);
            if (!dict.contains(temp)) {
                continue;
            }
            String newPath = null;
            if (path.length() == 0) {
                newPath = temp;
            } else {
                newPath = path + " " + temp;
            }
            helper(ans, newPath, s, dict, i, maxLength);
        }
    }
	
    private int getMaxLength(Set<String> dict) {
        int maxLength = 0;
        for (String word : dict) {
            maxLength = Math.max(maxLength, word.length());
        }
        return maxLength;
    }
    
    public boolean canBreak(String s, Set<String> dict) {
        if (s == null || s.length() == 0) {
            return true;
        }
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        dp[0] = true;
        for (int i = 1; i <= len; i++) {
            for (int j = 0; j < i; j++) {
                if (!dp[j]) {
                    continue;
                }
                if (dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }

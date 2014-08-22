---
layout: post
title: "[LeetCode 44] Wildcard Matching"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/wildcard-matching/)

<div class="question-content">
            <p></p><p>Implement wildcard pattern matching with support for <code>'?'</code> and <code>'*'</code>.</p>

<pre>'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the <b>entire</b> input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
</pre><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">did not solve</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is similar to "Regex Matching", and in fact can be solved using similar (DFS recursion) approach. [This blog](http://n00tc0d3r.blogspot.sg/2013/05/wildcard-matching.html) has the best coverage of analysis and solutions overall.

__The solution is DP__. The equation is not very difficult to write, but keep in mind to __check character count before entering the algorithm__. Failing to do so results in TLE! 

### My code 

__Updated on July 8th__, my DP solution. 1200 ms. 

    public boolean isMatch(String s, String p) {
        int len1 = s.length();
        int len2 = p.length();
        
        int count = 0;
        for (int i = 0; i < p.length(); i++) {
            if (p.charAt(i)!='*')
                count++;
        }
        if(count > s.length()) {
            return false;  
        }
        
        boolean[][] dp = new boolean[len2 + 1][len1 + 1];
        for (int i = 0; i <= len2; i++) {
            for (int j = 0; j <= len1; j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = true;
                } else if (i == 0) {
                    dp[i][j] = false;
                } else if (j == 0) {
                    if (p.charAt(i - 1) == '*') {
                        dp[i][j] = dp[i - 1][j];
                    } else {
                        dp[i][j] = false;
                    }
                } else {
                    if (p.charAt(i - 1) == '*') {
                        for (int k = j; k >= 0; k--) {
                            if(dp[i - 1][k]) {
                                dp[i][j] = true;
                                break;
                            }
                        }
                    } else if (p.charAt(i - 1) == '?') {
                        dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        dp[i][j] = dp[i - 1][j - 1] 
                            & p.charAt(i - 1) == s.charAt(j - 1);
                    }
                }
            }
        }
        return dp[len2][len1];
    }

__Updated on July 23th__, optimized DP solution. 700 ms. 

	public boolean isMatch(String s, String p) {
		int len1 = s.length();
		int len2 = p.length();
		
        int count = 0;
        for (int i = 0; i < p.length(); i++) {
            if (p.charAt(i)!='*')
                count++;
        }
        if(count > s.length()) {
            return false;  
        }

		boolean[][] dp = new boolean[len1 + 1][len2 + 1];
		for (int j = 0; j <= len2; j++) {
		    for (int i = 0; i <= len1; i++) {
				if (i == 0 && j == 0) {
					dp[i][j] = true;
				} else if (j == 0) {
					dp[i][j] = false;
				} else if (i == 0) {
				    dp[i][j] = p.charAt(j - 1) == '*' && dp[i][j - 1];
				}else {
					char wildCardChar = p.charAt(j - 1);
					if (wildCardChar == '*') {
						// find the first match between dp[0][j-1] and dp[len1][j-1]
						int q = 0;
						while (q <= len1 && !dp[q][j-1]) {
						    q++;
						}
						while (q <= len1) {
						    dp[q][j] = true;
						    q++;
						}
						break;
					} else if (wildCardChar == '?') {
						dp[i][j] = dp[i - 1][j - 1];
					} else {
						dp[i][j] = s.charAt(i - 1) == p.charAt(j - 1)
								&& dp[i - 1][j - 1];
					}
				}
			}
		}
		return dp[len1][len2];
	}

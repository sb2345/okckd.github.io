---
layout: post
title: "[LeetCode 6] ZigZag Conversion"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/zigzag-conversion/)

<div class="question-content">
<p></p><p>
The string <code>"PAYPALISHIRING"</code> is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
</p><pre>
P   A   H   N
A P L S I I G
Y   I   R
</pre>

And then read line by line: <code>"PAHNAPLSIIGYIR"</code><p></p>

<p>
Write the code that will take a string and make this conversion given a number of rows:

</p><pre>string convert(string text, int nRows);</pre>

<code>convert("PAYPALISHIRING", 3)</code> should return <code>"PAHNAPLSIIGYIR"</code>.
<p></p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">45 minutes</td>
	</tr>
</table>

### Analysis

__This question is easy__. Just follow the basic math function and the solution is achieved. 

I coded quickly, but then found that using a String to store result will exceed time limit. I then changed to use __char array__ to store result. 

Later I found that insead of using String, I can use __StringBuilder__ to make the program faster. 

### Solution

Two sets of code mentioned above is shown. 

### My code 

My first solution using __StringBuilder to store result__. Passed but not good. (Basically, return "" at the last line is an bad idea)

    public String convert(String s, int nRows) {
        if (nRows <= 1) return s;
        int eachPattern = 2 * nRows - 2;
        int numPatterns = (s.length() - 1) / eachPattern + 1;
        StringBuilder ans = new StringBuilder();
        for (int j = 0; j < nRows; j++) {
            for (int i = 0; i < numPatterns; i++) {
                ans.append(find(s, eachPattern, i, j));
                if (j != 0 && j != nRows - 1)
                    ans.append(find(s, eachPattern, i, 2 * (nRows - 1) - j));
            }
        }
        return ans.toString();
    }
    private String find(String s, int eachPattern, int i, int j) {
        // find (j)th element from (i)th pattern
        int temp = eachPattern * i + j;
        if (temp < s.length())
            return s.substring(temp, temp + 1);
        return "";
    }

Enhance solution, use __char\[\] to store result__

    public String convert(String s, int nRows) {
        if (nRows <= 1) return s;
        int eachPattern = 2 * nRows - 2;
        int numPatterns = (s.length() - 1) / eachPattern + 1;
        char[] ans = new char[s.length()];
        int index = 0;
        for (int j = 0; j < nRows; j++) {
            // j is current row number
            for (int i = 0; i < numPatterns; i++) { 
                // i is current pattern
                char temp = find(s, eachPattern, i, j);
                if (temp == 0) break;
                ans[index++] = temp;
                if (j != 0 && j != nRows - 1) {
                    temp = find(s, eachPattern, i, 2 * (nRows - 1) - j);
                    if (temp == 0) break;
                    ans[index++] = temp;
                }
            }
        }
        return String.valueOf(ans);
    }
    
    private char find(String s, int eachPattern, int i, int j) {
        // find (j)th element from (i)th pattern
        int temp = eachPattern * i + j;
        if (temp < s.length()) return s.charAt(temp);
        return 0;
    }


A much shorter version from [a blog](http://blog.csdn.net/linhuanmars/article/details/21145039) (the idea is same)

    public String convert(String s, int nRows) {
        if (s == null || s.length() == 0 || nRows <= 0) return "";
        if (nRows == 1) return s;
        StringBuilder res = new StringBuilder();
        int size = 2 * nRows - 2;
        for (int i = 0; i < nRows; i++) {
            for (int j = i; j < s.length(); j += size) {
                res.append(s.charAt(j));
                if (i != 0 && i != nRows - 1 && j + size - 2 * i < s.length())
                    res.append(s.charAt(j + size - 2 * i));
            }
        }
        return res.toString();
    }
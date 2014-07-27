---
layout: post
title: "[LeetCode 8] String to Integer (atoi)"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/string-to-integer-atoi/)

<div class="question-content">
            <p></p><p>Implement <span style="font-family:monospace">atoi</span> to convert a string to an integer.</p>

<p><b>Hint:</b> Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.</p>

<p>
<b>Notes:</b> 
It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front. </p>

<div class="spoilers"><b>Requirements for atoi:</b>

<p>The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.</p>

<p>The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.</p>

<p>If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.</p>

<p>If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.
</p>
</div><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">30 minutes</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is easy, just handle all cases listed below: 

1. null or empty string
2. white spaces
3. +/- sign
4. calculate real value
5. handle min & max

### Solution

I'm using __one loop to read it through, and in the end do some checking__. I think my code is quite optimized. There is another [good solution](http://www.programcreek.com/2012/12/leetcode-string-to-integer-atoi/) from online. Idea is same. 

### My code 

    public int atoi(String str) {
        char[] in = str.toCharArray();
        int start = -1, end = -1, sign = 1;
        for (int i = 0; i < in.length; i++) {
            if (start == -1) {
                if (in[i] == ' ') continue;
                else if (in[i] == '+')
                    start = end = i + 1;
                else if (in[i] == '-') {
                    start = end = i + 1;
                    sign = -1;
                } else if (in[i] >= '0' && in[i] <= '9') {
                    start = i;
                    end = i + 1;
                } else
                    return 0;
            } else {
                if (in[i] >= '0' && in[i] <= '9')
                    end = i + 1;
                else break;
            }
        }
        if (start == -1 || start == end || start >= in.length)
            return 0;
        BigInteger num = new BigInteger(str.substring(start, end));
        if (num.compareTo(BigInteger.valueOf(Integer.MAX_VALUE)) > 0)
            return (sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE);
        return sign * num.intValue();
    }
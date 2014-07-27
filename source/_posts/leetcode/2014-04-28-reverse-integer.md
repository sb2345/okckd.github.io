---
layout: post
title: "[LeetCode 7] Reverse Integer"
comments: true
category: Leetcode
tags: [  ]
---


### Question 

[link](http://oj.leetcode.com/problems/reverse-integer/)

<div class="question-content">
<p></p><p>Reverse digits of an integer.</p>

<p style="font-family:monospace">
<b>Example1:</b> x =  123, return  321<br>
<b>Example2:</b> x = -123, return -321
</p>

<div class="spoilers"><b>Have you thought about this?</b>
<p>Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!</p>
<p>If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.</p>
<p>Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?</p>
<p>Throw an exception? Good, but what if throwing an exception is not an option? You would then have to re-design the function (ie, add an extra parameter).</p>
</div><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="lime">10 minutes</td>
	</tr>
</table>

### Analysis

This question is very easy. __But 2 points are very tricky.__

First, __the overflow issue__. This detail is easily omitted. When overflow, we shall return -1. Note that when overflow, the +/- sign of the number changes. Look at the following overflow case for Java int: 


	300000000 * 10 returns -1294967296
	-300000000 * 10 returns 1294967296


So simply check if the number changed sign, we will know if overflow happens. 

Second, __how to handle the negative sign__. My solution will convert negative to positive and proceed. However after reading [this post](http://fisherlei.blogspot.sg/2012/12/leetcode-reverse-integer.html), I realize that we do not necessarily need to handle negative sign. The following code almost works fine: 


    public int reverse2(int x) {
        int reverse = 0;
        while (x != 0) {
            reverse = reverse * 10 + x % 10;
            x /= 10;
        }
        return reverse;
    }


Though above code looks teriffic, __but it's incorrect because it doesn't handle overflow__ (eg. input = 1000000003 or -1000000003). I made small modifications to correct it, and code is shown later.

### Solution

As shown. 

### My code 

First solution, consider +/- and overflow.

    public int reverse1(int x) {
        if (x < 10 && x > -10) return x;
        int sign = 1, num = x;
        if (x < 0) {
            sign = -1;
            num = -1 * x;
        }
        // now num is absolute value of x
        int reverse = 0;
        while (num > 0) {
            reverse = 10 * reverse + num % 10;
            num = num / 10;
        }
        if (reverse < 0) return -1;
            else return reverse * sign;
    }

Second solution, do not consider +/-, only consider overflow.

    public int reverse2(int x) {
        int reverse = 0;
        while (x != 0) {
        	if ((long)x * 10 < Integer.MIN_VALUE 
        		|| (long)x * 10 > Integer.MAX_VALUE)
        			return -1;
            reverse = reverse * 10 + x % 10;
            x /= 10;
        }
        return reverse;
    }


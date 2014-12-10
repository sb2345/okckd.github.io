---
layout: post
title: "[LeetCode 29] Divide Two Integers"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/divide-two-integers/)

<div class="question-content">
            <p></p><p>
Divide two integers without using multiplication, division and mod operator.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is more difficult than you thought__!

I had little experience with __Java bit operation__, so I was struggling in the beginning. I'm still not good at it now. Below is a quick tutorial on this topic. 

<table border="2">
  <tr>
    <th>operator</th>
    <th>what is means</th>
  </tr>
  <tr>
    <td>~</td>
    <td>invert every bit</td>
  </tr>
  <tr>
    <td>&lt;&lt;</td>
    <td>shift left (same as *2)</td>
  </tr>
  <tr>
    <td>&gt;&gt;</td>
    <td>signed shift right</td>
  </tr>
  <tr>
    <td>&gt;&gt;&gt;</td>
    <td>unsigned shift right</td>
  </tr>
  <tr>
    <td>^</td>
    <td>XOR</td>
  </tr>
  <tr>
    <td>|</td>
    <td>OR</td>
  </tr>
</table>
<br />

Note the unsigned right shift operator ">>>" shifts a __zero into the leftmost position__, while the leftmost position after ">>" __depends on sign extension__.

After the knowledge barriers of big operation is cleared, this problem basically is __a while loop that keeps subtracting (divisor * (2 ^ n)) from dividend__. There is various ways to do it. 

__But remember that overflow always can happen__, especially when you dealing with Integer.MAX_VALUE and Integer.MIN_VALUE. 

### Solution

I will post 2 solutions, __first of which is written by me__ using the idea from [this blog](http://leetcodenotes.wordpress.com/2013/10/19/divide-two-integers/). This is also the most common solution from the net. 

__Second solution is from__ [this post](http://discuss.leetcode.com/questions/209/divide-two-integers/385) and I translated the c++ into Java with a bit refactoring work. This code is extremely concise and beautiful. 

### My code 

__First code is written by me__. Please take a look at this line: 

> a = 0 - (long) dividend;

Previously I was using the 2 pieces of code below, and both won't work: 

> a = dividend * -1;

> a = 0 - dividend;

Some extra attentions should be taken on this.


    public int divide(int dividend, int divisor) {
        long sign = 1, a = dividend, b = divisor;
        if (dividend < 0) {
            sign *= -1;
            // this is where caused my error for last submission
            a = 0 - (long) dividend;
        }
        if (divisor < 0) {
            sign *= -1;
            b = 0 - (long) divisor;
        }
        return (int) (sign * helper(a, b));
    }

    public long helper(long a, long b) {
        if (a < b) return 0;
        long remain = a, ans = 0;
        while (remain != 0) {
            long count = 1, num = b;
            if (num > remain) {
                remain = 0;
                break;
            }
            while (num + num > 0 && num + num <= remain) {
                num = num << 1;
                count = count << 1;
            }
            remain -= num;
            ans += count;
        }
        return ans;
    }


__Second code, translated from c plus plus__.


    public int divide(int dividend, int divisor) {
        long a = dividend >>> 31 == 0 ? dividend : 0 - (long) dividend;
        long b = divisor >>> 31 == 0 ? divisor : 0 - (long) divisor;
        long ret = 0;
        while (a >= b) {
            long c = b;
            int i = 0;
            while (a >= c) {
                a -= c;
                ret += 1 << i++;
                c <<= 1;
            }
        }
        return (int) ((dividend ^ divisor) >>> 31 == 0 ? ret : 0 - ret);
    }


---
layout: post
title: "[LeetCode 32] Longest Valid Parentheses "
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/longest-valid-parentheses/)

<div class="question-content">
            <p></p><p>Given a string containing just the characters <code>'('</code> and <code>')'</code>, find the length of the longest valid (well-formed) parentheses substring.
</p>
<p>
For <code>"(()"</code>, the longest valid parentheses substring is <code>"()"</code>, which has length = 2.
</p>
<p>
Another example is <code>")()())"</code>, where the longest valid parentheses substring is <code>"()()"</code>, which has length = 4.
</p><p></p>
          </div>
          
### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

### Analysis

__There are 2 ways to solve this problem__, stack and DP. I will __not cover DP for now__, but this can be a future task. 

There are various way to solve this problem with stack. 

### Solution

__Stack method 1 is more straight-forward__ (code shown below). The idea is to keep a stack of "(" indexes, and another variable called "last". __Note that only ")" can violates a pattern__. So whenever I see a "(", just push to stack. When the pattern is violated by a ")", I update last. The code explains itself very well. If not, [look here](http://discuss.leetcode.com/questions/212/longest-valid-parentheses/1488)

__Stack method 2 is more tricky__. This time I will not only push the index of "(" to stack, but also the index of ")" when the pattern got violated. It's hard to explain, and hard to think of at first. 

__The DP solution is not very difficult__. Basically create an array of same length as string s. dp\[i\] denotes the length of valid parenthese ending with index i. The idea is similar to [this blog](http://blog.csdn.net/abcbc/article/details/8826782), but he used reverse DP, and I use normal DP. 

I will explain DP with an example of input "__)()()__". For this string, we have __dp\[0\] = 0, dp\[1\] = 0, dp\[2\] = 2, dp\[3\] = 0__. For dp\[4\], I check the 3rd position first, and find that dp\[4\] = 2. Then I also have to add dp\[2\] into dp\[4\] to make it complete. The end result is dp\[4\] = 2 + 2 = 4. 

### My code 

Stack method 1


    public int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<Integer>();
        int last = -1, max = 0;
        char[] ss = s.toCharArray();
        for (int i = 0; i < ss.length; i++) {
            if (ss[i] == '(') stack.push(i);
            else if (stack.isEmpty()) last = i;
            else {
                stack.pop();
                if (stack.isEmpty()) max = Math.max(max, i - last);
                else max = Math.max(max, i - stack.peek());
            }
        }
        return max;
    }


Stack method 2

    public int longestValidParentheses(String s) {
        int res = 0;
        Stack<Integer> stack = new Stack<Integer>();
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == ')' && !stack.isEmpty() && arr[stack.peek()] == '(') {
                stack.pop();
                if (stack.isEmpty()) res = i + 1;
                else res = Math.max(res, i - stack.peek());
            } else stack.push(i);
        }
        return res;
    }

DP solution

    public int longestValidParentheses(String s) {
        int len = s.length();
        if (len <= 1) return 0;
        int max = Integer.MIN_VALUE;
        int[] dp = new int[len];
        for (int i = 1; i < len; i ++) {
            if (s.charAt(i) == '(') dp[i] = 0;
            else {
                int j = i - 1 - dp[i - 1];
                if (j >= 0 && s.charAt(j) =='(') {
                    dp[i] = dp[i - 1] + 2;
                    if (j >= 1) dp[i] += dp[j - 1];
                }
                else dp[i] = 0;
            }
            max = Math.max(max, dp[i]);
        }
        return max;
    }

__Updated on July 18th, 2014__, rewrite the stack method 1. 

    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<Integer>();
        int start = -1;
        int longest = 0;
        char[] input = s.toCharArray();
        for (int i = 0; i < input.length; i++) {
            if (input[i] == '(') {
                stack.push(i);
            } else if (input[i] == ')' && stack.isEmpty()) {
                start = i;
            } else if (input[i] == ')') {
                stack.pop();
                if (stack.isEmpty()) {
                    longest = Math.max(longest, i - start);
                } else {
                    longest = Math.max(longest, i - stack.peek());
                }
            }
        }
        return longest;
    }

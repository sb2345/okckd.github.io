---
layout: post
title: "[LeetCode 16] 3Sum Closest"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/3sum-closest/)

<div class="question-content">
            <p></p><p>Given an array <i>S</i> of <i>n</i> integers, find three integers in <i>S</i> such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.</p>

<pre>    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
</pre><p></p>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">20 minutes coding only</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This is a simplified version of 3Sum. __The method is exactly the same as 3Sum, except the return is integer instead of a list of solutions__. This makes life easier because __we do not need to consider duplications__. 

Why? Because in 3Sum, when there is duplicate solution, we need to find them all. But in this question, if a solution is found, the closest value = 0, and is immediately returned. 

### Solution

The code explains itself. 

### My code 


    public int threeSumClosest(int[] num, int target) {
        if (num.length < 3) return 0;
        Arrays.sort(num);
        int diff = Integer.MAX_VALUE, realSum = -1;
        for (int i = 0; i < num.length - 2; i++) {
            int left = i + 1, right = num.length - 1;
            while (left < right) {
                int sum = num[i] + num[left] + num[right];
                if (sum == target) return target;
                else if (sum < target) left++;
                else right--;
                if (diff > Math.abs(sum - target)) {
                    diff = Math.abs(sum - target);
                    realSum = sum;
                }
            }
        }
        return realSum;
    }


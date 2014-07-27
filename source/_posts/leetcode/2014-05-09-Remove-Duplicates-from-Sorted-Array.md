---
layout: post
title: "[LeetCode 26] Remove Duplicates from Sorted Array"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/remove-duplicates-from-sorted-array/)

<div class="question-content">
            <p></p><p>
Given a sorted array, remove the duplicates in place such that each element appear only <i>once</i> and return the new length.</p>

<p>
Do not allocate extra space for another array, you must do this in place with constant memory.
</p>

<p>
For example,<br>
Given input array A = <code>[1,1,2]</code>,
</p>
<p>
Your function should return length = <code>2</code>, and A is now <code>[1,2]</code>.
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
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is easy. 

### Solution

Two pointer operations. 

### My code 


    public int removeDuplicates(int[] A) {
            if (A.length == 0) return 0;
            int left = 1, right = 1;
            int pre = A[0];
            while(right < A.length){
                if (A[right] != pre) {
                    A[left] = A[right];
                    pre = A[left];
                    left ++;
                }
                right ++;
            }
            return left;
    }


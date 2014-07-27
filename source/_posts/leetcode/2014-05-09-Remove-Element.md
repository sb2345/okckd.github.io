---
layout: post
title: "[LeetCode 27] Remove Element"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/remove-element/)

<div class="question-content">
            <p></p><p>Given an array and a value, remove all instances of that value in place and return the new length.
</p>

<p>
The order of elements can be changed. It doesn't matter what you leave beyond the new length.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
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

__I thought 6 lines is the most concise solution, until I read__ [this blog](http://needjobasap.blogspot.sg/2014/01/removeelement-leetcode.html).

### My code 


    public int removeElement(int[] A, int elem) {
            int left = 0, right = 0;
            while (right < A.length) {
                if (A[right] == elem) right++;
                else A[left ++] = A[right ++];
            }
            return left;
    }


Change while loop to for loop, the solution is only 4 lines of code. 


    public int removeElement(int[] A, int elem) {
            int p = 0;
            for (int i = 0; i < A.length; i ++)
                if (A[i] != elem) A[p ++] = A[i];
            return p;
    }


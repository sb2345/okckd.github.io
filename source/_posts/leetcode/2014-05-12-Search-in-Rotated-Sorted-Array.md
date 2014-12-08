---
layout: post
title: "[LeetCode 33] Search in Rotated Sorted Array"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/search-in-rotated-sorted-array/)

<div class="question-content">
            <p></p><p>Suppose a sorted array is rotated at some pivot unknown to you beforehand.</p>

<p>(i.e., <code>0 1 2 4 5 6 7</code> might become <code>4 5 6 7 0 1 2</code>).</p>

<p>You are given a target value to search. If found in the array return its index, otherwise return -1.</p>

<p>You may assume no duplicate exists in the array.</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is actually not difficult__. 

There are 2 ways to solve using binary search. 

__First solution, find the pivot and then decide on__ which side of the sorted array shall I continue searching. I implmented this code. 

__Second solution is a very clever way to solve this problem__. Without having any knowledge of pivot, directly check the mid-point against left number and right number. The idea is from [this blog](http://leetcode.com/2010/04/searching-element-in-rotated-array.html).

### Solution

The code is easy to understand.

### My code 

Find pivot and then binary search (written by me)


    public int search(int[] A, int target) {
        int len = A.length;
        if (len == 0) return 0;
        int left = 0, right = len - 1;
        while (right - left > 1) {
            int mid = (left + right) / 2;
            if (A[mid] > A[left]) left = mid;
            else right = mid;
        }
        // left now points to max value, and right the min value
        if (target >= A[0]) {
            right = left;
            left = 0;
        } else {
            left = right;
            right = len - 1;
        }
        // now search for target between left and right
        while (left <= right) {
            int mid = (left + right) / 2;
            if (A[mid] == target) return mid;
            else if (A[mid] > target) right = mid - 1;
            else if (A[mid] < target) left = mid + 1;
        }
        if (right >= 0 && left < len && A[left] == target) return left;
        else return -1;
    }


__Without knowledge of pivot__, a great solution.

Pay special attention to different larger/smaller conditions. It's very easy to miss a equal sign or something. 


    public int search(int[] A, int target) {
        int left = 0;
        int right = A.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (target == A[mid]) return mid;
            if (A[left] <= A[mid]) {
                if (A[left] <= target && target <= A[mid]) right = mid;
                else left = mid + 1;
            } else {
                if (A[mid] <= target && target <= A[right]) left = mid;
                else right = mid - 1;
            }
        }
        return -1;
    }


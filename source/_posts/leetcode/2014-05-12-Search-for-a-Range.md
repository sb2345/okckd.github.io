---
layout: post
title: "[LeetCode 34] Search for a Range"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/search-for-a-range/)

<div class="question-content">
            <p></p><p>Given a sorted array of integers, find the starting and ending position of a given target value.</p>

<p>Your algorithm's runtime complexity must be in the order of <i>O</i>(log <i>n</i>).</p>

<p>If the target is not found in the array, return <code>[-1, -1]</code>.</p>

<p>
For example,<br>
Given <code>[5, 7, 7, 8, 8, 10]</code> and target value 8,<br>
return <code>[3, 4]</code>.
</p><p></p>
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
		<td bgcolor="red">Difficult</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__The key to solve this problem is binary search__. Previously my solution is to find the element first, then check left bound and right bound 1 by 1. In worst case, this will take O(n) time. I wrote the code in 20 minutes and passed, but unfortunately, this is not the correct solution. 

There are many possible binary search solutions, and I will list out 2 solutions from the Internet. 

__First solution is from [this blog](http://xixiaogualu.blogspot.sg/2013/09/search-for-range.html)__. Using binary search to search twice - once for left bound, and once for right bound. Code is below. 

__Second solution is from [this blog](http://rleetcode.blogspot.sg/2014/02/search-for-range-java.html)__. This idea is still using binary search, but a tricky way. Instead of searching the number, it searches (number - 0.5) and (number + 0.5). 

### Solution

I will not explains the code, since it's easy to understand (but hard to write). It's important that I __practice implementing this code by myself__ some time. 

### My code 

Solution 1


    public int[] searchRange(int[] A, int target) {
        int i = 0, j = A.length - 1;
        int[] result = { -1, -1 };
        // the idea is to put the lower bound in i
        while (i < j) {
            int mid = i + (j - i) / 2;
            if (target <= A[mid]) j = mid;
            else i = mid + 1;
        }
        if (A[i] == target) result[0] = i;
        else return result;
        i = 0; 
        j = A.length;
        // the idea is to put the upper bound in j-1
        while (i < j) {
            int mid = i + (j - i) / 2;
            if (target >= A[mid]) i = mid + 1;
            else j = mid;
        }
        result[1] = j - 1;
        return result;
    }


Solution 2


    public int[] searchRange(int[] A, int target) {
        if (A == null) return null;
        int[] result = { -1, -1 };
        int low = binarySearch(A, target - 0.5);
        // Be care for there , low>=A.length must be checked
        if (low >= A.length || A[low] != target) return result;
        result[0] = low;
        result[1] = binarySearch(A, target + 0.5) - 1;
        return result;
    }

    public int binarySearch(int[] A, double t) {
        int low = 0, high = A.length - 1;
        while (low <= high) {
            int m = (low + high) / 2;
            if (A[m] < t) low = m + 1;
            if (A[m] > t) high = m - 1;
        }
        return low;
    }


---
layout: post
title: "[LeetCode 4] Median of Two Sorted Arrays"
comments: true
category: Leetcode
tags: [  ]
---

### Question 
[link](https://oj.leetcode.com/problems/median-of-two-sorted-arrays/)

<div class="question-content">
<p></p><p>There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).</p>
<p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">infiinty</td>
	</tr>
</table>

### Analysis

__This is a very tough question__. I read a lot but struggles even now. 

Note that the 2 arrays have __different sizes__ (i.e. m and n). __If the size of the 2 arrays are same__ (which is a special case of this question), there is a much easier "Divide and Conquer" solution. The idea is to compare the median of 2 arrays and eliminate half of each array every time. Details, look [this post](http://www.geeksforgeeks.org/median-of-two-sorted-arrays/).

Now for this questions. 

This solution is covered in the [MIT CLRS handouts](http://www2.myoops.org/course_material/mit/NR/rdonlyres/Electrical-Engineering-and-Computer-Science/6-046JFall-2005/30C68118-E436-4FE3-8C79-6BAFBB07D935/0/ps9sol.pdf). The basic idea is, finding the median of the first array, then assuming this number is the final median, and look where this element should have been put in the second array. There are 3 possible conditions. For example, if the arrays are {1, 4, 5, 6, 26} and {2, 13, 34}. We first get number 5, and compare it with 13. Then we know that median shall be large than 5, and we continue this (sort of) binary search with O(lgn) complexity. 

### Solution

I referred to NineChap for the 'find (K)th' solution. 

### My code 

__Code from [ninechap](http://answer.ninechapter.com/solutions/median-of-two-sorted-arrays/)__

    public double findMedianSortedArrays(int A[], int B[]) {
        int len = A.length + B.length;
        if (len % 2 == 0) {
            return (findKth(A, 0, B, 0, len / 2) + findKth(A, 0, B, 0, len / 2 + 1)) / 2.0 ;
        } else {
            return findKth(A, 0, B, 0, len / 2 + 1);
        }
    }
    
    // find kth number of two sorted array
    public static int findKth(int[] A, int A_start, int[] B, int B_start, int k){		
		if(A_start >= A.length) 
			return B[B_start + k - 1];
		if(B_start >= B.length)
			return A[A_start + k - 1];

		if (k == 1)
			return Math.min(A[A_start], B[B_start]);
		
		int A_key = A_start + k / 2 - 1 < A.length
		            ? A[A_start + k / 2 - 1]
		            : Integer.MAX_VALUE;
		int B_key = B_start + k / 2 - 1 < B.length
		            ? B[B_start + k / 2 - 1]
		            : Integer.MAX_VALUE; 
		
		if (A_key < B_key) {
			return findKth(A, A_start + k / 2, B, B_start, k - k / 2);
		} else {
			return findKth(A, A_start, B, B_start + k / 2, k - k / 2);
		}
	}

__Updated on July 6th__: I finally wrote this code by myself. It's difficult to write. 

    public double findMedianSortedArrays(int A[], int B[]) {
        int len1 = A.length;
        int len2 = B.length;
        if ((len1 + len2) % 2 == 1) {
            return findKth(A, B, 0, 0, (len1 + len2) / 2);
        } else {
            int num1 = findKth(A, B, 0, 0, (len1 + len2) / 2 - 1);
            int num2 = findKth(A, B, 0, 0, (len1 + len2) / 2);
            return (double) (num1 + num2) / 2;
        }
    }
    
    private int findKth(int A[], int B[], int start1, int start2, int k) {
        int len1 = A.length;
        int len2 = B.length;
        if (start1 >= len1) {
            return B[start2 + k];
        } 
        if (start2 >= len2) {
            return A[start1 + k];
        } 
        if (k == 0) {
            return Math.min(A[start1], B[start2]);
        }
        // now eliminate half of the size of k (half >= 1)
        int half = (k + 1) / 2;
        int aMid = start1 + half - 1 < len1 ? A[start1 + half - 1] : Integer.MAX_VALUE;
        int bMid = start2 + half - 1 < len2 ? B[start2 + half - 1] : Integer.MAX_VALUE;
        if (aMid < bMid) {
            // discard size of half from A
            return findKth(A, B, start1 + half, start2, k - half);
        } else {
            // discard size of half from B
            return findKth(A, B, start1, start2 + half, k - half);
        }
    }

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
    <p></p>
    
    <p>There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
    </p>
    
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
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a tough question__. 

__If the size of the 2 arrays (i.e. m and n) are same__, this would become a much easier question with simple "Divide and Conquer" solution. Well, not extremely easy like everyone can solve it, but a much simpler one. I do recommend you to read more at [this post](http://www.geeksforgeeks.org/median-of-two-sorted-arrays/) before you procceed. 

However, this question is not as simple. Let's talk about it. 

__This first solution is well covered in the [MIT CLRS handouts](http://www2.myoops.org/course_material/mit/NR/rdonlyres/Electrical-Engineering-and-Computer-Science/6-046JFall-2005/30C68118-E436-4FE3-8C79-6BAFBB07D935/0/ps9sol.pdf)__. The basic idea is, finding the median of the first array, then assuming this number is the final median, and look where this element should have been put in the second array. There are 3 possible conditions. For example, if the arrays are {1, 4, 5, 6, 26} and {2, 13, 34}. We first get number 5, and compare it with 13. Then we know that median shall be large than 5, and we continue this (like) binary search with O(lgn) complexity. This solution is complex and difficult in thinking. I would like to focus on a different solution. 

__Second solution, credit goes to [ninechap](http://answer.ninechapter.com/solutions/median-of-two-sorted-arrays/)__. Finding the median is like finding the (k)th element from the combination of 2 arrays. We might have to search for (k)th element twice, but the overall complexity is always O(lg n). 

### My code 

    public class Solution {
        public double findMedianSortedArrays(int A[], int B[]) {
            if (A == null || B == null) {
                return 0;
            }
            int len = A.length + B.length;
            int k1 = (len - 1) / 2;
            int k2 = len / 2;

            // now get 2 median numbes (they might be same)
            // then return the calculated median number:
            double mid1 = getKth(A, B, 0, 0, k1);
            double mid2 = getKth(A, B, 0, 0, k2);
            return (mid1 + mid2) / 2;
        }

        private double getKth(int[] A, int[] B, int a, int b, int k) {
            if (a == A.length) {
                // all elements in A is used up
                return B[b + k];
            } else if (b == B.length) {
                // all elements in B is used up
                return A[a + k];
            }
            // now both A[a] and B[b] are valid elements, check half of k
            if (k == 0) {
                // if we only have to compare 2 elements
                return Math.min(A[a], B[b]);
            } else {
                // 'half' number of elements will be discard from either A or B
                // since k is large than 0, half must be larger than 0
                int half = (k + 1) / 2;

                // mid1 and mid2 are boundary indexes to be discarded
                // mid1 is equals or larger than a
                int mid1 = a + half - 1;
                int mid2 = b + half - 1;

                // val1 and val2 are boundary values to be discarded
                int val1;
                int val2;
                if (mid1 >= A.length) {
                    val1 = Integer.MAX_VALUE;
                } else {
                    val1 = A[mid1];
                }
                if (mid2 >= B.length) {
                    val2 = Integer.MAX_VALUE;
                } else {
                    val2 = B[mid2];
                }

                // compare val1 and val2 and discard all elements to the left 
                // of the smaller one, inclusively
                if (val1 > val2) {
                    // discard mid2 and all elements to the left of it
                    return getKth(A, B, a, mid2 + 1, k - half);
                } else {
                    return getKth(A, B, mid1 + 1, b, k - half);
                }
            }
        }
    }

Note: starting from today, I would post my code with more focus on readability, instead of conciseness. Sometimes, the former is much more important than the latter. 

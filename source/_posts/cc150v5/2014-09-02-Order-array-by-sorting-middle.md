---
layout: post
title: "[CC150v5] 17.6 Order an Array by Sorting Middle"
comments: true
category: CC150v5
tags: [  ]
---

### Question

> Given an array of integers, write a method to find indices m and n such that if you sorted elements m through n, the entire array would be sorted. Minimize n-m (that is, find the smallest such sequence).

### Solution

Referring to [this guy](http://www.mitbbs.com/article_t/JobHunting/32772399.html): 

> 1. 找到heading的最长递增序列
>
> 1. 找到tailing的最长的递增序列

After that: 

> 1. 用中间部分的min去shrink左边 更新max
>
> 1. 根据更新后的max shrink右边 更新min
>
> 1. 再一次shrink左边

### Code

	public static int findEndOfLeftSubsequence(int[] array) {
		for (int i = 1; i < array.length; i++) {
			if (array[i] < array[i - 1]) {
				return i - 1;
			}
		}
		return array.length - 1;
	}

	public static int findStartOfRightSubsequence(int[] array) {
		for (int i = array.length - 2; i >= 0; i--) {
			if (array[i] > array[i + 1]) {
				return i + 1;
			}
		}
		return 0;
	}

	public static int shrinkLeft(int[] array, int min_index, int start) {
		int comp = array[min_index];
		for (int i = start - 1; i >= 0; i--) {
			if (array[i] <= comp) {
				return i + 1;
			}
		}
		return 0;
	}

	public static int shrinkRight(int[] array, int max_index, int start) {
		int comp = array[max_index];
		for (int i = start; i < array.length; i++) {
			if (array[i] >= comp) {
				return i - 1;
			}
		}
		return array.length - 1;
	}

	public static void findUnsortedSequence(int[] array) {
		// find left subsequence
		int end_left = findEndOfLeftSubsequence(array);

		if (end_left >= array.length - 1) {
			// System.out.println("The array is already sorted.");
			return; // Already sorted
		}

		// find right subsequence
		int start_right = findStartOfRightSubsequence(array);

		int max_index = end_left; // max of left side
		int min_index = start_right; // min of right side
		for (int i = end_left + 1; i < start_right; i++) {
			if (array[i] < array[min_index]) {
				min_index = i;
			}
			if (array[i] > array[max_index]) {
				max_index = i;
			}
		}

		// slide left until less than array[min_index]
		int left_index = shrinkLeft(array, min_index, end_left);

		// slide right until greater than array[max_index]
		int right_index = shrinkRight(array, max_index, start_right);

		if (validate(array, left_index, right_index)) {
			System.out.println("TRUE: " + left_index + " " + right_index);
		} else {
			System.out.println("FALSE: " + left_index + " " + right_index);
		}
	}

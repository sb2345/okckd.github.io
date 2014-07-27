---
layout: post
title: "[LeetCode 61] Rotate List"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/rotate-list/)

<div class="question-content">
            <p></p><p>Given a list, rotate the list to the right by <i>k</i> places, where <i>k</i> is non-negative.</p>

<p>For example:<br>
Given <code>1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;NULL</code> and <i>k</i> = <code>2</code>,<br>
return <code>4-&gt;5-&gt;1-&gt;2-&gt;3-&gt;NULL</code>.</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very basic question, but not very easy__. 

The implementation is a lot of node operations, I won't go into details. 

### Solution

__I have 2 solutions, one using preHead and one without__. I realize the solution without preHead is better, so I post the code below. 

__The most popular solution on Internet make use of list size and (n % size) to get the absolute steps__. This is an nice idea, but the code is lengthy. Since almost everyone is posting this solution, I'll post this code as well, from [this blog](http://rleetcode.blogspot.sg/2014/01/rotate-list-java.html). 

### My code

__My code__


    public ListNode rotateRight(ListNode head, int n) {
        if (head == null || n == 0) return head;
        ListNode left = head, right = head;
        for (int i = 0; i < n; i ++) {
            right = right.next;
            if (right == null) right = head;
        }
        while (right.next != null) {
            left = left.next;
            right = right.next;
        }
        if (left.next == null) return head;
        ListNode newHead = left.next;
        right.next = head;
        left.next = null;
        return newHead;
    }


__Solution in the blog.__


    public ListNode rotateRight(ListNode head, int n) {
        if (head == null || n == 0) {
            return head;
        }
        int len = 1;
        ListNode last = head;
        // calculate the lenght of given list
        while (last.next != null) {
            last = last.next;
            len++;
        }
        last.next = head;
        // Should considered the situtation that n larger than given list's length
        int k = len - n % len;
        ListNode preHead = last;
        // find the point which are previuse for our target head
        while (k > 0) {
            preHead = preHead.next;
            k--;
        }
        head = preHead.next;
        preHead.next = null;
        return head;
    }


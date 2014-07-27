---
layout: post
title: "[LeetCode 21] Merge Two Sorted Lists"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/merge-two-sorted-lists/)

<div class="question-content">
            <p></p><p>Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is easy__. There are difficult ways to solve. 

### Solution

I wrote 2 versions of code, one using recursion and one using direct approach (fake header + link operations). __Surprisingly my second code is EXACTLY same__ as the code written in [this blog](http://www.programcreek.com/2012/12/leetcode-merge-two-sorted-lists-java/). 

### My code 

Recursion: 


    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
            if (l1 == null) return l2;
            if (l2 == null) return l1;
            if (l1.val > l2.val) {
                l2.next = mergeTwoLists(l1, l2.next);
                return l2;
            }
            else{
                l1.next = mergeTwoLists(l1.next, l2);
                return l1;
            }

    }


Fake header + link operations


    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
            ListNode pre = new ListNode(Integer.MIN_VALUE);
            ListNode cur = pre;
            while (l1 != null && l2 != null) {
                if (l1.val < l2.val) {
                    cur.next = l1;
                    l1 = l1.next;
                } else {
                    cur.next = l2;
                    l2 = l2.next;
                }
                cur = cur.next;
            }
            if (l1 == null) cur.next = l2;
            else cur.next = l1;
            return pre.next;
    }


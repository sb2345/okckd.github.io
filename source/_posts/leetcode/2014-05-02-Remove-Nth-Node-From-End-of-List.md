---
layout: post
title: "[LeetCode 19] Remove Nth Node From End of List"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/remove-nth-node-from-end-of-list/)

<div class="question-content">
            <p></p><p>Given a linked list, remove the <i>n</i><sup>th</sup> node from the end of list and return its head.</p>

<p>
For example,</p>

<pre>   Given linked list: <b>1-&gt;2-&gt;3-&gt;4-&gt;5</b>, and <b><i>n</i> = 2</b>.

   After removing the second node from the end, the linked list becomes <b>1-&gt;2-&gt;3-&gt;5</b>.
</pre>

<p>
<b>Note:</b><br>
Given <i>n</i> will always be valid.<br>
Try to do this in one pass.
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
		<td bgcolor="lime">2</td>
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

__This question is easy__. Just keep 2 pointers of a certain distance, and move together. 

### Solution

The code explains itself. 

### My code 


    public ListNode removeNthFromEnd(ListNode head, int n) {
            ListNode p1 = head;
            ListNode p2 = head;
            for (int i=0 ; i<n ; i++){
                p2 = p2.next;
            }
            if (p2 == null){
                return head.next;
            }
            // now p1 and p2 move together
            while(p2.next != null){
                p1 = p1.next;
                p2 = p2.next;
            }
            p1.next = p1.next.next;
            return head;
    }


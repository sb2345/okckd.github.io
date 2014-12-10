---
layout: post
title: "[LeetCode 25] Reverse Nodes in k-Groups "
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/reverse-nodes-in-k-group/)

<div class="question-content">
<p></p><p>
Given a linked list, reverse the nodes of a linked list <i>k</i> at a time and return its modified list.
</p>

<p>
If the number of nodes is not a multiple of <i>k</i> then left-out nodes in the end should remain as it is.</p>

<p>You may not alter the values in the nodes, only nodes itself may be changed.</p>

<p>Only constant memory is allowed.</p>

<p>
For example,<br>
Given this linked list: <code>1-&gt;2-&gt;3-&gt;4-&gt;5</code>
</p>

<p>
For <i>k</i> = 2, you should return: <code>2-&gt;1-&gt;4-&gt;3-&gt;5</code>
</p>

<p>
For <i>k</i> = 3, you should return: <code>3-&gt;2-&gt;1-&gt;4-&gt;5</code>
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
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
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

I solved this problem at first, but second time when I try to do it again, I am faced with great difficulty (maybe I didn't slept well laterly?). 

__The problem is solved in 2 steps__. First, get the next k-group. If remaining items is less than k, terminate the program. Otherwise, reserve this k-group and keep going. 

To solve this question is very tricky. __We need to be clear about this: 4 nodes need to be kept track of__: 2 elements before and after the k-group, and 2 elements within the k-group. 

__The difficult point is while and after reverse the k-group__, how to maintain the 'pre' node and future 'pre' node correctly. 

### Solution

Used template to solve. 

### My code 

A standard solution from [this blog](http://blog.csdn.net/linhuanmars/article/details/19957455)

    public ListNode reverseKGroup(ListNode head, int k) {  
        if(head == null) return null;
        ListNode dummy = new ListNode(0);  
        dummy.next = head;  
        int count = 0;  
        ListNode pre = dummy, cur = head;  
        while(cur != null) {  
            cur = cur.next;
            if(++count == k) {
                pre = reverse(pre, cur);  
                count = 0; 
            }
        }
        return dummy.next;  
    }  
    private ListNode reverse(ListNode pre, ListNode end) {
        ListNode head = pre.next;  
        ListNode cur = pre.next.next;  
        while(cur!=end) {  
            ListNode next = cur.next;  
            cur.next = pre.next;  
            pre.next = cur;  
            cur = next;  
        }  
        head.next = end;  
        return head;  
    } 

__Updated on June 21st, 2014__, I used Linkedlist Template from NineChap and solved this problem fast and neat! 

    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode p = head;
        int count = 0;
        while (p != null) {
            p = p.next;
            count++;
        }
        return helper(head, k, count);
    }
    
    public ListNode helper(ListNode head, int k, int count) {
        if (head == null || k < 1 || count < k) {
            return head;
        }
        ListNode result = null;
        ListNode cur = head;
        for (int i = 0; i < k; i++) {
            if (cur == null) break;
            ListNode temp = cur.next;
            cur.next = result;
            result = cur;
            cur = temp;
        }
        head.next = helper(cur, k, count - k);
        return result;
    }

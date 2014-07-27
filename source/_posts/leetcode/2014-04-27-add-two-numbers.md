---
layout: post
title: "[LeetCode 2] Add Two Numbers"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/add-two-numbers/)

<div class="question-content">
<p></p><p>You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.</p>
<p style="font-family:monospace">
<b>Input:</b> (2 -&gt; 4 -&gt; 3) + (5 -&gt; 6 -&gt; 4)<br>
<b>Output:</b> 7 -&gt; 0 -&gt; 8</p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="">-------</td>
	</tr>
</table>

### Analysis

This question is easy and straight-forward

### Solution

__The only tricky part of this question__ is when to create a new ListNode Object. Node the following code for ListNode Class: 


/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */


__There is no constructor ListNode()__, which means we must initialize the value in __ListNode(int x)__ when create the ListNode object. This is weird, because we do not know the value of the first digit yet, how to create the object then? 

This is solved by a clever workaround by creating an initial object, and store the returned value in 'initialObject.next'. Details please see my solution.

### My code

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode ans = add(l1, l2, new ListNode(0), 0);
        return ans.next;
    }

    private ListNode add(ListNode a, ListNode b, ListNode pre, int extra) {
        int aa = 0, bb = 0, sum = 0;
        if (a == null && b == null) {
            if (extra == 0)	return pre;
            else {
                pre.next = new ListNode(1);
                return pre;
            }
        }
        if (a != null) aa = a.val;
        if (b != null) bb = b.val;
        sum = aa + bb + extra;
        pre.next = new ListNode(sum % 10);
        if (a == null)      add(null, b.next, pre.next, sum / 10);
        else if (b == null) add(a.next, null, pre.next, sum / 10);
        else                add(a.next, b.next, pre.next, sum / 10);
        return pre;
    }


A very good online [solution](http://gongxuns.blogspot.sg/2012/12/leetcodeadd-two-numbers.html)


    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carry =0;
        ListNode res = new ListNode(0);
        ListNode cur1 = l1, cur2 = l2, head=res;
        while(cur1!=null || cur2!=null){
            if(cur1!=null){
                carry+=cur1.val;
                cur1=cur1.next;
            }
            if(cur2!=null){
                carry+=cur2.val;
                cur2=cur2.next;
            }
            head.next=new ListNode(carry%10);
            head=head.next;
            carry/=10;
        }
        if(carry==1) head.next=new ListNode(1);
        return res.next;
    }


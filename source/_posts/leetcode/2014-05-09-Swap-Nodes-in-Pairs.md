---
layout: post
title: "[LeetCode 24] Swap Nodes in Pairs"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/swap-nodes-in-pairs/)

<div class="question-content">
            <p></p><p>
Given a linked list, swap every two adjacent nodes and return its head.
</p>

<p>
For example,<br>
Given <code>1-&gt;2-&gt;3-&gt;4</code>, you should return the list as <code>2-&gt;1-&gt;4-&gt;3</code>.
</p>

<p>
Your algorithm should use only constant space. You may <b>not</b> modify the values in the list, only nodes itself can be changed.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
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

__This is an very very interesting question__. We can use either recursions or link operations to solve the problem (the second being more difficult). I have write code for both. 

However, looking around the internet, I realize __the solution can be extremely concise__. 

### Solution

I post 3 pieces of code below. 

I will explain second code a little bit. __The idea is keep 3 pointers always__: pre, cur and (cur.next). Inside the while loop, I will swap cur and (cur.next), and let pre point to (cur.next). Then I can proceed to next loop, with the updated pre and cur pointer. 

__However, looking at the last code, I realize previous approach is too complex__. [This idea](http://oj.leetcode.com/discuss/3608/seeking-for-a-better-solution) is keeping only 1 pointer at a time, and swap the next 2 nodes following this pointer. In this way, the code is extremely concise and the logic is much more easier to understand. 

### My code 

Recursion code, by me. 


    public ListNode swapPairs(ListNode head) {
            if (head == null || head.next == null) return head;
            ListNode newHead = head.next;
            head.next = swapPairs(newHead.next);
            newHead.next = head;
            return newHead;
    }


Direct approach, written by me. Many blogs including [this one](http://gongxuns.blogspot.sg/2012/12/leetcodeswap-nodes-in-pairs.html) gives the same solution. 


    public ListNode swapPairs(ListNode head) {
            if (head == null) return head;
            ListNode preHead = new ListNode(1);
            preHead.next = head;
            ListNode cur = head, pre = preHead;
            while (cur != null && cur.next != null) {
                pre.next = cur.next;
                ListNode newCur = cur.next.next;
                cur.next.next = cur;
                cur.next = newCur;
                pre = cur;
                cur = newCur;
            }
            return preHead.next;
    }


This is a great solution by [leetcode user Tao2014](http://oj.leetcode.com/discuss/3608/seeking-for-a-better-solution).


    public ListNode swapPairs(ListNode head) {
            ListNode start = new ListNode(0); 
            start.next = head;
            for (ListNode cur = start; cur.next != null && cur.next.next != null; 
                    cur = cur.next.next) {
                cur.next = swap(cur.next, cur.next.next);
            }
            return start.next;
    }

    private ListNode swap(ListNode next1, ListNode next2) {
            next1.next = next2.next;
            next2.next = next1;
            return next2;
    }

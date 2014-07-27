---
layout: post
title: "[LeetCode 23] Merge k Sorted Lists"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/merge-k-sorted-lists/)

<div class="question-content">
            <p></p><p>
Merge <i>k</i> sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">Difficult</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are two ways to solve this problem. 

* k - number of lists
* n - String length of each list

__First approach is merge sort__. Using divide and conquer approach, divide the entire input into halves, and then merge 2 list each time. Instead of merging 1 by 1 which the time complexity is O(nk x (k-1)), the 2 lists to be merged is always similar length, thus time complexity is reduced to O(nk x logk). 

__You may wonder how I calculate time complexity__. See, each round of sort, nk nodes are read and sorted. This happened O(logk) times, where k is the number of lists. Thus totoal time take is O(nk x logk). 

__Second approach is heap sort__. The idea of this is to always keep a sorted list of the head of each list. But before the code, what actually is heap/priority queue? 

> __[Heap](http://en.wikipedia.org/wiki/Heap_%28data_structure%29) is a specialized tree-based data structure__. Heap is crucial in Dijkstra's algorithm and heapsort. 
>
> We take max heap for example. The keys of parent nodes are always greater than or equal to the children node. 
>
> __The heap is an implementation of priority queue__. In fact, priority queues are often referred to as "heaps", regardless of how they may be implemented. 
>
> Note that despite the similarity of the name "heap" to "stack" and "queue", the latter two are __abstract data types__, while a heap is a __specific data structure__, and "priority queue" is the proper term for the abstract data type. 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
</style>
<table class="tg">
  <tr>
    <th class="tg-s6z2">Heap</th>
    <th class="tg-s6z2">Time</th>
  </tr>
  <tr>
    <td class="tg-031e">Find max</td>
    <td class="tg-s6z2">O(1)</td>
  </tr>
  <tr>
    <td class="tg-031e">Delete</td>
    <td class="tg-s6z2">O(lgn)</td>
  </tr>
  <tr>
    <td class="tg-031e">Insert</td>
    <td class="tg-s6z2">O(lgn)</td>
  </tr>
  <tr>
    <td class="tg-031e">Merge</td>
    <td class="tg-s6z2">O(n)</td>
  </tr>
</table>
<br />

Both method are well explained in [this csdn blog](http://blog.csdn.net/linhuanmars/article/details/19899259). Time complexity analysis is given by [nootcoder blog](http://n00tc0d3r.blogspot.sg/2013/04/merge-k-sorted-lists.html). 

### Solution

First, divide and conquer code is lengthy but medium difficulty. 

Second solution, however, is not as easy. __Especially when we have to write Comparator on our own__.  A priority queue (heap) is implemented and head of each list is inserted into the heap. Then poll elements out from the heap until heap is empty. 

### My code 

Merge sort code.

    public ListNode mergeKLists(List<ListNode> lists) {
        if (lists == null || lists.size() == 0) {
            return null;
        }
        return mergeHelper(lists, 0, lists.size() - 1);
    }
    
    private ListNode mergeHelper(List<ListNode> lists, int start, int end) {
        if (start == end) {
            return lists.get(start);
        } 
        int mid = start + (end - start) / 2;
        ListNode firstHalf = mergeHelper(lists, start, mid);
        ListNode secondHalf = mergeHelper(lists, mid + 1, end);
        return mergeTwo(firstHalf, secondHalf);
    }
    
    private ListNode mergeTwo(ListNode head1, ListNode head2) {
    	ListNode dummy = new ListNode(0);
    	ListNode p = dummy;
    	while (head1 != null && head2 != null) {
    		if (head1.val < head2.val) {
    			p.next = head1;
    			head1 = head1.next;
    			p = p.next;
    		} else {
    			p.next = head2;
    			head2 = head2.next;
    			p = p.next;
    		}
    	}
    	if (head1 == null) {
    		p.next = head2;
    	} else {
    		p.next = head1;
    	}
    	return dummy.next;
    }

Heap sort code, written by me. [source](http://answer.ninechapter.com/solutions/merge-k-sorted-lists/)

__Look at how a Comparator is implemented__! 

	private Comparator<ListNode> listNodeComparator = new Comparator<ListNode>() {
		public int compare(ListNode o1, ListNode o2) {
			return o1.val - o2.val;
		}
	};

	public ListNode mergeKLists(List<ListNode> lists) {
		if (lists == null || lists.size() == 0) {
			return null;
		}
		Queue<ListNode> heap = new PriorityQueue<ListNode>(lists.size(),
				listNodeComparator);
		for (ListNode node : lists) {
			if (node != null) {
				heap.add(node);
			}
		}
		ListNode dummy = new ListNode(0);
		ListNode p = dummy;
		while (!heap.isEmpty()) {
			ListNode smallest = heap.poll();
			p.next = smallest;
			p = p.next;
			if (smallest.next != null) {
				heap.add(smallest.next);
			}
		}
		return dummy.next;
	}

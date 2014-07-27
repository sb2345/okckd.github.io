---
layout: post
title: "[LeetCode 57] Insert Interval"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/insert-interval/)

<div class="question-content">
            <p></p><p>Given a set of <i>non-overlapping</i> intervals, insert a new interval into the intervals (merge if necessary).</p>

<p>You may assume that the intervals were initially sorted according to their start times.</p>

<p>
<b>Example 1:</b><br>
Given intervals <code>[1,3],[6,9]</code>, insert and merge <code>[2,5]</code> in as <code>[1,5],[6,9]</code>.
</p>

<p>
<b>Example 2:</b><br>
Given <code>[1,2],[3,5],[6,7],[8,10],[12,16]</code>, insert and merge <code>[4,9]</code> in as <code>[1,2],[3,10],[12,16]</code>.
</p>

<p>
This is because the new interval <code>[4,9]</code> overlaps with <code>[3,5],[6,7],[8,10]</code>.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
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
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is not an easy question, though it's similar to the question "Merge Intervals"__. 

__My solution is based on solution of "Merge Intervals"__. I did 2 iteration in the list. 

There are many online solutions that only iterate once. 

### Solution

__My solution is first insert newInterval into the list, and then merge it__. The code is easy to read. 

__Second code is from [this repo](https://github.com/yuanx/leetcode/blob/master/InsertInterval.java)__. This is only 1 iteration, but in 3 stages. First, add all intervals ahead of newInterval into ans. Second, merge anything that can be merged with newInterval, and add to ans. Third, add the rest of intervals into ans. 

__Third code is from [this blog](http://www.programcreek.com/2012/12/leetcode-insert-interval/)__. This code is widely seen in blogs, but It's a very tricky way to solve. I don't have much love for this solution. 

### My code

__My code__


    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        int len = intervals.size();
        if (len == 0) {
            intervals.add(newInterval);
            return intervals;
        }
        int pre = Integer.MIN_VALUE;
        int insert = newInterval.start;
        // first loop, find insert position
        int i = 0;
        for (i = 0; i < len; i ++) {
            Interval cur = intervals.get(i);
            if (pre < insert && insert <= cur.end) {
                if (insert < cur.start) intervals.add(i, newInterval);
                else intervals.add(i + 1, newInterval);
                break;
            }
        }
        if (i == len) // no merge required
            intervals.add(newInterval);
        else // second loop
            while (i < intervals.size() - 1 && 
                    intervals.get(i).end >= intervals.get(i+1).start) {
                intervals.get(i).end = Math.max(intervals.get(i).end, 
                        intervals.get(i+1).end);
                intervals.remove(i + 1);
            }
        return intervals;
    }


__Second code, a quite good idea__. 


    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList<Interval> re = new ArrayList<Interval>();
        int len = intervals.size();
        int i = 0;
        while (i < len) {
            Interval temp = intervals.get(i);
            if (temp.end < newInterval.start)
                re.add(temp);
            else if (temp.start > newInterval.end)
                break;
            else {
                newInterval.start = Math.min(temp.start, newInterval.start);
                newInterval.end = Math.max(temp.end, newInterval.end);
            }
            i++;
        }
        re.add(newInterval);
        while (i < len) {
            re.add(intervals.get(i));
            i++;
        }
        return re;
    }


__Third code, the most popular solution__. Very tricky and concise indeed, but I don't think it's better than second code. 


    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList<Interval> result = new ArrayList<Interval>();
        for(Interval interval: intervals){
            if(interval.end < newInterval.start){
                result.add(interval);
            }else if(interval.start > newInterval.end){
                result.add(newInterval);
                newInterval = interval;        
            }else if(interval.end >= newInterval.start 
                    || interval.start <= newInterval.end){
                newInterval = new Interval(
                    Math.min(interval.start, newInterval.start), 
                    Math.max(newInterval.end, interval.end));
            }
        }
        result.add(newInterval); 
        return result;
    }

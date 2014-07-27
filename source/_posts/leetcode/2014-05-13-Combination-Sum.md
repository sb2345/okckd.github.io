---
layout: post
title: "[LeetCode 39] Combination Sum"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/combination-sum/)

<div class="question-content">
            <p></p><p>
Given a set of candidate numbers (<b><i>C</i></b>) and a target number (<b><i>T</i></b>), find all unique combinations in <b><i>C</i></b> where the candidate numbers sums to <b><i>T</i></b>. 
</p>

<p>The <b>same</b> repeated number may be chosen from <b><i>C</i></b> unlimited number of times.
</p>

<p><b>Note:</b><br>
</p><ul>
<li>All numbers (including target) will be positive integers.</li>
<li>Elements in a combination (<i>a</i><sub>1</sub>, <i>a</i><sub>2</sub>, … , <i>a</i><sub>k</sub>) must be in non-descending order. (ie, <i>a</i><sub>1</sub> ≤ <i>a</i><sub>2</sub> ≤ … ≤ <i>a</i><sub>k</sub>).</li>
<li>The solution set must not contain duplicate combinations.</li>
</ul>
<p></p>

<p>
For example, given candidate set <code>2,3,6,7</code> and target <code>7</code>, <br>
A solution set is: <br>
<code>[7]</code> <br>
<code>[2, 2, 3]</code> <br>
</p>
<p></p>
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
		<td bgcolor="yellow">20 min coding only</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an NP problem__. 

It can be solved with basic recursion methods. I refered to [this blog](http://blog.csdn.net/linhuanmars/article/details/20828631) for the idea. 

### Solution

__Recursively fetch the next element and subtract the value from the target__. In the end, if target happen to be 0, then 1 solution is found. If target result to be less than 0, return. If larger than 0, continue. 

### My code 


    public ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        Arrays.sort(candidates);
        helper(candidates, ans, 0, new ArrayList<Integer>(), target);
        return ans;
    }

    private void helper(int[] cand, ArrayList<ArrayList<Integer>> ans, 
                        int start, ArrayList<Integer> items, int target) {
        if (target < cand[start]) return;
        for (int i = start; i < cand.length; i ++) {
            if (cand[i] > target) break;
            items.add(cand[i]);
            if (cand[i] == target) ans.add(new ArrayList<Integer>(items));
            else helper(cand, ans, i, items, target - cand[i]);
            items.remove(items.size() - 1);
        }
    }


---
layout: post
title: "[LeetCode 40] Combination Sum II"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/combination-sum-ii/)

<div class="question-content">
            <p></p><p>
Given a collection of candidate numbers (<b><i>C</i></b>) and a target number (<b><i>T</i></b>), find all unique combinations in <b><i>C</i></b> where the candidate numbers sums to <b><i>T</i></b>.
</p>

<p>Each number in <b><i>C</i></b> may only be used <b>once</b> in the combination.
</p>
<p><b>Note:</b><br>
</p><ul>
<li>All numbers (including target) will be positive integers.</li>
<li>Elements in a combination (<i>a</i><sub>1</sub>, <i>a</i><sub>2</sub>, … , <i>a</i><sub>k</sub>) must be in non-descending order. (ie, <i>a</i><sub>1</sub> ≤ <i>a</i><sub>2</sub> ≤ … ≤ <i>a</i><sub>k</sub>).</li>
<li>The solution set must not contain duplicate combinations.</li>
</ul>
<p></p>

<p>
For example, given candidate set <code>10,1,2,7,6,1,5</code> and target <code>8</code>, <br>
A solution set is: <br>
<code>[1, 7]</code> <br>
<code>[1, 2, 5]</code> <br>
<code>[2, 6]</code> <br>
<code>[1, 1, 6]</code> <br>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This problem is derived from the "Combination Sum" problem__. 

The solution is the "Combination Sum" solution plus some duplication avoidance technique. 

### Solution

__Main part of this solution is same as "Combination Sum"__. There is only 2 lines of code that needs to be added/modified. 

__First change__, When go into the next recursive call, instead of: 

> helper(cand, ans, i, ... )

Change it to 

> helper(cand, ans, i + 1, ... )

__Second change__, inside the for-loop, instead of getting next element from array, get the next element with different value. The 2 types of modifications below both works: 

> At the beginning of the for-loop: if (i > start && cand\[i\] == cand\[i-1\]) continue;

> At the end of the for-loop: while(i < cand.length - 1 && cand\[i\] == cand\[i + 1\]) i++;

The 2 kinds of code are shown below. 

### My code 

This idea is from [this blog](http://fisherlei.blogspot.sg/2013/01/leetcode-combination-sum-ii-solution.html). This is also the most popular solution online. 


    public ArrayList<ArrayList<Integer>> combinationSum2(int[] num, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        Arrays.sort(num);
        helper(num, ans, 0, new ArrayList<Integer>(), target);
        return ans;
    }

    private void helper(int[] cand, ArrayList<ArrayList<Integer>> ans, 
                        int start, ArrayList<Integer> items, int target) {
        if (start >= cand.length || target < cand[start]) return;
        for (int i = start; i < cand.length; i ++) {
            if (cand[i] > target) break;
            items.add(cand[i]);
            if (cand[i] == target) ans.add(new ArrayList<Integer>(items));
            else helper(cand, ans, i + 1, items, target - cand[i]);
            items.remove(items.size() - 1);
            while(i < cand.length - 1 && cand[i] == cand[i + 1]) i++;
        }
    }


The idea from [this blog](http://blog.csdn.net/linhuanmars/article/details/20829099). Only difference is the way to remove duplications (no while-loop at the end, instead, a checking method at the beginning of the for-loop).


    public ArrayList<ArrayList<Integer>> combinationSum2(int[] num, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        Arrays.sort(num);
        helper(num, ans, 0, new ArrayList<Integer>(), target);
        return ans;
    }

    private void helper(int[] cand, ArrayList<ArrayList<Integer>> ans, 
                        int start, ArrayList<Integer> items, int target) {
        if (start >= cand.length || target < cand[start]) return;
        for (int i = start; i < cand.length; i ++) {
            if (i > start && cand[i] == cand[i-1]) continue;
            if (cand[i] > target) break;
            items.add(cand[i]);
            if (cand[i] == target) ans.add(new ArrayList<Integer>(items));
            else helper(cand, ans, i + 1, items, target - cand[i]);
            items.remove(items.size() - 1);
            // while(i < cand.length - 1 && cand[i] == cand[i + 1]) i++;
        }
    }


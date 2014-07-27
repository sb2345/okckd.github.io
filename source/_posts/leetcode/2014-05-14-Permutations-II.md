---
layout: post
title: "[LeetCode 47] Permutations II"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/permutations-ii/)

<div class="question-content">
            <p></p><p>
Given a collection of numbers that might contain duplicates, return all possible unique permutations.
</p>

<p>
For example,<br>
<code>[1,1,2]</code> have the following unique permutations:<br>
<code>[1,1,2]</code>, <code>[1,2,1]</code>, and <code>[2,1,1]</code>.
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
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is based on the solution for "Permutations"__. 

This question, together with "Permutations", is very classic and frequent questions during interview, and is the basis for many similar problems. __We must be able to write the solution in 1 go without even looking__. 

### Solution

The solution is simply the solution for "Permutations" __plus some duplication avoidance techniques__. This reminds me of the question - \[LeetCode 40\] Combination Sum II. 

__I solved this problem quickly by using previous "adding elements one by one" solution__. The idea is when getting element from remaining list and add to current list, check for duplication. If the number occured before, skip operation. (Don't forget sorting is required at first) This is just 2 line of code, and it works like magic. 

Solutions based on other "Permutations" solutions will be similar. __The main idea is to always find the next different value before proceed the recursion__. I will post another solution from [this blog](http://www.programcreek.com/2013/02/leetcode-permutations-ii-java/), which is based on the swapping element method. 

### My code 

__My code__, based on "adding elements one by one" solution from previous question.


    public ArrayList<ArrayList<Integer>> permuteUnique(int[] num) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> remain = new ArrayList<Integer>();
        Arrays.sort(num);
        for (Integer a: num)
            remain.add(a);
        helper(ans, new ArrayList<Integer>(), remain);
        return ans;
    }

    private void helper(ArrayList<ArrayList<Integer>> ans, 
            ArrayList<Integer> cur, ArrayList<Integer> remain) {
        int len = remain.size();
        if (len == 0) {
            ans.add(new ArrayList(cur));
            return;
        }
        for (int i = 0; i < len; i ++) {
            if (i != 0 && remain.get(i-1) == remain.get(i)) 
                continue;
            int t = remain.remove(i);
            cur.add(t);
            helper(ans, cur, remain);
            remain.add(i, t);
            cur.remove(cur.size() - 1);
        }
    }


__Another solution based on the swapping element method__


    public ArrayList<ArrayList<Integer>> permuteUnique(int[] num) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        permuteUnique(num, 0, result);
        return result;
    }

    private void permuteUnique(int[] num, int start, ArrayList<ArrayList<Integer>> result) {

        if (start >= num.length ) {
            ArrayList<Integer> item = convertArrayToList(num);
            result.add(item);
        }

        for (int j = start; j <= num.length-1; j++) {
            if (containsDuplicate(num, start, j)) {
                swap(num, start, j);
                permuteUnique(num, start + 1, result);
                swap(num, start, j);
            }
        }
    }

    private ArrayList<Integer> convertArrayToList(int[] num) {
        ArrayList<Integer> item = new ArrayList<Integer>();
        for (int h = 0; h < num.length; h++) {
            item.add(num[h]);
        }
        return item;
    }

    private boolean containsDuplicate(int[] arr, int start, int end) {
        for (int i = start; i <= end-1; i++) {
            if (arr[i] == arr[end]) {
                return false;
            }
        }
        return true;
    }

    private void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

__Updated on June 13th__. The way to remove duplicate is very difficult. The key points to keep in mind: 

1. Use another array to flag the 'visited' items
2. Check items with same value, and __ONLY USE THE FIRST INSTANCE OF THE SAME VALUE__. Which is to say, if current = previous, but previous is not visited, do not use current number. 

I post the new code written by me using template (actually same as first code)

    public List<List<Integer>> permuteUnique(int[] num) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (num == null || num.length == 0) {
            return ans;
        }
		Arrays.sort(num);
        helper(ans, new LinkedList<Integer>(), num, new boolean[num.length]);
        return ans;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num, boolean[] visited) {
        if (path.size() == num.length) {
            ans.add(new LinkedList<Integer>(path));
            return;
        }
        for (int i = 0; i < num.length; i++) {
            if (visited[i]) {
                continue;
            }
			if (i > 0 && !visited[i - 1] && num[i - 1] == num[i]) {
                continue;
            }
            path.add(num[i]);
			visited[i] = true;
            helper(ans, path, num, visited);
            path.remove(path.size() - 1);
			visited[i] = false;
        }
    }

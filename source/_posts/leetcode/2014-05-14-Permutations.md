---
layout: post
title: "[LeetCode 46] Permutations"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/permutations/)

<div class="question-content">
            <p></p><p>
Given a collection of numbers, return all possible permutations.
</p>

<p>
For example,<br>
<code>[1,2,3]</code> have the following permutations:<br>
<code>[1,2,3]</code>, <code>[1,3,2]</code>, <code>[2,1,3]</code>, <code>[2,3,1]</code>, <code>[3,1,2]</code>, and <code>[3,2,1]</code>.
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very classic question__. __The solution is very standard__. 

__One solution__ is to recursively push elements into a list, until all elements are pushed. __Another solution__ is using 2 nested for-loops to keep adding next elements. __There is one more solution__ which swaps each element with each element after it. 

__Keep in mind: this type of permutation questions always requires insert/delete before/after a recursion__! See code for details. 

I will explain 3 solutions one by one. 

### Solution

__First, double nested for-loop method__. This is a very standard way to write code and often seen in solutions. [This post](http://www.programcreek.com/2013/02/leetcode-permutations-java/) explains it very well: 

> Loop through the array, in each iteration, a new number is added to different locations of results of previous iteration. Start from an empty List.

__Second, swap element method__. It is also explained in [the same post](http://www.programcreek.com/2013/02/leetcode-permutations-java/). This is an very interesting idea which I never thought of. [Someone say](http://blog.csdn.net/u010500263/article/details/18178243) this solution relates to __N-Queens problem__. 

> Swap each element with each element after it

__Third solution, which is my solution - adding elements one by one__. I kept a current list and a remaining element list. Each time I get a new item from remaining list, and add it into current list. This solution is good, however __since remaining elements is array, it's hard to remove elements from it__. I simply convert the array into ArrayList. [Someone else's solution](http://blog.csdn.net/u010500263/article/details/18178243) would use another visited array to keep track of remainings. Both works fine. 

__That's all the solutions__! Look below for code. 

### My code 

__The double nested for-loop method__


    public ArrayList<ArrayList<Integer>> permute(int[] num) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

        //start from an empty list
        result.add(new ArrayList<Integer>());

        for (int i = 0; i < num.length; i++) {
            //list of list in current iteration of the array num
            ArrayList<ArrayList<Integer>> current = new ArrayList<ArrayList<Integer>>();

            for (ArrayList<Integer> l : result) {
                // # of locations to insert is largest index + 1
                for (int j = 0; j < l.size()+1; j++) {
                    // + add num[i] to different locations
                    l.add(j, num[i]);
                    ArrayList<Integer> temp = new ArrayList<Integer>(l);
                    current.add(temp);
                    l.remove(j);
                }
            }
            result = new ArrayList<ArrayList<Integer>>(current);
        }
        return result;
    }


__The swap element method__


    public ArrayList<ArrayList<Integer>> permute(int[] num) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        permute(num, 0, result);
        return result;
    }

    void permute(int[] num, int start, ArrayList<ArrayList<Integer>> result) {

        if (start >= num.length) {
            ArrayList<Integer> item = convertArrayToList(num);
            result.add(item);
        }

        for (int j = start; j <= num.length - 1; j++) {
            swap(num, start, j);
            permute(num, start + 1, result);
            swap(num, start, j);
        }
    }

    private ArrayList<Integer> convertArrayToList(int[] num) {
        ArrayList<Integer> item = new ArrayList<Integer>();
        for (int h = 0; h < num.length; h++) {
            item.add(num[h]);
        }
        return item;
    }

    private void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }


__Adding elements one by one__ (my code)


    public ArrayList<ArrayList<Integer>> permute(int[] num) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> remain = new ArrayList<Integer>();
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
            int t = remain.remove(i);
            cur.add(t);
            helper(ans, cur, remain);
            remain.add(i, t);
            cur.remove(cur.size() - 1);
        }
    }


__Adding elements one by one__ (other people's code). It's very similar. 


    public ArrayList<ArrayList<Integer>> permute(int[] num) {  
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();  
        ArrayList<Integer> element = new ArrayList<Integer>();  
        boolean[] visited = new boolean[num.length];  
        helper(num, result, element, visited);  
        return result;  
    }  

    public void helper(int[] num, ArrayList<ArrayList<Integer>> result, 
            ArrayList<Integer> element, boolean[] visited){  
        if (element.size() == num.length){  
            // duplicate element and add it to result 
            // (element would be changed from time to time. 
            // If directly use element  
            // only result would be changed when element changed)  
            result.add(new ArrayList<Integer>(element));   
            return;  
        }  

        for(int i=0; i<num.length; i++){  
            if(!visited[i]){  
                visited[i] = true;  
                element.add(num[i]);  
                helper(num, result, element, visited);  

                // After providing a complete permutation, pull out the last number
                element.remove(element.size()-1);  
                visited[i] = false;  
            }  
        }  
    }  


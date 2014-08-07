---
layout: post
title: "[LeetCode 42] Trapping Rain Water"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/trapping-rain-water/)

<div class="question-content">
            <p></p><p>
Given <i>n</i> non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining. 
</p>

<p>
For example, <br>
Given <code>[0,1,0,2,1,0,1,3,2,1,2,1]</code>, return <code>6</code>.
</p>

<p>
<img src="http://www.leetcode.com/wp-content/uploads/2012/08/rainwatertrap.png"><br>
</p><p style="font-size: 11px">The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. <b>Thanks Marcos</b> for contributing this image!</p><p></p>
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

__This is an interesting question__. 

I come up with a great solution, which is different from most online solutions. 

__My solution of using 2 iterations__. First, find the point of max height (m). Second, iterate from 0 to right side, until reach m, while filling in the trapped water. Third, iterate from last to left side, until reach m. 

__The most popular solution online is DP__. The explanation from [this blog](http://rleetcode.blogspot.sg/2014/03/trapping-rain-water-java-python.html) is slightly confusing, so I will explain it here. __Basic idea is to do 2 iteration__. First time get the heighest bound to the left of every point. Second time get the heighest bound to the right. 

> Example: input = \[0,1,0,2,1,0,1,3,2,1,2,1\]. 

> Assume the 2 DP arrays are called highestLeftSoFar and highestRightSoFar.

> highestLeftSoFar  = 0,1,1,2,2,2,2,3,3,3,3,3

> highestRightSoFar = 3,3,3,3,3,3,3,3,2,2,2,1

> For each point, get the lowest bound (of the 2 bounds), and calculate water. 

__There is another solution making use of stack__ from [this blog](http://n00tc0d3r.blogspot.sg/2013/06/trapping-rain-water.html). This idea is IMHO not very good, but it can be a good thinking/coding excercise. (I put the code in next section, but I did not write it)

> We kind of add up level by level, as shown in picture below.

{% img middle /assets/images/trapping_rain.png %}

1. Use Stack to store the index of a bar;
2. If the current one is smaller then the top of the stack, push it to stack;
3. Otherwise, pop up the top until stack is empty or top is greater than the current one, add up the volume, push the current one to stack.

> The tricky part is what is the volume to be added each time when we pop up a value from the stack.

### Solution

Coding part is easy. 

### My code 

My solution.


    public int trap(int[] A) {
        int len = A.length;
        if (len <= 2) return 0;
        int m = 0, left = 0, right = 0, sum = 0;
        for (int i = 0; i < len; i ++) if (A[m] < A[i]) m = i;
        // now m points to the max height of the entire array
        for (int i = 0; i < m; i ++) {
            sum += Math.max(0, left - A[i]);
            left = Math.max(left, A[i]);
        }
        for (int i = len - 1; i > m; i --) {
            sum += Math.max(0, right - A[i]);
            right = Math.max(right, A[i]);
        }
        return sum;
    }


DP solution.


    public int trap(int[] A) {
        if (A == null ||A.length == 0) return 0;
        int[] highestLeftSoFar = new int[A.length];
        int[] highestRightSoFar = new int[A.length];
        for (int i = 0; i < highestLeftSoFar.length; i ++)
            highestLeftSoFar[i] = i == 0 ? 
                A[i] : Math.max(A[i], highestLeftSoFar[i-1]);
        for (int i = A.length - 1; i >= 0; i --)
            highestRightSoFar[i] = i == A.length-1 ? 
                A[i] : Math.max(A[i], highestRightSoFar[i+1]);
        int totalVolume=0;
        for (int i = 0; i < A.length; i ++)
            totalVolume += Math.max(0, 
                Math.min(highestLeftSoFar[i], highestRightSoFar[i]) - A[i]);
        return totalVolume;
    }


Stack Solution.


    public int trap(int[] A) {
        int cur = 0;
        while (cur < A.length && A[cur] == 0) cur ++;
        int vol = 0;
        Stack<Integer> stack = new Stack<Integer>();
        while (cur < A.length) {
            while (!stack.isEmpty() && A[cur] >= A[stack.peek()]) {
                int b = stack.pop();
                if (stack.isEmpty()) break;
                vol += ((cur - stack.peek() - 1) * (Math.min(A[cur], A[stack.peek()]) - A[b]));
            }
            stack.push(cur ++);
            cur ++;
        }
        return vol;
    }

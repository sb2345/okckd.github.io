---
layout: post
title: "[LeetCode 31] Next Permutation"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/next-permutation/)

<div class="question-content">
            <p></p><p>
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
</p>
<p>
If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
</p>
<p>
The replacement must be in-place, do not allocate extra memory.
</p>
<p>
Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.<br>
<code>1,2,3</code> → <code>1,3,2</code><br>
<code>3,2,1</code> → <code>1,2,3</code><br>
<code>1,1,5</code> → <code>1,5,1</code><br>
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
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">half hour</td>
	</tr>
</table>

### Analysis

__There is only 1 popular solution on the Internet__, which is same as mine. 

The image below explains it very well (for the input number "687432").

{% img left /assets/images/next_permutation.png %}

### Solution

My first attempted code is a bit lenthy but works perfectly. 

Second time, I read [this blog](http://blog.csdn.net/havenoidea/article/details/12176737) and optimized my code. It's same solution, actually. 

### My code 

My first code. 


    public void nextPermutation(int[] num) {
        if (num.length < 2) return;
        // locate 2 pointers: m and n
        int m = num.length - 2;
        while (m >= 0 && num[m] >= num[m+1]) m --;
        if (m == -1) {
            Arrays.sort(num);
            return;
        }
        int n = num.length - 1;
        while (num[n] <= num[m]) n --;
        // now number pointer by m and n should be swopped
        num = swopNum(num, m, n);
        // then, head and tail swop from position (m+1) to the end
        int left = m + 1, right = num.length - 1;
        while (left < right)
            num = swopNum(num, left++, right--);
    }

    private int[] swopNum(int[] num, int a, int b) {
        num[a] = num[a] + num[b];
        num[b] = num[a] - num[b];
        num[a] = num[a] - num[b];
        return num;
    }


Second time code.


    public void nextPermutation(int[] num) {
        int len = num.length;
        if (len < 2) return;
        int posStartReverse = 0, last = len - 1;
        for (int i = len - 2; i >= 0; i --) {
            if (num[i] >= num[i+1]) continue;
            for (int j = len - 1; j > i; j --) 
                if (num[i] < num[j]) {
                    swapNum(num, i, j);
                    break;
                }
            posStartReverse = i + 1;
            break;
        }
        while (posStartReverse < last) swapNum(num, posStartReverse++, last--);
    }

    private int[] swapNum(int[] num, int a, int b) {
        num[a] = num[a] + num[b];
        num[b] = num[a] - num[b];
        num[a] = num[a] - num[b];
        return num;
    }

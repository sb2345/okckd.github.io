---
layout: post
title: "[Question] Knapsack Problem with Duplications"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/04/integer-knapsack-problem-duplicate.html)

> You have n types of items, where the ith item type has an integer size si and a real value vi. You need to ﬁll a knapsack of total capacity C with a selection of items of maximum value. You can add multiple items of the same type to the knapsack. 

> This is similar to "0-1 Knapsack Problem", but duplication is allowed for this question. 

### Analysis

Of course this is DP, and it's 1-D DP. However, __there is one very tricky special case__. 

### Solution

Using 'M(j)' to denote the max value for total weight j, 'w' to denote weight, and 'v' to denote value, the equation is: 

> M(j) = max{M(j − 1), max(i=1...n) M(j − wi) + vi}

__Note the 2 cases are__: 

1. when (j)th spot is not filled, the max value is __M(j-1)__
1. when (j)th spot is filled, the max value is __max(i=1...n) M(j − wi) + vi__

This question is trickier than "0-1 Knapsack Problem", if not more difficult. __Study the 2 question together__. 

### Code

__not written by me__ 

    int knapsack(int value[], int weight[], int n, int C, vector<int> backtrack) {
     int *M = new int[C+1];  
     int i, j, tmp, pos;  
     for(i=1; i<= C; i++) {  
         M[i] = M[i-1];  
         pos = i-1;               
         for(j=0; j< n; j++)  
         {  
             if (i >= weight[j])  
                 tmp = M[i-weight[j]] + value[j];  
             if (tmp > M[i]){  
                 M[i] = tmp;  
                 pos = i - weight[j];  
             }  
         }  
         backtrack.push_back(pos);  
     }   
     int ans = M[C];  
     delete[] M;        
     return ans;  
    }  

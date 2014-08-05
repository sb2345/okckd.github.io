---
layout: post
title: "[Question] 0-1 Knapsack Problem"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)

> Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value. 

> In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights. Also given an integer W which represents knapsack capacity, find out the maximum possible value. 

> You cannot break an item, either pick it or don’t pick it (0-1 property). 

### Analysis

This is a very similar question to "Coin Change", because directly using recursion to solve will result in a lot of re-calculations. It's a DP question. 

### Solution

Using i to denote the items to put into Knapsack, and w denote the total weight, the equation is: 

> K[i][w] = max(val[i-1] + K[i-1][w-wt[i-1]],  K[i-1][w]);

### Code

    int knapSack(int W, int wt[], int val[], int n) {
       int i, w;
       int K[n+1][W+1];

       // Build table K[][] in bottom up manner
       for (i = 0; i <= n; i++)
       {
           for (w = 0; w <= W; w++)
           {
               if (i==0 || w==0)
                   K[i][w] = 0;
               else if (wt[i-1] <= w)
                     K[i][w] = max(val[i-1] + K[i-1][w-wt[i-1]],  K[i-1][w]);
               else
                     K[i][w] = K[i-1][w];
           }
       }

       return K[n][W];
    }

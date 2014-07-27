---
layout: post
title: "[LeetCode Plus] Coins in a Line "
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---

### Question 

[link](http://leetcode.com/2011/02/coins-in-line.html)

> There are n coins in a line. Two players take turns to take a coin from one of the ends of the line until there are no more coins left. The player with the larger amount of money wins. Assume that you go first, describe an algorithm to compute the maximum amount of money you can win. 

### Analysis

__There's a guaranteed 'win strategy'__, if the input array is even size. Find the sum of coins at even and odd positions respectively. Then, make sure you always take coin from even (or odd, whichever sum is bigger) position. 

This strategy is clever and simple, but __DOES NOT maximize your total sum__. 

### Solution

__The optimized solution is to use [2-D DP](http://tech-queries.blogspot.sg/2011/06/get-maximum-sum-from-coins-in-line.html)__. Now we have array A and C(i, j) which is the maximum sum possible when remaining coins are from i to j. 

You can take either i or j. Since the opponent is as smart as you, he would have chosen the choice that yields the minimum amount to you. 

So, the final equation is: 

> C(i, j) = max { Ai + min{C(i+2, j), C(i+1, j-1)}, Aj + min{C(i+1, j-1), C(i, j-2)} }

### Code

C++ code

    #define MAX 100  
    int maxMoney(int A[], int N) {
        int C[MAX][MAX] = {0};  
        int x, y, z; //x = C[m+2][n], y = C[m+1][n-1], z = C[m][n-2]  
        for (int i = 0; i < N; i++) {
            for (int m = 0, n = i; n < N; m++, n++) {
              //calculate x, y, z  
              x = (m+2 < N)                         ? C[m+2][n] : 0;  
              y = (m+1 < N && n-1 >= 0)    ? C[m+1][n-1] : 0;  
              z = (n-1 > 0)                            ? C[m][n-2] : 0;  
              C[m][n] = max(A[m] + min(x,y),  
                                     A[n] + min(y,z));  
              //For Debugging        
              cout << x << ", " << y << ", " << z << endl;  
              cout << m << ", " << n << ", " << C[m][n] << endl;  
            }
        }
        return C[0][N-1];
    }

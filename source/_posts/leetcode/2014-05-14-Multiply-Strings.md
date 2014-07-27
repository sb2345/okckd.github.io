---
layout: post
title: "[LeetCode 43] Multiply Strings"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/multiply-strings/)

<div class="question-content">
            <p></p><p>Given two numbers represented as strings, return multiplication of the numbers as a string.</p>

<p>Note: The numbers can be arbitrarily large and are non-negative.</p><p></p>
          </div>
### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="red">40min coding only</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is easy, but difficult for me__ at first. 

The basic idea is to __multiple numbers 1 by 1, and do decimal carry later__. Note the max length of result is (m+n) assuming 2 input are length m and n respectively. 

The implementation seems easy, but how to __convert the result array into string__ takes me an extremely long time. Most online solutions use __StringBuilder__. I later figured out a way to simply use a char array. Performance is same. 

### Solution

First solution is written by me using the idea from [this blog](http://blog.csdn.net/fightforyourdream/article/details/17370495), __using char array for result__. 

Second code is the code by the author, making use of __StringBuilder__. 

### My code 


    public String multiply(String num1, String num2) {
        char[] a = num1.toCharArray();
        char[] b = num2.toCharArray();
        int len1 = a.length, len2 = b.length, len3 = len1 + len2;
        if (len1 == 0 || len2 == 0) return "0";
        int[] sum = new int[len3];
        // now do multiply one by one, and put into sum array
        for (int i = 0; i < len1; i ++) 
            for (int j = 0; j < len2; j ++) 
                sum[i+j+1] += (a[i]-'0') * (b[j]-'0');
        // now carry the digits to the previous position, and keep the remainder
        for (int i = len3 - 1; i > 0; i --) {
            sum[i-1] += sum[i] / 10;
            sum[i] = sum[i] % 10;
        }
        // now print result into String
        int k = 0;
        while (k < len3 && sum[k] == 0) k ++;
        if (k == len3) return "0";
        char[] ans = new char[len3 - k];
        for (int i = k; i < len3; i ++)
            ans[i-k] = (char) (sum[i] + '0');
        return new String(ans);
    }


Everything is same except the change from char array to StringBuilder.


    public String multiply(String num1, String num2) {  
        String n1 = new StringBuilder(num1).reverse().toString();  
        String n2 = new StringBuilder(num2).reverse().toString();  

        int[] d = new int[n1.length()+n2.length()];     
        for(int i=0; i<n1.length(); i++){  
            for(int j=0; j<n2.length(); j++){  
                d[i+j] += (n1.charAt(i)-'0') * (n2.charAt(j)-'0');     
            }  
        }  

        StringBuilder sb = new StringBuilder();  
        for(int i=0; i<d.length; i++){  
            int digit = d[i]%10;      
            int carry = d[i]/10;     
            if(i+1<d.length){  
                d[i+1] += carry;  
            }  
            sb.insert(0, digit);        // prepend  
        }  

        while(sb.charAt(0)=='0' && sb.length()>1){  
            sb.deleteCharAt(0);  
        }  
        return sb.toString();  
    }  


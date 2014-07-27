---
layout: post
title: "[LeetCode 13] Roman to Integer"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/roman-to-integer/)

<div class="question-content">
            <p></p><p>Given a roman numeral, convert it to an integer.</p>

<p>Input is guaranteed to be within the range from 1 to 3999.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is easier than "Integer to Roman".

__This question is easy, but writing code is not very very easy__. The main idea is to always read 2 char and check. If pre > cur, then OK. If pre < cur, we need to subtract (2 * pre) from the result. 

The rest is fine. 

### Solution

The code explains itself. 

### My code 

    public int romanToInt(String s) {
        int pre = 0;
        int cur = 0;
        int sum = 0;
        if (s.equals("")) return 0;
        for (char t: s.toCharArray()){
            cur = getNum(t);
            if (pre != 0 && pre < cur){
                sum += cur - (2 * pre);
                pre = 0;
            } else {
                sum += cur;
                pre = cur;
            }
        }
        return sum;
    }
    
    private int getNum(char a){
        switch(a){
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
        }
        return 0;
    }


This is another [very interesting solution](http://yucoding.blogspot.sg/2013/05/leetcode-question-87-roman-to-interger.html) from online. __It basically just use addition, and solve the problem perfectly!__ (The code is C++)

    class Solution {
    public:
        int romanToInt(string s) {
            // 4:IV, 9:IX, 40:XL, 90:XC, 400:CD, 900:CM,
            // 1:I, 10:X, 100:C, 1000:M
            int res=0;
            char pre = ' ';
            for(int i=0;i<s.size();i++){
                if (s[i]=='M' && pre!='C') {res+=1000;}
                if (s[i]=='C' && pre!='X') {res+=100;}
                if (s[i]=='X' && pre!='I') {res+=10;}

                if (s[i]=='M' && pre=='C') {res+=800;}
                if (s[i]=='C' && pre=='X') {res+=80;}
                if (s[i]=='X' && pre=='I') {res+=8;}

                if (s[i]=='I' ) {res+=1;}

                if (s[i]=='V' && pre!='I'){res+=5;}
                if (s[i]=='L' && pre!='X'){res+=50;}
                if (s[i]=='D' && pre!='C'){res+=500;}

                if (s[i]=='V' && pre=='I'){res+=3;}
                if (s[i]=='L' && pre=='X'){res+=30;}
                if (s[i]=='D' && pre=='C'){res+=300;}

                pre = s[i];
            }
            return res;
        }
    };
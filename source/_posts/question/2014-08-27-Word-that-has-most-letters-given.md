---
layout: post
title: "[Question] Find word that has the most letters given "
comments: true
category: Question
tags: [  ]
---

### Question

[link](http://programmers.stackexchange.com/questions/188687/try-to-find-a-word-in-the-dictionary-that-has-most-letters-given)

> Given some random letters, for example "a,e,o,g,z,k,l,j,w,n" and a dictionary. 

> Try to find a word in the dictionary that has most letters given. 

> Example: "abbee" -> 3 occurance. 

### Solution

1. Make an array that marks all given chars. Like this:

    index={a:1, b:0, c:0, d:0, e:1, f:0, g:1...}

1. Iterate over each word of dictionary. 

    The array gives an easy way to search a char's existance. I did not write code for this question. 

### Code

    max=0;
    max_index=0;
    
    foreach(dictionary as position=>word) {
        sum=0;
        foreach(word as letter)
        {
          sum += index[letter];
        }
        if(sum > max)
        {
            max = sum;
            max_index = position;
        }
    }

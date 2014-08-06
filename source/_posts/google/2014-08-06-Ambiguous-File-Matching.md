---
layout: post
title: "[Google] Ambiguous File Matching"
comments: true
category: Google
tags: [  ]
---

### Question 

[link](http://www.careercup.com/question?id=5678301561487360)

> Given 10 files (text files) each of size of 900 Mb. 

> Given another file named "hello". match the contents of this file with other 10 file and return the file whose contents closely match with the contents of file "hello". 

### Solution

The solution given on the site is not adequate, but I have to choose one that make a little sense. 

> Score each file's contents on several parameters: 
> 
> 1. no. of words 
> 2. no. of letters 
> 3. no. of spaces 
> 4. count of each of the letters 
> 5. count of each words 

> Give weightage to each of the properties and arrive at a number (score). The closest of the scores is the answer.

I think maybe can use [Counting Bloom Filter](http://en.wikipedia.org/wiki/Bloom_filter#Counting_filters), although bloom filter does not record word sequences. 

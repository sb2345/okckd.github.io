---
layout: post
title: "[Design] Big Data - Top k Frequency 2"
comments: true
categories:
- Design
- Top K
tags: [  ]
---

### Question 

[link](http://blog.csdn.net/v_july_v/article/details/7382693)

> 一个文本文件，大约有一万行，每行一个词，要求统计出其中最频繁出现的前10个词，请给出思想，给出时间复杂度分析。

### Analysis

__The basic solution for 'Top K' questions__ is 【分治+trie树/hash+小顶堆】. 

In the previous post [Big Data - Top k Frequency]({% post_url /design/2014-07-25-big-data-Top-k-frequency %}), we used HashMap for calculating query frequency. Now we __use Trie to do it__. 

> 这题是考虑时间效率。用trie树统计每个词出现的次数，时间复杂度是O(n x le)（le表示单词的平准长度）。然后是找出出现最频繁的前10个词，可以用堆来实现，前面的题中已经讲到了，时间复杂度是O(n x lg10)。所以总的时间复杂度，是O(n x le)与O(n x lg10)中较大的哪一个。

#### How to use Trie to calculate word frequency? 

在Trie的node节点中[添加count域后](http://blog.csdn.net/ohmygirl/article/details/7953814)，可以统计单词出现的次数。统计的方法就是在插入单词的时候，令相应的count域加1（初始化为0）. 

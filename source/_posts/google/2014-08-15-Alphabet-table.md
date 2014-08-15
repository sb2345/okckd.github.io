---
layout: post
title: "[Google] Alphabet Table (`)"
comments: true
category: Google
tags: [  ]
---

### Question 

[link](http://blog.sina.com.cn/s/blog_979956cc0101i67x.html)

> 每一种语言，都有自己的字母表，类似英文的a-z，但是顺序不相同。例如，有的语言可能是z是第一个之类的。现在给定这个语言的字典，请分析这个字典，得到这个语言的字母表的顺序。 

> 例如：有如下的字母：C CAC CB BCC BA。 经过分析，得到字母表为C->A->B。

### Solution

http://page.renren.com/601882592/channel-noteshow-927705419

1. C 2. CAC 3. CB 4. BCC 5. BA 经过分析，得到字母表为C->A->B。 分析 字典序相邻的位置的字符串，只会有如下两种情况： （1）排在前面的字符串是下一个串的子串，如C与CAC （2）两个字符串具有第一对不相同的字符对，如CAC和CBB，第一个不相同的字符对为（A，B），这是就要求A在字母表中的顺序在B前面。对于后面字符并没有要求，如并不要求第二个不相同的字符对（C，B）中的C在字母表中的顺序在B前面。 所以按照第（2）种情况建图，然后对该有向无环图求拓扑排序即可。 


### Code


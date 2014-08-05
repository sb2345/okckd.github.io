---
layout: post
title: "[Design] MapReduce"
comments: true
category: Design
tags: [  ]
---

### An Overview

__[MapReduce](http://searchcloudcomputing.techtarget.com/definition/MapReduce) is a software framework__, or a __[distributed programming model](http://www.theserverside.com/news/1321219/Why-Should-You-Care-About-MapReduce)__ intended for processing massive amounts of data in large clusters. 

Google uses MapReduce for __indexing every Web page__ they crawl

1. __Map__, a function that parcels out work to different nodes in the distributed cluster.

1. __Reduce__, another function that collates the work and resolves the results into a single value.

### 

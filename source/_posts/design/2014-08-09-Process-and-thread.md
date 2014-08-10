---
layout: post
title: "[Design] Process VS. Thread"
comments: true
category: Design
tags: [  ]
---

### First difference

__[A process](http://www.programmerinterview.com/index.php/operating-systems/thread-vs-process/) can contain multiple threads__. When you open Microsoft Word, you start __a process__ that runs Word. The OS creates a process and begins executing the __primary thread__ of that process. 

Since a process can consist of multiple threads, a thread could be considered __a ‘lightweight’ process__. 

### Second difference

Another difference is that __threads__ within the same process __share the same address space__, whereas different __processes__ do not. 

This allows threads to read from and write to the same data structures and variables, and also __facilitates communication between threads__. Communication between processes – also known as IPC, or __inter-process communication__ – is quite difficult and resource-intensive.

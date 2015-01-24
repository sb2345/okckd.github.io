---
layout: post
title: "[Design] Process VS. Thread "
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

### One more thing

We already know that all thread under same process share same address space. __Let's talk a little about Stack and Heap in RAM__. 

Each thread gets __its own Stack__, while sharing __the same Heap__. Stack size is fixed. Stack is reclaimed when thread ends. 

Heap allocation is customized by __heap allocator__. There's no rules. Heap size can be expanded, if approved by the OS. 

As Heap holds global resources, it must be __thread-safe__, thus making it very complex to manage. For more, refer to __[Design] Stack and Heap__. 

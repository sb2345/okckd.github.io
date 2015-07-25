---
layout: post
title: "[Design] Process VS. Thread "
comments: true
category: Design

---

## First difference: inclusion

__[A process](http://www.programmerinterview.com/index.php/operating-systems/thread-vs-process/) can contain multiple threads__. When you open Microsoft Word, you start a process that runs Word. The OS creates a process and begins executing the __primary thread__ of that process. 

## Second difference: address space

__Threads within the same process share the same address space__, whereas different processes do not. 

__This facilitates communication between threads__, allows threads to read from and write to the same data structures and variables. 

Communication between processes – also known as IPC, or __inter-process communication__ – is quite difficult and resource-intensive.

### behind the scene: System stack and heap

Each thread gets __its own Stack, while sharing the same Heap__. Stack size is fixed. Stack is reclaimed when thread ends. 

Heap allocation is customized by __heap allocator__. There's no rules. Heap size can be expanded, if approved by the OS. As Heap holds global resources, it must be __thread-safe__, thus making it very complex to manage. 

For more, refer to __[Design] Stack and Heap__. 

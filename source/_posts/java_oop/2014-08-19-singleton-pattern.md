---
layout: post
title: "[Java OOP] Singleton Pattern "
comments: true
category: Java OOP
tags: [  ]
---

### Singleton Pattern

__Singleton__ design pattern is one of the __2 most frequent topics__ for OOD. 

__[Singleton pattern](http://en.wikipedia.org/wiki/Singleton_pattern)__ is a design pattern that restricts the instantiation of a class to one object. 

#### in Java

Since Java 5.0, the easiest way to create a Singleton is the __[enum type approach](http://en.wikipedia.org/wiki/Singleton_pattern#The_Enum_way)__. Here the code is not given. 

We will instead cover a very popular implementation: __[Lazy initialization](http://en.wikipedia.org/wiki/Singleton_pattern#Lazy_initialization)__. 

    public class SingletonDemo {
        private static volatile SingletonDemo instance = null;
        private SingletonDemo() { }
        public static SingletonDemo getInstance() {
            if (instance == null) {
                synchronized (SingletonDemo.class) {
                    if (instance == null) {
                        instance = new SingletonDemo();
                    }
                }
            }
            return instance;
        }
    }

An alternate simpler version (non-sync):

    public class SingletonDemo {
        private static SingletonDemo instance = null;
        private SingletonDemo() { }
        public static synchronized SingletonDemo getInstance() {
            if (instance == null) {
                instance = new SingletonDemo();
            }
            return instance;
        }
    }

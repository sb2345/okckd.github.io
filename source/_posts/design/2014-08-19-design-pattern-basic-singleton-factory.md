---
layout: post
title: "[Design] Design Pattern - Singleton & Factory"
comments: true
category: Design
tags: [  ]
---

### First Word

__Singleton__ and __Factory Method__ design pattern are the __2 most frequent topics__ for OOD. 

### Singleton Pattern

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

### Factory Method Pattern

__[Factory method pattern](http://en.wikipedia.org/wiki/Factory_method_pattern)__ is a creational pattern which uses __factory methods__ to deal with the problem of creating objects without specifying the exact class of object that will be created. 

This is done by creating objects via factory method, either:

1. specified in an interface/abstract class and implemente (differently)
1. implemented in a base class, and be overridden in derived classes

#### in Java

A normal [Maze Game](http://en.wikipedia.org/wiki/Factory_method_pattern#Java):

    public class MazeGame {
        public MazeGame() {
            Room room1 = makeRoom();
            Room room2 = makeRoom();
            room1.connect(room2);
            this.addRoom(room1);
            this.addRoom(room2);
        }

        protected Room makeRoom() {
            return new OrdinaryRoom();
        }
    }

A magic game:

    public class MagicMazeGame extends MazeGame {
        @Override
        protected Room makeRoom() {
            return new MagicRoom();
        }
    }

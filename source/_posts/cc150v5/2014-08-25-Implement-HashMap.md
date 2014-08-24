---
layout: post
title: "[CC150v5] 8.10 Implement a hashmap (`)"
comments: true
category: CC150v5
tags: [  ]
---

### Question

> Design and implement a hash table which uses chaining (linked lists) to handle collisions.

### Solution

I wrote this topic before (using Java source code as a reference). This time, I would like to take another (easier) approach. 

The main part of this is to use an array of list structure like this: 

	LinkedList<Cell<K, V>>[] items;

And the Cell Class looks like this: 

    public class Cell<K, V> {
        private K key;
        private V value;

        public Cell(K k, V v) {
            key = k;
            value = v;
        }

        public boolean equivalent(Cell<K, V> c) {
            return equivalent(c.getKey());
        }

        public boolean equivalent(K k) {
            return key.equals(k);
        }

        public K getKey() {
            return key;
        }

        public V getValue() {
            return value;
        }
    }

### Code

undone

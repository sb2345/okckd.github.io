---
layout: post
title: "[CC150v5] 11.8 Get Rank in Stream of Integers "
comments: true
category: CC150v5
tags: [  ]
---

### Question

> Imagine you are reading in a stream of integers. Periodically, you wish to be able to look up the rank of a number x (the number of values less than or equal to x). 

> Implement the data structures and algorithms to support these operations. That is, implement the method __track(int x)__, which is called when each number is generated, and the method __getRankOfNumber(int x)__, which returns the number of values less than or equal to x (not including x itself). 

### Solution

__This question requires a special type of Data Structure__. It basically is a modified BST like this: 

> The tree node stores both number value and the __count of node on left subtree__

{% img middle /assets/images/get-rank-number-stream.png %}

Suppose we want to find the rank of 24 in the tree above. We would compare 24 with the root, 20, and find that 24 must reside on the right. The root has 4 nodes in its left subtree, and when we include the root itself, this gives us five total nodes smaller than 24. We set counter to 5.

Then, we compare 24 with node 25 and find that 24 must be on the left. The value of counter does not update, since we're not "passing over" any smaller nodes. The value of counter is still 5. 

Next, we compare 24 with node 23,and find that 24 must be on the right. Counter gets incremented by just 1 (to 6), since 23 has no left nodes.

Finally, we find 24 and we return counter: 6.

### Code

I did not write code myself. It's too complex! 

__RankNode.java__

    public class RankNode {
        public int left_size = 0;
        public RankNode left;
        public RankNode right;
        public int data = 0;
        public RankNode(int d) {
            data = d;
        }

        public void insert(int d) {
            if (d <= data) {
                if (left != null) {
                    left.insert(d);
                } else {
                    left = new RankNode(d);
                }
                left_size++;
            } else {
                if (right != null) {
                    right.insert(d);
                } else {
                    right = new RankNode(d);
                }
            }
        }

        public int getRank(int d) {
            if (d == data) {
                return left_size;
            } else if (d < data) {
                if (left == null) {
                    return -1;
                } else {
                    return left.getRank(d);
                }
            } else {
                int right_rank = right == null ? -1 : right.getRank(d);
                if (right_rank == -1) {
                    return -1;
                } else {
                    return left_size + 1 + right_rank;
                }
            }
        }
    }

__Main Class__: 

    public class Question {
        private static RankNode root = null;

        public static void track(int number) {
            if (root == null) {
                root = new RankNode(number);
            } else {
                root.insert(number);
            }
        }

        public static int getRankOfNumber(int number) {
            return root.getRank(number);
        }

        public static void main(String[] args) {
            int size = 100;
            int[] list = AssortedMethods.randomArray(size, -100, 100);
            for (int i = 0; i < list.length; i++) {
                track(list[i]);
            }

            int[] tracker = new int[size];
            for (int i = 0; i < list.length; i++) {
                int v = list[i];
                int rank1 = root.getRank(list[i]);
                tracker[rank1] = v;
            }

            for (int i = 0; i < tracker.length - 1; i++) {
                if (tracker[i] != 0 && tracker[i + 1] != 0) {
                    if (tracker[i] > tracker[i + 1]) {
                        System.out.println("ERROR at " + i);
                    }
                }
            }

            System.out.println("Array: " + AssortedMethods.arrayToString(list));
            System.out.println("Ranks: " + AssortedMethods.arrayToString(tracker));
        }

    }

---
layout: post
title: "[LeetCode Plus] Lowest Common Ancestor of a Binary Tree Part I"
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---


### Question 

[link](http://leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-tree-part-i.html)

<div class="entry bg-color bg-img font-color">
    <blockquote>
        <p class="font-color bg-color bg-img">Given a binary tree, find the lowest common ancestor of two given nodes in the tree.</p>
    </blockquote>
    <p class="font-color bg-color bg-img"><span id="more-790" class="font-color"></span>
        <br>
    </p><pre class="bg-color bg-img font-color">        _______<span style="color: #990000;" class="font-color">3</span>______
       /              \
    ___<span style="color: #990000;" class="font-color">5</span>__          ___<span style="color: #990000;" class="font-color">1</span>__
   /      \        /      \
   <span style="color: #990000;" class="font-color">6</span>      _<span style="color: #990000;" class="font-color">2       0       8</span>
         /  \
         <span style="color: #990000;" class="font-color">7   4</span></pre>
    <p class="font-color">If you are not so sure about the definition of lowest common ancestor (LCA), please refer to my previous post: <a href="http://www.leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-search-tree.html" class="font-color bg-color bg-img">Lowest Common Ancestor of a Binary Search Tree (BST)</a> or the definition of LCA <a href="http://en.wikipedia.org/wiki/Lowest_common_ancestor" class="font-color">here</a>. Using the tree above as an example, the LCA of nodes <strong><span style="color: #990000;" class="font-color">5</span></strong> and <strong><span style="color: #990000;" class="font-color">1</span></strong> is <strong><span style="color: #990000;" class="font-color">3</span></strong>. Please note that LCA for nodes <strong><span style="color: #990000;" class="font-color">5</span> </strong>and <strong><span style="color: #990000;" class="font-color">4</span> </strong>is <strong><span style="color: #990000;" class="font-color">5</span></strong>.</p>
    <p class="font-color bg-color bg-img"><strong>Hint:</strong>
        <br>Top-down or bottom-up? Consider both approaches and see which one is more efficient.</p>
</div>

### Analysis 

This tree is not BST, so it's more difficult then previous. Top-down approach would take O(n^2) time due to duplicate traverse. 

__However, there is a very good bottom-up approach with O(n) time__. This solution, though tricky, is the most standard and common interview question that can be asked about Binary Tree. 

> We traverse from the bottom, and once we reach a node which matches one of the two nodes, we pass it up to its parent. The parent would then test its left and right subtree if each contain one of the two nodes. If yes, then the parent must be the LCA and we pass its parent up to the root. If not, we pass the lower node which contains either one of the two nodes (if the left or right subtree contains either p or q), or NULL (if both the left and right subtree does not contain either p or q) up.

The coding is much easier than coming up with this idea. 

<blockquote cite="http://leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-tree-part-i.html">
<p class="font-color"><strong>Notes:<br> </strong>The LCA problem had been studied extensively by many computer scientists. There exists efficient algorithms for finding LCA in constant time after initial processing of the tree in linear time. For the adventurous reader, please read this article for more details: <a href="http://www.topcoder.com/tc?module=Static&amp;d1=tutorials&amp;d2=lowestCommonAncestor" class="font-color">Range Minimum Query and Lowest Common Ancestor in Topcoder</a>.
</p>
</blockquote>

### Code

Assuming root node is given. C++ code from leetcode.com.

    Node *LCA(Node *root, Node *p, Node *q) {
      if (!root) return NULL;
      if (root == p || root == q) return root;
      Node *L = LCA(root->left, p, q);
      Node *R = LCA(root->right, p, q);
      if (L && R) return root;  // if p and q are on both sides
      return L ? L : R;  // either one of p,q is on one side OR p,q is not in L&R subtrees
    }

Assuming parent node is not given. This Java code is from [ninechap](http://answer.ninechapter.com/solutions/lowest-common-ancestor/) (The first method getRoot() is used to get root node). 

    private TreeNode getRoot(node) {
        while (node.parent != null) {
            node = node.parent;
        }
        return node;
    }
    
    private TreeNode getAncestor(TreeNode root, TreeNode node1, TreeNode node2) {
        if (root == null || root == node1 || root == node2) {
            return root;
        }
        
        // Divide
        TreeNode left = getAncestor(root.left, node1, node2);
        TreeNode right = getAncestor(root.right, node1, node2);
        
        // Conquer
        if (left != null && right != null) {
            return root;
        } 
        if (left != null) {
            return left;
        }
        if (right != null) {
            return right;
        }
        return null;
    }
    
    public TreeNode latestCommonAncestor(TreeNode node1, TreeNode node2) {
        if (node1 == null || node2 == null) {
            return null;
        }
        TreeNode root = getRoot(node1);
        return getAncestor(root, node1, node2);
    }

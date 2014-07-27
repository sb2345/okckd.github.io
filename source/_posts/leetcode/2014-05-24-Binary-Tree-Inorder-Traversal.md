---
layout: post
title: "[LeetCode 94] Binary Tree Inorder Traversal"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-inorder-traversal/)

<div class="question-content">
            <p></p><p>Given a binary tree, return the <i>inorder</i> traversal of its nodes' values.</p>

<p>
For example:<br>
Given binary tree <code>{1,#,2,3}</code>,<br>
</p><pre>   1
    \
     2
    /
   3
</pre>
<p></p>
<p>
return <code>[1,3,2]</code>.
</p>

<p><b>Note:</b> Recursive solution is trivial, could you do it iteratively?</p>

<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a classic AND EXTREMELY IMPORTANT question__. I solved it at first attempt, but forget about it and couldn't solve on 2nd time. 

About DFS, it is always implemented with a stack, no matter recursion is used or not. See [here](http://leetcode.com/2010/09/printing-binary-tree-in-level-order.html) 

> DFS uses a data structure called Stack and is commonly implemented using recursion (since function calls are pushed and popped off the memory stack). If recursion is not allowed, we can simulate the recursion by using iterative method with the help of stack. 

__A not-very-intuitive solution is Morris Traversal__. The idea behind this is [Threaded binary tree](http://en.wikipedia.org/wiki/Threaded_binary_tree). I don't like this method, so I will skip. 

The idea written below (2nd code) is very interesting, and was never seen before. Should keep it in mind. 

### Solution

__The most classic and standard solution for this question__ is explained well in [this blog](http://leetcode.com/2010/04/binary-search-tree-in-order-traversal.html). 

> First, the current pointer is initialized to the root. Keep traversing to its left child while pushing visited nodes onto the stack. When you reach a NULL node (ie, you've reached a leaf node), you would pop off an element from the stack and set it to current. Now is the time to print current's value. Then, current is set to its right child and repeat the process again. When the stack is empty, this means you're done printing.

### Code

__First, my previous code, very good solution__.

    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stk = new Stack<TreeNode>();
        stk.push(root);
        ArrayList<Integer> ls = new ArrayList<Integer>();
        
        if(root == null)
            return ls;
        while(stk.size() > 0){
            TreeNode cur = stk.peek();
            if (cur == null){
                stk.pop();
                if (stk.size() == 0) return ls;
                TreeNode temp = stk.pop(); 
                ls.add(temp.val);
                stk.push(temp.right);
                // why do I need a temp variable at this step?
                // this isn't good enough, change it in the future
            } else if (cur.left != null){
                stk.push(cur.left);
            } else {
                ls.add(cur.val);
                stk.pop();
                stk.push(cur.right);
            }
        }
        return ls;
    }
    // Program Logic:
    // If cur is null
    //    Remove cur
    //    Print next stack node
    //    Push next stack node's right
    // Else if cur got left
    //    Push cur.left
    // Else if cur not got left
    //    Print cur
    //    Remove cur
    //    Push cur.right
    // End if

__Second, standard solution, which is a simplified version of above code__

    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        while (p != null || ! stack.isEmpty()) {
            if (p != null) {
                stack.push(p);
                p = p.left;
            }
            else if (! stack.isEmpty()) {
                TreeNode temp = stack.pop();
                ans.add(temp.val);
                p = temp.right;
            }
        }
        return ans;
    }

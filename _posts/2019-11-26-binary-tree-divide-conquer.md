---
layout:     post
title:      "Bianry Tree and Divide & Conquer Problems"
subtitle:   "二叉树，分治法和题目总结"
date:       2019-11-26
author:     "Eryn"
tags:
    - Leetcode
    - Binary Tree
    - Divide & Conquer
    - Algorithm
    - Data Structure
---


## Binary Tree Divide & Conquer
-----------------------

### ### Closest Binary Search Tree Value
### Vertical Order Traversal of a Binary Tree
### Minimum Subtree
### Binary Tree Paths
### Flatten Binary Tree to Linked List
### Balanced Binary Tree
### Kth Smallest Element in a BST
### Lowest Common Ancestor III
### Validate Binary Search Tree
### Closest Binary Search Tree Value II
### Binary Search Tree Iterator


### Find tree value(在binary tree中search a value)
**Bottom-up 必背代码     
```java
public boolean findTarget(TreeNode root, int target) {
    if (root == null) return false;
    if (root.val == target) return true;
    boolean left = findTarget(root.left, target);
    boolean right = findTarget(root.right, target);
    return left || right;
}
```

### Maximum Average Subtree
**在java里面如果想同时返回多个值，唯一的办法是用一个自己创建的object(e.g. Pair)**

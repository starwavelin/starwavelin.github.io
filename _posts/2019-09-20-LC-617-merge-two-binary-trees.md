---
layout:     post
title:      "LeetCode 617. Merge Two Binary Trees"
subtitle:   "LeetCode 617. 合并两个二叉树"
date:       2019-09-21
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
本公众号上两篇发了《硅谷的中国人为什么目前逊色于印度人》《EB2/3绿卡申请者反对S.386提案方法汇总》，我们希望我们的国人同胞在美国能有好的出路与发展。  
那今天，我们就再回到软件工程师的基本功，做一道二叉树的题：合并两个二叉树。

解题“七步走” (保持这种sense)：  
1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thinking Process (What data structure, algorithm?)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

### 题目要求
[原题链接](https://leetcode.com/problems/merge-two-binary-trees/)  
有两棵节点为整数数字组成的二叉树，现在要合并它们。在合并的过程中，如果树1和树2的对应节点都不为空，则合并后的树的对应节点为树1和树2的对应节点的值的和；如果其中仅某一棵树的节点为空，则合并后的树的对应节点为非空的那棵树的节点；如果两棵树的对应节点均为空，则合并后的树在那个节点也是空。

### 举例与输入输出
例子直接用LeetCode上的图，还是很好理解的。

![oh-my-zsh](/img/in-post/20190921-lc-617-merge-two-binary-trees/lc617.png)

### 思路: 与什么题目很像
首先，根据我们先前做过的二叉树题目，凡此类问题大多用递归方法。  
想想，本题是要我们构建一个新的二叉树，那建树是从什么地方开始呢，直观的做法是从树的全局的根开始，逐步的往下建造。因此，本题和[二叉树的前序遍历](http://starwavelin.com/2019/07/28/LC-144-binary-tree-preorder-traversal/)比较接近，可以按照“根左右”的顺序通过已有的两棵树逐步构建新的合并后的树。  

### 代码
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        // Base Cases
        if (t1 == null) {
            return t2;
        }
        else if (t2 == null) {
            return t1;
        }

        // 构建新树的全局的根
        TreeNode root = new TreeNode(t1.val + t2.val);

        // Divide
        root.left = mergeTrees(t1.left, t2.left);
        root.right = mergeTrees(t1.right, t2.right);

        // Conquer
        return root;
    }
}
```

### 时间空间复杂度
我们把树t1的总结点数记做`m`，树t2的总结点数记做`n`。那么，  
时间复杂度：由于合并后的树的总结点数为先前两个数结点多的哪一个，所以是`O(max(m, n))`。  
空间复杂度：为递归栈的深度，也就是两棵树中更高的那棵树的高度，所以是`O(log(max(m, n)))`。

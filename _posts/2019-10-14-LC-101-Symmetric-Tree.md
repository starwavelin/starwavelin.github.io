---
layout:     post
title:      "LeetCode 101. Symmetric Tree"
subtitle:   "LeetCode 101. 对称二叉树"
date:       2019-10-14
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
判断一棵二叉树是否为对称二叉树。

输入空间：二叉  
解空间：二叉

解题“七步走” (保持这种sense)：  
1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thinking Process (What data structure, algorithm?)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

### 题目要求
[原题链接](https://leetcode.com/problems/symmetric-tree/)  
判断一棵二叉树是否为对称二叉树。  
对称二叉树的定义是，以全局的根为对称轴，把全局的根的右子树翻转到左边，能够刚好跟全局的根的左子树相吻合，那么它就是对称二叉树，反之就不是。

### 举例与输入输出
例子直接用LeetCode上的图。

![oh-my-zsh](/img/in-post/20191014-lc-101/lc101.png)

### 思路:从定义出发
本题和我们之前做的[LC 110 判断平衡二叉树](../../../../2019/08/25/LC-110-balanced-binary-tree/)一样，都可以利用分治法，从**定义出发**进行求解。我们要想明白的是如下三点：
1. 把全局的根剔除之后，对左根形成的左子树和右根形成的右子树进行判断。这就需要用到辅助函数，辅助函数需要带上两个根。在辅助函数最初始的状态，其参数一个为左子树的左根，另一个为右子树的右根。注意，我们仍然要把这两个根看作是基于递归的不断运动着的两个根。
2. 在分治法的base cases情况，判断什么时候左根和右根会导致二叉树不为对称二叉树是重点（因为判断了`不是`的base case, `是`的base case就是它的补集）。
3. 在分治法的`分`的情况，针对左根和右根，我们要比对两种情况，左根的左子是否等于右根的右子，左根的右子是否等于右根的左子，这样。

其他看代码都容易掌握，这里稍稍展开一下上述的第2点。Base case左根和右根能导致树不为对称二叉树的情况有三种，举最简单的三个例子，分别是(以下用`#`号代表`null`)
```
   1
  / \
  2 #
```
全局根1的左根为2，1的右根不存在，所以不对称。

```
   1
  / \
  # 2
```
全局根1的左根不存在，1的右根为2，所以不对称。

```
   1
  / \
  8 2
```
全局根1的左根为8，1的右根为2，8与2不相等，所以不对称。

### 本题（LC 101）代码
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
  public boolean isSymmetric(TreeNode root) {
    if (root == null) {
      return true;
    }

    return isSym(root.left, root.right);
  }

  private boolean isSym(TreeNode leftRoot, TreeNode rightRoot) {
    if (leftRoot == null && rightRoot == null) {
      return true;
    }

    // 不为对称的base case
    if ( (leftRoot != null && rightRoot == null)
      || (leftRoot == null && rightRoot != null)
      || (leftRoot.val != rightRoot.val) ) {
        return false;
      }

    // Divide
    boolean case1 = isSym(leftRoot.left, rightRoot.right);
    boolean case2 = isSym(leftRoot.right, rightRoot.left);

    // Conquer
    return case1 && case2;
  }
}
```

### 时间空间复杂度
时间复杂度：遍历树的所有节点，`O(n)`，  
空间复杂度：为递归栈的深度，所以是`O(log(n))`。

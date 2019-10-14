---
layout:     post
title:      "LeetCode 235. Lowest Common Ancestor of a Binary Search Tree"
subtitle:   "LeetCode 235. 二叉搜索树的最近公共祖先"
date:       2019-10-14
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
寻找一棵二叉搜索树的最近公共祖先。

### 二叉搜索树的定义
在开始讲本题前，我们先来回顾一下二叉搜索树的定义。二叉搜索树(Binary Search Tree)是二叉树(Binary Tree)的一个子集。它的定义是一种递归式的定义，表述如下：
> 对于二叉树的每一个节点而言，其左子树的任何一个节点的值都会小于或等于当前节点，其右子树的任何一个节点的值都会大于或等于当前节点。

上述是一个递归式的定义。  
二叉搜索树还有一个属性就是，如果用中序遍历的方式遍历二叉树，得到的会是一个排好序的数组。为了打字方便，下面提到的二叉搜索树我可能就用其英语缩写BST代替了。  

举一个是BST的例子。
```
      8
    /   \
   5    13
  / \   /
  1 7  10
```
显然，任何一个非叶节点的左子的任意一个值都小于（或等于）节点本身的值，右子都大于（或等于）节点本身的值。其中序遍历得到的数组是`[1, 5, 7, 8, 10, 13]`。

举一个不是BST的例子。
```
      8
    /   \
   5    13
  / \   /
  1 9  10
```
这不是一棵二叉搜索树，因为对于节点8（根节点）而言，其左子树有一个节点为9，比8来得大。我们来看中序遍历这棵二叉树的结果，为`[1, 5, 9, 8, 10, 13]`，也能看出结果数组也不是全局有序的。  

好，回到本题。  

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
[原题链接](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)  
寻找一棵二叉搜索树的两个节点的最近公共祖先。  
最近公共祖先的定义是：在给定的BST中，对于给出的两个节点p和q,最近公共祖先A是能满足p和q皆为A的子节点，且A是在从上到下的层次关系中最靠近p和q的节点。（言下之意，本定义也允许A是p或q节点中的一个）

### 假设
面试者：我们能假设该BST中没有相同数值的节点吗？  
面试官：可以。

面试者：我们能假设该给出的p和q节点，p的值一定小于q吗？  
面试官：不可以。

### 举例与输入输出
例子直接用LeetCode上的图。

![oh-my-zsh](/img/in-post/20191014-lc-235/lc235.png)

在例子1中，节点2和8的最近公共祖先就是全局的根节点6。在例子2中，节点2和4，由于2刚好是4的父节点，所以2和4的最近公共祖先就是节点2。

### 思路：迭代法，利用好BST的属性
我们先前做的很多二叉树的题目，都是用递归的方法，或者更细致一点，都是用递归思想中的分治方法来求解的。当然，相当一部分可以用递归方法求解的二叉树题目，也可以用迭代的方法来求解，只不过很多时候迭代的方法要用到队列或者栈等辅助的数据结构。  

对于BST，由于其本身具备in-order traversal会形成有序数组这个属性，所以有时候用迭代的方法解题会更简单。迭代法的意思是，从全局的根节点开始，利用一个loop(往往用whie loop)，或向左子树走，或向右子树走，找到最终答案的过程。

对于本题，只要想清楚最近公共祖先A，相对于节点p和q，只可能有如下三种情况，就容易写出之后的代码了：

1. 最近公共祖先大于p,q当中值较大的那一个(寻找过程要往A的左子树走)
```
     A
   /
p
   \
    q
```

2. 最近公共祖先小于p,q当中值较小的那一个(寻找过程要往A的右子树走)
```
     A
       \
         p
        /
       q
```

3. 最近公共祖先的值刚好介于p,q之间（那我们其实已经找到了最近公共祖先）
就是上述截图例子1的情况。在例子1中，如果我们把p和q的值分别换成4和7，其最近公共祖先依然是值刚好介于4和7之间的根节点6。

### 本题（LC 235）代码
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
  public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    while (true) {
      // Case 1
      if (root.val > Math.max(p.val, q.val)) {
        root = root.left;
      }

      // Case 2
      else if (root.val < Math.min(p.val, q.val)) {
        root = root.right;
      }

      // Case 3: we found it
      else {  // the else block cannot be omitted
        break;  
      }
    }
    return root;
      // even if the given tree is an empty tree, return root is fine
  }
}
```

### 时间空间复杂度
时间复杂度：每一次向下搜索二叉树都会扔掉当前树的一半节点，所以`O(log(n))`，  
空间复杂度：为递归栈的深度，所以是`O(log(n))`。

### 思考
当然，这道题也可以用递归的方法来求解。读者朋友们可以先想一想，我会在下一期讲“LC 236 二叉树的最近公共祖先”那道题的时候，给出递归的解法。

---
layout:     post
title:      "LeetCode 145. Binary Tree Postorder Traversal"
subtitle:   "LeetCode 145. 二叉树的后序遍历"
date:       2019-08-03
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
### 回顾
上一期我们做的“[LeetCode 144. 二叉树的前序遍历](https://mp.weixin.qq.com/s?__biz=MzUyODY0MTM4Mg==&mid=2247483853&idx=1&sn=34ae76652ce2c02f16d441ee38ffa530&chksm=fa6c7dc4cd1bf4d203052e64f1326698e408d4a3e392e052f96e6f38abac92c9602f5ec2d524&token=1681623248&lang=zh_CN#rd)”的解法一，有网友问道为什么我们可以把存结果的整数列表`res`放到辅助的traverse()递归函数中，逐步将每一步的结果填充入其中呢？  
其实，笔记哥上一次分享的文章《[10张 GIF 动图让你弄懂递归等概念](https://mp.weixin.qq.com/s?__biz=MzUyODY0MTM4Mg==&mid=2247483857&idx=1&sn=0644253d3a5fcb3f08726b099d01bf09&chksm=fa6c7dd8cd1bf4ceb063c2c182a9599349b250f2f4920d02582ee983706d2d071503867ea5a8&token=1681623248&lang=zh_CN#rd)》中的“GIF 7：按值传递和按引用传递的区别”解释了这个问题。  
在Java语言中，`int`,`float`,`char`,`double`等等是primitive type，中文貌似翻译做“原始型”，这些类型的数据就是按照数值传递的，所以当这些类型的变量被传进一个函数的时候，内存中的栈(stack)复制了一份它的数值，两个“它们”其实是完全不同的拷贝；当在函数中的它被改值的时候，外面的那个它是不会感应到值的变化的，即这个动图中的“pass by value”☕️杯的例子。OK，我们上一期做题的时候，传给`traverse()`函数的是一个整数列表(List<Integer>)，这在Java语言中是对象类型，且对象类型传递的是原对象的引用，对应的就是动图中“pass by reference”☕️杯的例子。所以啊，当res这个整数列表在traverse()递归函数中被改了值的时候，traverse()函数外面的res是可以同时感应到值的改变的，因为传递给traverse()函数只是一个新的res的引用，这两个引用其实都指向内存堆(heap)中的同一个记录res的值的一段空间。  

再次的，解题“七步走” (面试答题时候不一定每一步都用上，但要保持这种sense)：  
1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thinking Process (What data structure, algorithm?)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

### 题目要求
[原题链接](https://leetcode.com/problems/binary-tree-postorder-traversal/)  
中译：通过后序遍历的方式遍历一个二叉树，并把遍历的每一个节点的值存到一个数组（或整数列表，如果使用的是Java语言）中，返回这个数组。

### 举例与输入输出
如下图所示，第一层根节点有有一个根为4，根的左节点为null，右节点为9。在第二层节点9之下，它有左节点为7，右节点为null。在图中，我用#号来表示null。
```
   4
  /  \
 #   9
    /  \
    7   #
   / \
   #  #
```
那么，我们要得到的结果就应是数组[7, 9, 4]。

### 思路1: 从postorder的定义出发的方法
postorder的定义用中文概括就是按 **“左右根”** 的顺序进行访问。欢迎读者按照上一期“[LeetCode 144. 二叉树的前序遍历](https://mp.weixin.qq.com/s?__biz=MzUyODY0MTM4Mg==&mid=2247483853&idx=1&sn=34ae76652ce2c02f16d441ee38ffa530&chksm=fa6c7dc4cd1bf4d203052e64f1326698e408d4a3e392e052f96e6f38abac92c9602f5ec2d524&token=1681623248&lang=zh_CN#rd)”的 思路1 的思考过程，在草稿纸上画一下这棵树的后序遍历访问过程。

### 代码1
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
    public List<Integer> postorderTraversal(TreeNode root) {
        // 生成存放结果的整数列表
        List<Integer> res = new ArrayList<>();

        // 把整数列表放到辅助的traverse()递归函数中，逐步将其填充入结果
        traverse(root, res);

        // 返回结果整数列表
        return res;
    }

    void traverse(TreeNode root, List<Integer> res) {
        // 递归的基本情况: 当根为null的时候
        if (root == null) {
            return;
        }

        // 递归的recursive情况: 从postorder定义出发
        traverse(root.left, res);  // 处理当前root的左子树
        traverse(root.right, res);  // 处理当前root的右子树
        res.add(root.val);  // 添加当前root的值进入到结果列表
    }
}
```

### 思路2: 分治法
欢迎读者模仿上一期“[LeetCode 144. 二叉树的前序遍历](https://mp.weixin.qq.com/s?__biz=MzUyODY0MTM4Mg==&mid=2247483853&idx=1&sn=34ae76652ce2c02f16d441ee38ffa530&chksm=fa6c7dc4cd1bf4d203052e64f1326698e408d4a3e392e052f96e6f38abac92c9602f5ec2d524&token=1681623248&lang=zh_CN#rd)”的 思路2 的思考过程，想一想这棵树的后序遍历访问过程。

您可以思考一下：这一次，节点7是不是我们最先处理好的节点？如果是的话，为什么这一次它会在结果数组中出现在第一位呢？

OK，再次回顾一下我们在 [LeetCode 226. Invert Binary Tree](http://starwavelin.com/2019/06/10/LC-226-invert-binary-tree/) 这道题的讲解中的分治法模板。
```
模板：
public TreeNode someFunction(TreeNode root) {
   1. write base case

   2. write division，conceptually as below:
   root.left = someFunction(root.right);
   root.right = someFunction(root.left);

   3. Conquer
   ie. combine some results
   return value;
}
```

经模板推倒出如下代码

### 代码2
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
    public List<Integer> postorderTraversal(TreeNode root) {
        // 生成存放结果的整数列表
        List<Integer> res = new ArrayList<>();

        // base case
        if (root == null) {
            return res;
        }

        // write division
        List<Integer> left = postorderTraversal(root.left);
        List<Integer> right = postorderTraversal(root.right);

        // conquer
        // conquer的前提是假定当前根的左子树、右子树都搞定了，
        // 就按 左右根 的顺序把结果合并起来就行了，符合postorder定义
        res.addAll(left);
        res.addAll(right);
        res.add(root.val);

        // 返回结果整数列表
        return res;
    }
}
```

**代码小结**  
1. 回答👆的思考问题。节点7确实是我们最先处理好的节点。这一次，在后序遍历的分治解法中，它会在结果数组中出现在第一位，是因为分治解法的治(conquer)的过程保证了输出结果的顺序。
我们看看程序运行到存储以9为全局的根的子树时候的情况
```
res.addAll(left); // 结果列表加入 7
res.addAll(right); // 结果列表加入 空列表，原因是9的右子树为空
res.add(root.val); // 结果列表加入 9
```

### 时间与空间复杂度分析
时间复杂度，由于二叉树的每一个节点都会遍历到，所以是`O(n)`，n为二叉树的节点个数。  
空间复杂度，由于新开了一个变量用于存所有节点的值的`res`，所以空间复杂度为`O(n)`。

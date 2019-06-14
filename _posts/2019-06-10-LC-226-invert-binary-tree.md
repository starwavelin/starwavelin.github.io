---
layout:     post
title:      "LeetCode 226. Invert Binary Tree 从这题了解算法面试的套路"
subtitle:   "LeetCode 226. 翻转二叉树"
date:       2019-06-10
author:     "starwavelin"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
### 什么是算法面试的套路？
很多小伙伴发现自己在北美的软件工程师算法面试中，题都答对了，为什么最后没有给Offer呢？
原来，算法考察的不仅仅是写代码的能力，它还考察你的考虑问题的全面性、你的思路、语言表达以及是否会主动跑个测试这样的好习惯等等方面的能力。而且，即便是考LeetCode原题，你到底是背答案背进去的，还是理解了讲清楚写出来的，这里面也是有很大差别的呢。

因此，我这里总结了回答一道算法面试题的如下七步走。也许，并不是每一道题都会用到如下七步，但只要您平常解题时候养成这样的好习惯，之后在面试时必定游刃有余。

1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thought Process (What data structure, what algorithm)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests


下面我以*LeetCode 226. Invert Binary Tree*为例与你一起过一遍拿到一道算法面试题以后的与面试官交流答题步骤。

### 题目要求
[原题链接](https://leetcode.com/problems/invert-binary-tree/)  
简明中文翻译：反转一个二叉树

### 假设
你可以问面试官：这个二叉树是否是平衡的？  
面试官预计回答说：二叉树是否平衡对本题不重要。

### 举例与输入输出
直接使用LeetCode原题的例子
![oh-my-zsh](/img/in-post/20190610-lc-226/example.png)
从这个例子中就可以搞清楚，这道题不单单是对最大的树而言，它的左右子树进行了互换；而且是最大的树之内的任何一个子树而言，它的左右子树也都进行了互换（反转）。    
什么意思呢？因为假如我们只对最大的，或者说最外层的树进行左右子树互换，那么我们得到的Inverted Binary Tree就应该长下面这样：
```
          4
        /   \
       7     2
      / \   / \
     6   9  1  3
```
显然这不是题目的要求。所以啊，通过举例子，跟面试官交流清楚input/output,就能确保你100%了解题目的真正要求。

### 思路1: preorder approach
显然这道题可以通过自顶向下(top-down approach)的递归方法来求解，也可以叫做前序遍历的方法。大家可以看我草稿纸上画的：
![oh-my-zsh](/img/in-post/20190610-lc-226/thought1.png)

### 代码1
有了思路以后，写代码主要就是熟练度的问题。下面提供笔记哥比较熟的Java语言的代码解答。
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
    public TreeNode invertTree(TreeNode root) {
        if (root == null)
            return null;
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

### 思路2: Divide and Conquer (分治法)思想
这道题也可以通过自底向上(bottom-up approach)的 **分治思想的递归方法** 来求解，也可以叫做后序遍历的方法。后序遍历是指先处理好根的左节点、而后处理根的右节点，最后再来处理根的本身。大家可以看我草稿纸上画的：
![oh-my-zsh](/img/in-post/20190610-lc-226/thought2.png)

即自底向上很重要的一个思想是：我们要假定overall的根的左子树都已经搞定了（反转好了），右子树也已经反转好了，然后剩下的步骤就是搞定overall的根的左右两边。  
那，我们怎么才能用代码实现“overall的根的左子树都已经搞定了”， “overall的根的右子树都已经搞定了”----靠递归嘛。

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
    public TreeNode invertTree(TreeNode root) {
        if (root == null)
            return null;
        TreeNode tmp = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(tmp);
        return root;
    }
}
```

**代码小结**  
可以看出，这道题的分治法（Divide and Conquer, 简称 D&C）代码也不长，就6行。所以，这个分治法代码可以作为一个模板，解决以后的类似可以用D&C求解的问题。
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
用 **代码2** 来比对这个模板，我觉得吧，代码2还少了"3. Conquer"的部分，不是最好的例子，但以后遇到的题目肯定会用到具体的Conquer操作。  
另外就是，有朋友会问为什么实际的代码中还要用到`tmp`变量, 而不是直接的 `root.left = someFunction(root.right);` `root.right = someFunction(root.left);`那样的写法。道理也很简单，当你执行`root.left = someFunction(root.right);`的时候，你已经把`root.left`进行改变了嘛，所以，当之后的函数要去作用的是**原本的root.left**的时候，你是不是应该把**原本的root.left**用一个变量先存起来呢？

### 时间与空间复杂度分析
时间复杂度，由于二叉树的每一个节点都会遍历到，所以是`O(n)`，n为二叉树的节点个数。  
空间复杂度，由于只新开了一个变量`tmp`，所以空间复杂度为`O(n)`。

### 测试
面试中的测试其实就是表现你的好习惯。你可以用原有的例子，或者新举一个例子，在白板上手动跑一下你的代码，由你来带领面试官验证你的代码的正确性。万一，你在手动白板测试过程中发现自己哪里做的不对，也不要慌张，想想是代码的哪一个环节出错了，对应的进行修改。在你有这样好习惯的基础之上，面试官也是很愿意跟你一起看看的。毕竟，北美的算法面试不是高考。算法面试的主要目标是找到未来的可以很好进行合作的同事，所以能力一方面，沟通协调等软实力则是也很重要的另一方面。

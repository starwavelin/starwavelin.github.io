---
layout:     post
title:      "LeetCode 144. Binary Tree Preorder Traversal"
subtitle:   "LeetCode 144. 二叉树的前序遍历"
date:       2019-07-28
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
首先回顾一下“七步走”。并不是解答每一道题都会用到如下七步，但只要您平常解题时养成好习惯，之后在面试中必游刃有余。

1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thought Process (What data structure, what algorithm)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

下面我以 *LeetCode 144. Binary Tree Preorder Traversal* 为例讲解。

### 题目要求
[原题链接](https://leetcode.com/problems/binary-tree-preorder-traversal/)  
简明中文翻译：通过前序遍历的方式遍历一个二叉树，并把遍历的每一个节点的值存到一个数组（或整数列表，如果使用的是Java语言）中，返回这个数组。

### 假设
略

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
那么，我们要得到的结果就应是数组[4, 9, 7]。

### 思路1: 自顶向下(top-down approach)的递归方法，也是preorder的从定义出发的方法
preorder的定义用中文概括就是按“根左右”的顺序进行访问。所以，上面的例子可以这么看：先访问了根，根是有东西的，是4，把4存到结果数组中，接着看根的左子树，左子树为空，OK，略过，再看根的右子树，右子树的根为9，好，把9存到结果数组中，再看9的左子树，这时的根为7，好，把7存到结果数组中；注意，这时候查看过程（即程序）还没有完，7的左子树是什么，空，OK，忽略，7的右子树是什么，是空，OK，再忽略，程序回到处理9时候的情况，再看看9的右子树，OK，9的右子树为空，忽略。**在这个时候**，程序才处理完了，我们把已经填充了[4, 9, 7]的结果数组返回。

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
    public List<Integer> preorderTraversal(TreeNode root) {
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

        // 递归的recursive情况: 从preorder定义出发
        res.add(root.val);  // 添加当前root的值进入到结果列表
        traverse(root.left, res);  // 处理当前root的左子树
        traverse(root.left, res);  // 处理当前root的右子树
    }
}
```

### 思路2: Divide and Conquer (分治法)思想
虽然从定义出发，preorder的访问顺序应为根左右，但这道题也可通过自底向上(bottom-up approach)的 **分治思想的递归方法** 来求解。

自底向上很重要的一个思想是：我们要假定overall的根的左子树都访问好了，右子树也已经访问好了，**但是**，这些个访问好的节点我们都没有存到结果数组里，而是把overall的根的值先存到结果数组里，然后，剩下的步骤是处理overall的根的左右两边。  

“把overall的根的值先存到结果数组里，然后，剩下的步骤是处理overall的根的左右两边。”--这个过程，符合Preorder的定义。

那么，在上面[4, 9, 7]的例子中，先被处理好的节点是哪一个呢？你先自己思考一下。


答案是节点7，但处理好归处理好，结果数组中的第一个出现的数字不是7。这里，“处理好”的意思是，我访问了7的左子树，为空，7的右子树，也为空，没得访问了，7算处理好了，存到结果数组中。 那，为什么结果数组的第一个数字又不是7呢？这里卖个关子，请你认真往下看：

可能读者看到这里有点清楚了，但也还有点抽象。我想，既然，我们在 [LeetCode 226. Invert Binary Tree](http://starwavelin.com/2019/06/10/LC-226-invert-binary-tree/) 这道题的讲解中，已经给出了一个分治法模板，我们就再来看看这个模板，而后看看如何套用模板实现代码。

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
    public List<Integer> preorderTraversal(TreeNode root) {
        // 生成存放结果的整数列表
        List<Integer> res = new ArrayList<>();

        // base case
        if (root == null) {
            return res;
              /* 这是个容易错的点，当当前root为null时，
                我们不可以返回null，而是要返回当前已有的res，这时候的res可能只是一个空的List。
                但只有这样，我们才能保证res.addAll(someArrayList）;的有效性
              */
        }

        // write division
        List<Integer> left = preorderTraversal(root.left);
        List<Integer> right = preorderTraversal(root.right);

        // conquer
        // conquer的前提是假定当前根的左子树、右子树都搞定了，就按根左右的顺序把结果合并起来就行了，符合preorder定义
        res.add(root.val);
        res.addAll(left);
        res.addAll(right);

        // 返回结果整数列表
        return res;
    }
}
```

**代码小结**  
1. 我们上面提到先处理好的节点是7，但处理好归处理好， 结果数组的第一个数并不是7，是因为，7虽然先存入了结果数组，但它在相对于处理节点9的过程中，会作为`List<Integer> left`的结果，并到含有9的数组里面去，原因就是我们在conquer的过程中，是先有
```
res.add(root.val); // 结果数组加入 9
res.addAll(left); // 结果数组加入 7
```

2. 也提一下`addAll(ArrayList)`函数，这是Java的`ArrayList`数据类型自带的一个函数，用于平摊地把结果加入到一个列表中，所以，通过`addAll(ArrayList)`函数，您得到的结果不会是`[4, [9, [7]]]`， 而是`[4, 9, 7]`

3. 相对于解法1，该解法肯定是更耗时的，因为在递归的过程中，解法1对每一个被处理到的节点只要做1次的add操作，而解法2对每一个被涉及到的节点最多会做3次add操作。

4. 但该解法也有两个优点：（1）易于多线程化，（2）不用将存结果的变量`res`作为参数传到别的函数中。

### 时间与空间复杂度分析
时间复杂度，由于二叉树的每一个节点都会遍历到，所以是`O(n)`，n为二叉树的节点个数。  
空间复杂度，由于新开了一个变量用于存所有节点的值的`res`，所以空间复杂度为`O(n)`。

### 测试
略

---
layout:     post
title:      "LeetCode 110. Balanced Binary Tree"
subtitle:   "LeetCode 110. 判断一棵树是否为平衡二叉树"
date:       2019-08-25
author:     "代码笔记哥"
header-img:
tags:
    - 二叉解空间
    - Binary Tree
---
上一篇我们讲到了[中英文语境中对二叉树部分类型的表述](http://starwavelin.com/2019/08/24/types-of-binary-trees/)的略有不同，今天我们来看一道跟二叉树定义有关的题：判断一棵树是否为平衡二叉树。

### 回顾
解题“七步走” (保持这种sense)：  
1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thinking Process (What data structure, algorithm?)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

### 题目要求
[原题链接](https://leetcode.com/problems/balanced-binary-tree/)  
给你一棵二叉树，判断它是否为平衡二叉树。

### 假设
询问面试官，搞清楚平衡二叉树的定义。  
面试官告诉你：平衡二叉树是指，对一棵二叉树内的**任意**一个节点，其左子树的最大深度与右子树的最大深度的差值小于或等于1。

### 举例与输入输出
```
   3
  / \
 9  20
   /  \
  15   7
```
这是一棵平衡二叉树，它的任意一个节点的左子和右子树的最大深度的差值为1。以全局的根节点3为例，它的左子树最大深度为2，右子树的最大深度为3，所以发现它的左子和右子树的最大深度的差值恰好为1。符合。

```
   3
    \
    20
   /  \
  15   7
```
这**不是**一棵平衡二叉树，它有一个节点的左子和右子树的最大深度的差值大于1。以全局的根节点3为例，它的左子树最大深度为1（因为左子树为null），右子树的最大深度为3，所以发现它的左子和右子树的最大深度的差值为2。所以该树不是平衡二叉树。

### 思路1: 从定义出发
如果一棵二叉树为平衡二叉树，则它的任何一个节点必须符合：
1. 它的左子树是一棵平衡二叉树
2. 它的右子树是一棵平衡二叉树
3. 它的左子树的最大深度与右子树的最大深度的差值的绝对值<=1  

以上三点之间是 **逻辑与(AND)** 的关系。  
在做二叉树的题目，当我们要对“任何一个节点”进行操作的时候，其实就是对`root`这个变量进行操作，我们心里始终把`root`想成是“一个移动着的根”，就会对二叉树的递归属性更好理解了。  
显然，上述三点中的第1、2点，要求递归地调用“是否为平衡二叉树”这个函数。而第3点，则可以用我们已经做过的题目[104. 二叉树的最大深度](http://starwavelin.com/2019/08/17/LC-104-maximum-depth-of-binary-tree/)来解决

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
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }

        boolean isLeftTreeBalanced = isBalanced(root.left);
        boolean isRightTreeBalanced = isBalanced(root.right);
        return isLeftTreeBalanced
            && isRightTreeBalanced
            && Math.abs(maxDepth(root.left) - maxDepth(root.right)) <= 1;
    }

    private int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

*代码分析*  
1. 上面的Java代码中的private函数`maxDepth(TreeNode root)`即为我们做过的[LeetCode 第104题](http://starwavelin.com/2019/08/17/LC-104-maximum-depth-of-binary-tree/)的题解。这告诉我们在解题中，将一道新的题目合理的往已知题目靠拢，利用已知题目的解为新题服务是一种有益的做法。
2. 主函数`isBalanced(TreeNode root)`中的`return`部分涉及的三个被`&`起来的判断，即我们的思路1当中，从定义出发的对平衡二叉树的三点判断的体现。

### 代码1的时间空间复杂度
我们把二叉树的高度记做`h`，总的节点数记做`n`。那么，  
时间复杂度：由于对二叉树的每一个节点，我们都要做一个最大深度的计算，所以是`O(nh)`。  
空间复杂度：为递归栈的深度，也就是树的高度，所以是`O(h)`。

### 思路2: 在思路1的基础上改进，逆向思维
我们在做[LeetCode 第104题](http://starwavelin.com/2019/08/17/LC-104-maximum-depth-of-binary-tree/)的时候，是单单从全树的根节点，计算出全树的最大深度。那么，在做这道平衡二叉树的题的时候，有没有可能只从全树的根出发，通过自底向上的递归方法，把这棵树是否是平衡二叉树或最大深度的信息，传递到全树的根节点。

这是可行的。我们可以这么想，只要在计算`maxDepth`的过程当中，我发现某个节点的左子树最大深度与右子树最大深度的差值大于1了，我就返回这棵树不是平衡二叉树就行了。反之，如果在计算`maxDepth`的过程当中，我始终**没有发现**有某个节点的左子树最大深度与右子树最大深度的差值大于1，那就说明整棵树是一棵平衡二叉树。

因为`maxDepth`的返回值的类型为整数，那么我们可以用`Integer.MIN_VALUE`（Java中整数的最小值）来标记我们发现这棵树不是平衡二叉树了。另外，函数名字也不能再叫`maxDepth`了，毕竟我们要干两件事，所以我给起名叫`checkBalanceAndCalcMaxDepth`。函数名有点长，但就是“判断是否平衡二叉树且计算最大深度”的意思。

### 代码2
```
class Solution {
    public boolean isBalanced(TreeNode root) {
        return checkBalanceAndCalcMaxDepth(root) != Integer.MIN_VALUE;
    }

    private int checkBalanceAndCalcMaxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = checkBalanceAndCalcMaxDepth(root.left);
        int right = checkBalanceAndCalcMaxDepth(root.right);

        // 与纯粹求maxDepth那道题不同的地方：
        if (left == Integer.MIN_VALUE || right == Integer.MIN_VALUE || Math.abs(left - right) > 1) {
            return Integer.MIN_VALUE;
        }

        return Math.max(left, right) + 1;
    }
}
```

*代码分析*
1. 值得注意的是，在工业界，一般一个函数就干一个事情才是好的编码习惯。本题的代码2是一个优化了时间复杂度的解法，但就不再符合“一个函数就干一个事情”的原则。

### 代码2的时间空间复杂度
我们把二叉树的高度记做`h`，总的节点数记做`n`。那么，  
时间复杂度：由于这次我们只对二叉树的根节点，做一个最大深度的计算或是否平衡树的判断，所以是`O(n)`。  
空间复杂度：为递归栈的深度，也就是树的高度，所以是`O(h)`。

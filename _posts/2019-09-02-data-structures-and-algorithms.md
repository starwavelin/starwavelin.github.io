---
layout:     post
title:      "数据结构与算法，傻傻分不清楚？"
subtitle:   "Distinguish Data Structures and Algorithms"
date:       2019-09-02
author:     "代码笔记哥"
header-img:
tags:
    - 算法
---
笔记哥的公众号的“最新讲题”部分，目前的目标是帮助自己和大家复习北美软件工程师的算法面试。
而为了对付算法面试，我们需要学习数据结构与算法。那什么是*算法面试*，什么是*数据结构*，什么又是*算法*？为什么有时候这数据结构与算法这两个概念合在一起讲，这两者之间有什么区别呢？

别急，听我娓娓道来。

**算法面试**：这其实是软件工程师圈子里的一个行话。在英文里的一个对应词应该是 Coding Interview，直接翻译过来应作“编程面试”。但由于大家（至少我在美的华人朋友圈里）都已经习惯叫“算法面试”了，所以我也一般都用这个词来表示 Coding Interview。 Coding Interview的考察内容，主要就是数据结构和算法。但我猜啊，由于称呼“数据结构与算法面试”这样的长词语太拗口了，所以大家都叫它“算法面试”了。

**数据结构**：假如我们单说数据结构（Data Structures），它指的是计算机存储并组织数据的方式。我下面会展开讲讲常见的算法面试中会遇到的数据结构有哪些类型。

**算法**：算法（Algorithms）是指为了解决某个问题而定义出的一系列的清晰指令，是对解决问题的方案准确且完整的描述。这个定义听着有点儿拗口，但我自己以前学算法的时候，老师就把算法比作做菜的菜谱。比如我要煎鸡蛋，那么我需要：
```
打开炉灶的火->放上平底锅->倒入少许油->打入鸡蛋->再打入一粒鸡蛋
->调成小火->盖上锅盖焖煮->8分钟后撒上一些盐->撒上一些胡椒
->再过4分钟后看到蛋黄颜色可口，将鸡蛋乘入盘中->关掉炉灶的火
```
OK，这么一串为了煎鸡蛋而做出的清晰指令，就可以理解为一套算法。

### 数据结构
对于目前的北美面试算法，需要掌握的数据结构类型可以分为如下四大类。由于我之后会写相应的推文讲每一大类的数据结构的用途与定义，常见功能及复杂度，实现原理以及注意事项等等，所以每一个数据结构我只是简单的列一下。

1. 线性数据结构 (Linear Data Structure)  
常见的有(Java语言语境下)：Array, ArrayList, LinkedList, Stack, Queue
2. 树形数据结构 (Tree Shape Data Structure)  
常见的有：树与Heap（堆）。树当中有可以分为二叉树、多叉树等  
3. 字典类型（或称哈希类型）数据结构 (Map/Set Data Structure)  
常见的有：HashMap, HashSet  
4. 图类数据结构 (Graph Data Structure)  
常见的分类有：有向图、无向图 等等  

### 算法
这里我也写一下面试当中常见到的几种算法类型
1. 排序算法 (Sorting)  
O(n^2)的数量级的算法：冒泡排序、选择排序、插入排序  
O(nlogn)的算法：归并排序、快速排序、堆排序  
O(n)但是消耗空间的算法：桶排序  
当然，一般面试题不会直接考这些算法的代码，而是运用这些排序算法的思想来解决问题。  
2. 搜索算法 (Searching)  
二分搜索  
3. 递归 (Recursion)  
递归是一种思想，一般不算做一个单独的算法类型。掌握递归的要点在于发现**递归关系**与**基本Case**。  
3.1 重复计算  
如果一段代码，使用递归解决，思路是很清晰的，但由于具有大量的重复计算，效率是低下的，那么我们可以考虑记忆化（Memorization）的算法来避免重复计算，这往往形成动态规划的方法  
经典例子：  
[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)  
[55. Jump Game](https://leetcode.com/problems/jump-game/)  
[223. Rectangle Area](https://leetcode.com/problems/rectangle-area/)
4. 广度优先搜索 (Breadth First Search)  
特点：越接近初始节点的点就会越早地被遍历到。  
经典例子：  
[127. Word Ladder](https://leetcode.com/problems/word-ladder/)  
[690. Employee Importance](https://leetcode.com/problems/employee-importance/)  
[120. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)  
[120. Number of Islands](https://leetcode.com/problems/number-of-islands/)
5. 深度优先搜索 (Depth First Search)  
特点：遍历的时候先一条路走到黑。  
经典例子：  
[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)  
[104. Maximum Depth of Binary Tree](http://starwavelin.com/2019/08/17/LC-104-maximum-depth-of-binary-tree/)  
[112. Path Sum](https://leetcode.com/problems/path-sum/)  
[207. Course Schedule](https://leetcode.com/problems/course-schedule/)
6. 回溯算法 (Backtracking)  
特点：回溯算法的解空间可以用树来表示。  
经典例子：  
[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)  
[n Sum](https://blog.csdn.net/ffj0721/article/details/84256818)  
[79. Word Search](https://leetcode.com/problems/word-search/)  
[212. Word Search II](https://leetcode.com/problems/word-search-ii/)  
[51. N-Queens](https://leetcode.com/problems/n-queens/)
7. 动态规划 (Dynamic Programming)  
动态规划往往是最能有效考察算法和设计能力的题目类型，面对这类题目最重要的是抓住问题的阶段，了解每个阶段的状态，从而分析阶段之间的转化关系。  
经典例子：  
路径系列问题  
[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)  
[62. Unique Paths](https://leetcode.com/problems/unique-paths/)  
[63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)  
[1055. Shortest Way to Form String](https://leetcode.com/problems/shortest-way-to-form-string/)    
买卖股票类问题  
[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  
[123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)  
[198. House Robber](https://leetcode.com/problems/house-robber/)  
[213. House Robber II](https://leetcode.com/problems/house-robber-ii/)    
子序列问题  
[115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)  
[152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)  
[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence)  
[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)  
8. 贪心算法 (Greedy Algorithm)  
特点：对问题求解的时候，总是做出在当前看来是最好的做法。  
经典例子：  
[322. Coin Change](https://leetcode.com/problems/coin-change/)  
[518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)  
[122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)  
[714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)  

这些算法我也不展开多讲，但读者朋友们会在今后的讲题中逐步遇到的。

### 小结
总的来讲，数据结构和算法，二者的区别在于：  
数据结构描述的是**空间上的组织概念**  
算法描述的是**时间上的过程概念**   

但两者是往往是配合在一起，解决实际编程中的问题。

P.S. 点击阅读原文可以直接跳转具体题目的LeetCode链接

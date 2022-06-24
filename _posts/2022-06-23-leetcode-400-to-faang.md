---
layout:     post
title:      "如何刷400道LeetCode题实现FAANG自由？"
subtitle:   ""
date:       2022-06-23
author:     "代码笔记哥"
header-img:
tags:
    - 算法
---

### 前言
本文原文为Blind上的一篇网友投稿。该网友已经刷了200道题，计划再刷200-250道。笔记哥觉得该网友的说法挺有道理，所以翻译其中的干货部分，供大家参考。    
  

### 1. 数据结构的基本功
首先的一步是了解各种基础数据结构的用法。注意，这第一步你只要确保会运用它们就行了，不要求了解这各种数据结构是怎么实现的。  
那这些数据结构包括哪些呢？罗列如下：   

Array, Stack & Queue, Tree, Graph, HashTable, Heap, LinkedList.     


了解它们的基本用法，就是在你熟悉的面试用编程语言中，知道如何实例化、初始化这类数据结构，会他们的常用的添加、删除、查找元素的方法，就可以了。

注意，这一步只要求你了解这些基础数据结构的基本功，不要求了解各种组合运用这些数据结构的**算法**。关于“数据结构”和“算法”的联系与区别，请看笔记哥的[数据结构与算法，傻傻分不清楚](../../../../2019-09-02-data-structures-and-algorithms)一文。

### 2. 了解基本算法和递归
如果说上面一步只要求了解基本数据结构，那这一步就一定要求您了解基本的算法了。   
这里笔记哥夹一点私货，笔记哥认为基本算法包括如下：   

双指针法，贪心法，各种排序算法，二分搜索，广度优先搜索，深度优先搜索，分治法。
还有难的就是 动态规划。   


OK，回到这个作者提到的，这个作者特别把“递归”也列了出来。   
因为有了一定工作经验的程序员，是一定要懂得如何用简洁的可复用的递归方法来解决问题的。上面提到的排序算法中的 归并排序、快速排序就用到了递归，深度优先搜索和一些的分治法用到了递归。   

在掌握了上述基本算法之后，要开始注意模式(pattern)的总结。比如，学会了归并排序(Merge Sort)，就要想办法把Merge相关的题目往这上面靠；学会了快速排序(Quick Sort)，那也试着去攻克quick select相关题目。对于分治法，除了递归类型的，我们也要掌握非递归类型的--比如在数组、矩阵和树当中进行二分查找。


### 3. 模板！模板！模板！
重要的事情说三遍。模板不一定是在一开始就总结的，但你可以在每种题型都刷了10-20题之后，总结你自己的模板。
比如 --

* 树类型的问题
  * DFS from top down
  * DFS from bottom up
  * BFS
  * Tree's construction
* Graph的问题
  * BFS
  * DFS
  * 染色法
  * 图的几种表示法
  * Union Find
  * Minimum Spanning Tree
  * Disjoint Sets
* DP 
  * Memorization
* Bineary Search
  * Modified Binary Search
* Two Pointers
  * Sliding Window
* Prefix Sum
* Stack & Queue
  * Monotonic Stacks and Queues
* Linked List related
  * Fast Slow Pointers
  
对于这些题型，好在LeetCode网站都对题目标记了Tag，你可以按照Tag专门来刷一类型，然后总结出自己的模板。  

### 4. 不要小看Easy题目
当你把步骤1和2的基本数据结构和基本算法的题都做10道这样，你就大概做了 `20 * 10 = 200` 道题目。那么，你再把各种数据结构和算法（加上稍难一点的数据结构和算法类型）再各自做10道题，你就练习了大概400题了。记住这个过程中别小看一些Easy题目，因为有些Easy题目其实是原本的Medium和Hard，只是随着Bar的增高而被重新归类为Easy；有的Easy其实是如果用任意方法解出是Easy，但如果要求一定要用Optimal Solution来解，就会成为Medium或者Hard；有的Easy是原始问题不难，但是跟进问题(Follow up)就会变成Medium或者Hard。总之，Easy难度的问题也是值得一做的，并且到后期你可以尝试一题多解。


### 总结

您还有什么要补充的刷LeetCode进FAANG的方法？如果YES，请留言，不吝赐教。

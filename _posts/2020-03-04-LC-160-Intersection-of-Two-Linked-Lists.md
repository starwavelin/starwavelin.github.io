---
layout:     post
title:      "LeetCode 160. Intersection of Two Linked Lists"
subtitle:   "LeetCode 160. 找出两个链表开始交叉的节点"
date:       2020-03-04
author:     "代码笔记哥"
header-img:
tags:
    - 线性解空间
    - Linked List
---

截止今天（美东时间3月4日晚），全美国新冠确诊达160例。根据一亩三分地网站的北美新冠疫情动态，第160例为新泽西州第1例，30+男性，现在在Bergen County医院住院中。这一例也离纽约市不远。

不论怎样，生活还要继续，我们来做一道题吧。就做LeetCode第160题。  
笔记哥是刚开始学Python，懂得不多，现学现卖，欢迎大家多提宝贵意见。

输入空间：线性 - 链表
解空间：线性

### 题目要求
找出两个链表开始交叉处的节点，返回该节点；假如两个链表没有交叉，返回None。
需要跟面试官确认的是，两个链表一旦开始交叉了，之后的所有节点就都相同了。

如图，两个链表的交叉处的节点为8。

### 思路
两个链表可能等长也可能不等长，但不论怎么样，我们都先要知道两个链表的长度。  
在我们知道了两链表的长度以后，用长的链表长度减去短的链表长度的差值，使我们得知要把长的链表从它的头向后走的步数。  
当长的链表向后走了这个“差值”步数以后，我把这称为两个链表现在在**同一起跑线**了。在这样的情况下，我们用一个while循环来同步比对两个链表的对应的两个节点。当我们遇到两个节点其实为同一个的情况的时候，将其返回即为所得。若一直无法遇到，则说明给出的两个链表并没有交叉。

### 代码
```python
from typing import List

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        if headA is None or headB is None:
            return None;
        lenA = self.get_length(headA)
        lenB = self.get_length(headB)
        if lenA > lenB:
            for i in range(0, lenA - lenB):
                headA = headA.next
        else:
            for i in range(0, lenB - lenA):
                headB = headB.next
        while (headA is not None and headB is not None and headA is not headB):
            headA = headA.next
            headB = headB.next
        return headA if (headA is not None and headB is not None) else None

    def get_length(self, head: ListNode):
        count = 0
        while (head != None):
            count += 1
            head = head.next
        return count
```

##### 相关的Python语言特性
1. （欢迎读者帮助确认我说的是否正确）在Python3当中，比较两个对象的内容是否相同用`==`，比较两个对象是否完全相同（即内容和内存占有皆相同，即是否为同一个对象），用的是英语单词`is`
2. Python的三元运算写法真特别，我一开始一直想用`return headA != None and headB != None ? headA : None`，但后来发现这是Java或TypeScript习惯，应该要用`return something if condition else some_other_thing`的写法，😓

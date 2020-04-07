---
layout:     post
title:      "LeetCode 1365. How Many Numbers Are Smaller Than the Current Number"
subtitle:   "LeetCode 1365. 数组中比当前数字小的数字的个数"
date:       2020-04-07
author:     "代码笔记哥"
header-img:
tags:
    - 线性解空间
    - Hash
    - Sorting
---

截止今天（美东时间4月7日傍晚），全美新冠确诊达39万5489例。
OK。冷静，做题。

数组中比当前数字小的数字的个数。  

输入空间：数组  
解空间：线性

解题“七步走” (保持这种sense)：  
1. 题意 Scenario
2. 假设 Assumptions
3. 举例与输入输出 Examples and figure out Input/Output
4. 思路（什么数据结构， 什么算法）Thinking Process (What data structure, algorithm?)
5. 代码 Coding
6. 复杂度分析 Complexity Analysis
7. 测试 Tests

### 题目要求
直接举例子讲。  
比如给你一个数组`[8, 1, 2, 2, 3]`。你可以发现，数组中比数字8小的数有4个，所以返回数组的第一个数为4；比数字1小的数为0个，所以返回数组的第二个数为0。以此类推，我们得到返回数组应该是`[4, 0, 1, 1, 3]`。注意，对于给定数组中的两个2而言，只有数字1比它们小，所以返回数组中有两个1。对于数字3而言，一共有[1, 2, 2]共3个数比它小，所以3在返回数组中对应的数为3，表示有3个数比它小的意思。

### 假设
面试人员告诉你，这题我们可以假定给定数组里面至少有两个数字。并且，给定数组里数字的取值范围在1到100之间。

### 举例与输入输出
已写在题目要求中。

### 思路1：利用哈希表
我们可以这么想，遍历数组一次，把每个数字出现的频率用哈希表记下来。所以，对于例子中的给出数组，我们就会有如下哈希表记录。
```
<8, 1> -- 数字8出现1次
<1, 1> -- 数字1出现1次
<2, 2> -- 数字2出现2次
<3, 1> -- 数字3出现1次
```
所以哈希表中的Key为给出数组中出现的数字，Value为该数字出现的频率。
然后，我们第二次遍历数组，这次遍历的时候，我们就把遍历到的当前数与哈希表中的key进行比对，当`key<当前数`的时候，我们就把count计数累加起来。这样就能得到每一个当前数所对应的比它小的数字的个数。

### 参考代码1
```java
public int[] smallerNumbersThanCurrent(int[] nums) {
  Map<Integer, Integer> map = new HashMap<>();
  for (int num: nums) {
    map.put(num, map.getOrDefault(num, 0) + 1);
  }
  for (int i = 0; i < nums.length; i++) {
    int count = 0;
    for (int key: map.keySet()) {
      if (key < nums[i]) {
        count += map.get(key);
      }
    }
    nums[i] = count;
  }
  return nums;
}
```
**时间空间复杂度**  
时间复杂度：这段代码由于有nested for loop，所以`O(n^2)`，  
空间复杂度：开了一个哈希表空间，其keys可能会有nums的个数规模，所以是`O(n)`。

### 思路2：复制数组并排序
我们可以想是否能用一个数组去记录下原来数组的每个数的索引，然后对这个新的数组进行排序。比如，`[8, 1, 2, 2, 3]`排好序后就是[1, 2, 2, 3, 8]。那么我们就容易发现，比数字8小的数字的个数恰好就是8的前面4个数，也就是8在新数组中的索引4。**在新数组中**,当遇到有相同数字的时候，比如新数组中的后一个2，我们就不直接用索引，而是把索引值递减到新数组中比2小的数，即数字1。数字1的个数作为比2小的数的个数。

### 参考代码
```java
public int[] smallerNumbersThanCurrent(int[] nums) {
  int[] sorted = Arrays.copyOf(nums, nums.length); // sorted 即为复制的新数组
  Arrays.sort(sorted); // 将新数组有序化
  for (int i = 0; i < nums.length; i++) {
    int position = Arrays.binarySearch(sorted, nums[i]);
    while (position > 0 && sorted[position - 1] == sorted[position]) {
      position--;
    }
    nums[i] = position; //答案可以存在给出数组中
  }
  return nums; //返回最终的经过变化处理的给出数组
}
```
**时间空间复杂度**  
时间复杂度：这段代码先是用了Arrays.sort()排序，`O(nlogn)`；而后又在遍历nums的过程中，每一次扫描都调用一个二分搜索，这一步时间复杂度为`n * logn = O(nlogn)`。所以综合起来时间复杂度为`O(nlogn)`。  
空间复杂度：复制了一个数组，其规模为nums的数字个数，所以是`O(n)`。

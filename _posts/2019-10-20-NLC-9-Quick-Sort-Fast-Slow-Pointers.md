---
layout:     post
title:      "NLC 9. QuickSort - Fast Slow Pointer Approach"
subtitle:   "复习快速排序（一）用快慢双指针来实现交换"
date:       2019-10-19
author:     "代码笔记哥"
header-img:
tags:
    - Sorting
---

### 文化背景
快速排序(QuickSort)是各种比较排序(冒泡排序、选择排序、插入排序、希尔排序、归并排序、快速排序)当中最快的一种。它是由英国计算机科学家托尼·霍尔(Tony Hoare)于1959年发明。这位托尼·霍尔于1980年获得图灵奖，目前是爵士头衔。下面给大家看看这位大牛的照片：

![oh-my-zsh](/img/in-post/20191020-quick-sort/Tony_Hoare.png)

除了快速排序，有名的快速选择(Quickselect)算法也是这位哥们发明的。当然啦，我们今天主要是讲(或者说和大家一起复习)快速排序。由于快速排序在实现的一些细节上，有多种不同的方法。根据本文章的标题，我这次侧重讲在快速排序的swap(交换)的过程中，如何运用快慢指针的方法。

也许您看到这儿有点懵，我还不知道快速排序怎么回事呢，这个“交换”又是快速排序里面的什么东东？不急，听我慢慢道来。  

### 举例与输入输出
输入：`[3, 5, 1, 2, 7, 6, 4]`  
输出：`[1, 2, 3, 4, 5, 6, 7]`   
条件：必须使用快速排序实现数组的排序  

### 算法原理
基本的算法原理，主要为三步走：
1. 从数组中挑出一个元素为基准(pivot)
2. 分区化(partition)：对数组进行重新排列，所有比pivot小的元素放到pivot的前面，所有比pivot大的元素放到pivot的后面。当这一过程结束后，pivot就会落在最终完全排好序的数组的正确位置。
3. 通过递归，对pivot前的数组与pivot后的数组再次执行步骤1和2，直到全数组都有序。

所以，那个“交换”的过程，是数组分区化过程中的一个关键步骤。本文章讲的是利用双指针法当中的一个快指针、一个慢指针，慢指针追赶快指针的方法，来寻找需要在分区过程中，交换的两个元素的位置。  

也为了更方便的讲解分区过程，本文中的快速排序的方法实现中的pivot的选择方面，不考虑“随机化pivot”这类花俏的算法，只举两种选择pivot的例子：1. pivot总选择待排序数组最左边的元素； 2. pivot总选择待排序数组最右边的元素。

### pivot总选待排序数组最左边元素的算法过程

![oh-my-zsh](/img/in-post/20191020-quick-sort/fast_slow_pointer_pivot_always_left.jpg)

### 代码实例1
```
public static void sort(int[] nums) {
  if (nums == null || nums.length == 0) {
    return;
  }
  quicksort(nums, 0, nums.length - 1);
}

private static void quicksort(int[] nums, int left, int right) {
  if (left < right) {
    int partitionIndex = partition(nums, left, right);
    quicksort(nums, left, partitionIndex - 1);
    quicksort(nums, partitionIndex + 1, right);
  }
}

private static int partition(int[] nums, int left, int right) {
  int pivot = left;  // here pivot means the index, not the element
  int i = pivot + 1; // i is the slow Pointer
  // j is the fast Pointer
  for (int j = i; j <= right; j++) {
    if (nums[j] < nums[pivot]) {
      swap(nums, i, j);
      i++;
    }
  }
  if (pivot != i - 1) {
    swap(nums, pivot, i - 1);
  }
  return i - 1;
}

private static void swap(int[] nums, int i, int j) {
  int tmp = nums[i];
  nums[i] = nums[j];
  nums[j] = tmp;
}
```

### pivot总选待排序数组最右边元素的算法过程



### 代码实例2


### 测一测
下面还提供了一段可以在Eclipse或其他Java语言IDE里面跑起来的代码片段，您只需要复制粘贴下面代码到与上面答案代码一起的同一个class当中，就可以跑起来，输入自己的测试样例，看看参考的答案代码是否正确。
```
public static void main(String[] args) {
	System.out.println("*** Welcome to Coding Bro's Quick Sort Test ***");

	Scanner sc = new Scanner(System.in);
	System.out.print("Input your integer array, leave each number by space: ");
	String[] strs = sc.nextLine().split(" ");
	int[] testArr = new int[strs.length];
	for (int i = 0; i < strs.length; i++) {
		testArr[i] = Integer.parseInt(strs[i]);
	}

	sort(testArr);
	displayResult(testArr);
}

public static void displayResult(int[] ret) {
	for (int element : ret) {
		System.out.print(element + " ");
	}
	System.out.println();
}
```

### 时间空间复杂度
**时间复杂度**：我们知道在最坏的情况下，快速排序可能退化为`O(n^2)`。这个`O(n^2)`的时间复杂度恰好会在数组本身有序的情况下产生。但，我们讨论快速排序的时候，往往是说其均摊的时间复杂度，那么，这个时间复杂度就是`O(n·log(n))`。  
**空间复杂度**：为递归栈的深度，所以是`O(log(n))`。

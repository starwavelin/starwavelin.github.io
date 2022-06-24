---
layout:     post
title:      "TS刷题常用API: Array"
subtitle:   "Commonly used TypeScript/JavaScript API for LeetCode - Array related"
date:       2022-05-28
author:     "代码笔记哥"
header-img:
tags:
    - 算法
    - JS
    - API
    - Extensible Note
---
WIP:   

### 前言
本文提供笔记哥用JavaScript/TypeScript刷题时的常用的Array相关的的API。    
方便阅读和快速理解，本文尽量提供这些API的中文注解。

### 1. 基于基础array [] 的操作
1. 往数组尾部增加元素
```js
arr.push(n);
```

2. 往数组尾部增加另一个数组的所有元素，但不是直接添加另一个数组，而是要另一个数组的元素都展开后加入
```js
// assume arr2 代表另一个数组
arr.push(...arr2);
```

3. 往数组中间插入一个元素
```js
arr.splice(insertIndex, 0, element);
```
举例：
```js
res.splice(insertPos, 0, newInterval);
```
在上面的parameters中，第二个parameter `0`是deleteCount。因为splice函数允许从insertIndex的位置开始，往后删除若干个元素，但由于我们这里不做任何删除，所以为`0`。  
此外，splice允许从插入位置开始，插入多个元素，比如：  
```js
arr.splice(insertIndex, 0, ele1, ele2, ele_n);
```
```js
arr.splice(insertIndex, 0, ...arr2);
```

4. 从数组头部删除并返回元素
```js
arr.shift(n);
```

5. 从数组尾部删除并返回元素
```js
arr.pop(n);  //这和 Stack相关的函数名称pop()刚好相同 
```

6. 有shift就有unshift， 从数组头部增加元素，相当于prepend
```js
arr.unshift(num);
```
从这里可以看出，JavaScript中的数组更像是一个双端队列deque，因为它的头尾都可以加减元素。



### 2. 基于基础array [] 的使用callback function的操作

1. 利用reduce()函数做数组内的元素求和
语法：
```js
return arr.reduce((pre, cur) => {
    return pre + cur;
}, initValue);
```
在遍历的过程中，`cur`是遍历到的当前元素，`pre`则为当前元素的前一个元素。所以在开始遍历数组的第一个元素时，`pre`的值即为`initValue`。  
应用举例：  
```js
return arr.reduce((pre, cur) => {
    return pre + cur;
}, 0);
```

2. sort排序，sort()内的callback function决定了排序法则  
**从小到大排序：**
```js
arr.sort((a, b) => a - b);
```
注意，有时在编译器中，若要对数组内的数值进行排序，这个callback函数是要明确写出来的，否则对一个正整数数组`arr`，`arr.sort()`得到的是原来的没有排序的结果。   
**从大到小排序：**  
只要把callback函数内的两个相减变量的顺序颠倒一下即可。
```js
arr.sort((a, b) => b - a);
```


### 3. 使用Array class的操作

1. 初始化某个固定长度的数组，并将其中的每个元素赋予一个初始值
语法：
```js
Array(len).fill(num);
```
举例：
```js
const arr = Array(ratings.length).fill(1);
```
规定`arr`是个长度与`ratings`的长度相同的数组，且数组内的每个值都初始化为1。


### 总结

您还有什么要补充的JavaScript/TypeScript刷题常用的Array类API吗？如果YES，请留言，不吝赐教。

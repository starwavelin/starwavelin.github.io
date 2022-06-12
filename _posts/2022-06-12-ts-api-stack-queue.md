---
layout:     post
title:      "TS刷题常用API: 利用Array构造Stack和Queue"
subtitle:   "TS: Implement Stack and Queue classes from Array"
date:       2022-06-12
author:     "代码笔记哥"
header-img:
tags:
    - 算法
    - TypeScript
    - API
---

### 前言
截止目前(2022年6月12日)笔记哥并没有发现TypeScript有自带的Queue或Stack class/interface供刷题或平常编程开发调用。    
当然，这也有可能是笔记哥上网查找得不够仔细；假如有发现TypeScript自带的Queue或Stack class/interface的朋友可以麻烦在评论区评论一下您的发现以及相关链接。    
好，下面就假定确实没有这样的Stack或Queue class，我自己利用TS有的Array及其相关方法来实现它们，供刷题和平日工作之用。   

### 1. 用Array实现Stack

```ts
export class Stack<T> {
    private items: T[] = [];

    constructor(items: T[]) {
        this.items = items;
    }

    push = (...items: T[]) => this.items.push(items)

    pop = () => this.items.pop()

    peek = () => !this.length ? undefined : this.items[this.length - 1]

    get length() {
        return this.items.length;
    }
}
```


### 2. 用Array实现Queue

```ts
export class Queue<T> {
    private items: T[] = [];

    constructor(items: T[]) {
        this.items = items;
    }

    enqueue = (...items: T[]) => this.items.push(items)

    dequeue = () => this.items.shift()

    peek = () => !this.length ? undefined : this.items[0]

    get length() { return this.items.length }
}
```


### 3. 小结

上面两个实现，至少有两个与Array相关的函数是可以补充在先前的《TS刷题常用API: Array》笔记里的。

1. 从数组头部删除并返回元素
语法：
```js
arr.shift(n);
```

2. 从数组尾部删除并返回元素
语法：
```js
arr.pop(n);  //这和 Stack相关的函数名称pop()刚好相同 
```

### 总结

您还有什么要补充的TypeScript刷题常用的与Stack， Queue相关的API或者应用吗？如果YES，请留言，不吝赐教。

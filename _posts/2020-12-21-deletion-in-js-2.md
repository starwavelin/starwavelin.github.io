---
layout:     post
title:      "九种从JavaScript数组删除元素的方法(下)"
subtitle:   "Remove elements form a JavaScript array: Part II"
date:       2020-12-21
author:     "代码笔记哥"
header-img:
tags:
    - JS
---
### 前言
上一篇“[九种从JavaScript数组删除元素的方法(上)](../../../../2019/11/16/deletion-in-js-1/)”，提供了4️⃣种删除JavaScript数组中的元素的方法。本篇来讲后面的5种方法。

### 1. 用数组的filter方法来“删除”特定元素
与上一篇提到的`splice()`方法有所不同，`filter()`方法不会改变原数组，但是会根据filter函数里面的条件，来返回一个新的数组。举例如下：
```js
const arr = [1, 2, 3, 4, 5, 6];
const filtered = arr.filter((value, index, arr) => {
    return value > 3; // 只有数组arr中大于3的元素，才符合filter的标准，会保留在新的filtered数组中;
    // 数组arr中元素小于等于3的，就会被“删除”，不会留在新的filtered数组中。
});

console.log(filtered); // [4, 5, 6]
```

### 2. 利用第三方工具包，比如lodash
虽然原生态的JavaScript并没有对数组的`remove()`方法，但是第三方库，比如`lodash`，是有的。使用lodash中的删除方法，关键要给出删除的条件；另外与上面的`filter()`方法不同的是，删除是对原数组的操作，所以删除后的结果会在原来的数组`arr`中体现。举例如下：
```js
const arr = [1, 2, 3, 4, 5, 6];
const evenDeleted = _.remove(arr, n => { //下划线“_”即为引入的lodash库
    return n % 2 === 0;
});
console.log(arr); //  arr数组变为[1, 3, 5]，原数组所有的偶数元素被删除
```

### 3. 我们自己写一个remove方法
假如我们不能使用lodash这样的包，我们可以怎么办？其实我们可以自己写一个从原数组arr中，根据特定条件进行remove的方法。这里面要用到上一篇提到过的`splice()`函数，以及callback函数（回调函数、回叫函数）概念。写法如下:

```js
function remove(arr, cb) { //arr即为原数组，cb是callback函数的签名(function signature)
    let i = arr.length;
    while (i--) {
        if (cb(arr[i])) {
            arr.splice(i, 1);
        }
    }
    return arr;
}
```

这段代码片段的核心点有两个：  
1. 我们从后向前用while循环来遍历arr数组，遇到符合删除条件的，我们就用splice删它。`splice(index, 1)`方法删元素的原理是：当前元素符合要被删除的条件时，删除它，把它后面的元素依次从右向左整一格。因此这也告诉我们为什么要用while循环从数组末尾向左遍历数组，因为这样即便有删除也会遍历原数组所有的元素，不会中途跳过某个元素。   
2. 代码片段的第4行：当回调函数的条件满足的时候，我们执行第5行的删除操作。  

下面再用两个例子来看看我们如何写这个回叫函数来实现我们要交给原数组的删除条件。  

例子1：删除数组中的偶数元素。
```js
function removeInCondition(element) {
    return element % 2 === 0;
}

console.log(remove([1, 2, 3, 4, 5, 6], removeInCondition)); //output: [1, 3, 5]
```

例子2：删除数组中数值为6的所有元素。
```js
const dataToDel = 6;
function removeInCondition(element) {
    return element === dataToDel;
}

console.log(remove([1, 6, 6, 4, 5, 6], removeInCondition)); //output: [1, 4, 5]
```

大家可以在Chrome浏览器的console里面跑一跑上面的例子，看看是否正确。

### 4. 利用delete operator
JavaScript自带的`delete`运算符，也可以用于某种意义上的删除数组元素，之所以说是某种意义上，是因为它的删除原理和`splice()`是很不一样的，我们先看一个例子，再说明不一样在哪儿。

```js
const arr = [1, 2, 3, 4, 5];
delete arr[3]; // delete element with index 3

//你觉得索引为3的那个元素，也就是数字4被删除了吗？

//我们看一下：
console.log(arr);
// output is: [1, 2, 3, empty, 5]
```

为什么output的结果显示原来的数字4变成了`empty`呢？  
原来，`delete`这个JavaScript运算符是不会影响原数组的长度的，它的主要职能其实是删除某个JavaScript对象中的特定的property。当然在JavaScript中一个数组也是对象类型，它就是把数组中的这个特定元素所占的内存给释放了，所以变成了`empty`。

所以，这个方法只是提供了一个JavaScript中删除数组中元素的思路，请根据你具体的编程要求来判断是否采用delete这个运算符。

### 5. 简单粗暴，重置数组
这个方法其实没什么太多说的，就是个抖机灵的方法。  
如果，你的requirement是，删除原数组中的所有元素，那么，你直接把原数组的句柄指向一个空数组，就得了。举例:

```js
let arr = [1, 2, 3, 4, 5];
arr = [];
console.log(arr);
// output is: []
```

### 总结

笔记哥个人认为，对于JavaScript中删除数组元素这个操作的9种方法，我们需要重点掌握 `pop()`, `shift()`, `splice()`, `filter()` 和那个自己写的方法。这其中，`splice()`方法更有其强大之处，比如本文里的自写方法就是基于`splice()`方法。其他的抖机灵的方法，大家知道一下会用就可以了。

针对“从JavaScript中删除数组元素”这个操作，您还有什么不同于这两篇推文所述的9种方法吗？如果YES，请留言，不吝赐教。

---
layout:     post
title:      "九种从JavaScript数组删除元素的方法(上)"
subtitle:   "Remove elements form a JavaScript array: Part I"
date:       2019-11-16
author:     "代码笔记哥"
header-img:
tags:
    - JS
---
JavaScript语言并不具备直接的类似`Array.remove()`这样的方法，但对于要掌握这门语言的工程师而言，它其实有多种多样的从数组中删除元素的方法。比如：我们可以使用`pop()`方法从数组的尾部删除元素，使用`shift()`方法从数组的头部删除元素，再者可以用`splice()`方法从数组的中间位置删除元素。另外，我们可以用`filter()`方法按特定的要求从数组中筛选出元素。

本文为“九种从JavaScript数组删除元素的方法(上)”，提供4️⃣种JavaScript数组的删除元素的方法。

### 1. 从数组尾部删除元素
从数组的尾部移除元素其实又分为两种方法，第一种是设定数组长度法，举例如下：
```
const arr = [1, 2, 3, 4, 5, 6]; // 数组arr原本的长度为6
arr.length = 3; // 设定数组的长度为3
console.log(arr); //  设定长度为3以后，数组arr变为[1, 2, 3]，即它原先的最后3个元素'4','5','6'被删除
```

第二种是使用`pop()`函数法。就这个方法，其实数组就相当于一个栈（数据结构:stack），我们把最后入栈的那个元素删除。所以，`pop()`函数法与“设定数组长度法”的相同之处在于，都是从数组尾部删除元素，不同之处在于，总是删除数组的最后**一个**元素。
```
const arr = [1, 2, 3, 4, 5, 6];
arr.pop(); // 调用这个函数会返回‘6’，即arr数组的最后那个元素
console.log(arr); //  现在，数组arr变为[1, 2, 3, 4, 5]，即它原先的最后那一个元素'6'被删除
```

### 2. 从数组头部删除元素
从数组头部删除数据可以用`shift()`方法。这个方法类似Java语言中的`dequeue()`方法。`shift()`方法只能删除数组的第一个元素。举例如下：
```
const arr = [1, 2, 3, 4, 5, 6];
arr.shift(); // 调用这个函数会返回‘1’，即arr数组的第一个元素
console.log(arr); //  数组变为[2, 3, 4, 5, 6]，它的第一个元素被删除
```
注意，如果原数组为一个空数组，那么调用`arr.shift()`后的返回值会是`undefined`。

### 3. 运用splice()方法从数组中间根据索引删除元素
上述的`shift()`方法只能删除数组的第一个元素，那假如我要删除数组的头两个元素，怎么办？这时候就需要用到`splice()`方法了。  
splice中文意思是移动，顾名思义，它相当于从某个位置开始，向后数几个元素，然后把数组后面的元素往左边移动几个位置，去覆盖原本的一些元素。所以，用`splice()`做从数组中删除元素的动作时，它带两个参数。第一个是要删除元素的**初始位置**，第二个是从要删除元素开始，你要删除元素的**个数**。  
比如上面说的我要删除数组的头两个元素，那么，要删除元素的初始位置（索引）就是0，要删除元素的个数就是2。示例如下：
```
const arr = [1, 2, 3, 4, 5, 6];
arr.splice(0, 2); // 调用这个函数会以数组为返回值类型，返回被删除的头两个元素 [1, 2]
console.log(arr); //  数组变为 [3, 4, 5, 6]，它的前两个元素被删除
```

既然这样，`splice()`给了我们更大的删除元素的灵活度，我可以从中间删除元素。比如，我想从上面的例子中，删除3，4，5这三个元素。
```
const arr = [1, 2, 3, 4, 5, 6];
arr.splice(2, 3); // 要删除元素3，所在的索引为2，然后我要从数字3开始，向后删除三个元素，那么就是 arr.splice(2, 3)
console.log(arr); //  数组变为 [1, 2, 6]，它的中间三个元素被删除
```

### 4. 改造splice()方法从数组中找出要删除元素的值并删除它
那么，假定一个整数数组中有且仅有一个数字5，我要把这个数字5从中删除掉，怎么办？根据我们上面所学，假定数字5所对应的索引为`i`,我们只需要遇到那个数字5的时候，调用`arr.splice(i, 1)`去删除它就可以了。举例如下：
```
const arr = [1, 2, 3, 6, 5, 7];
for (let i = 0; i < arr.length; i++) {
  if (arr[i] === 5) {
    arr.splice(i, 1);
  }
}
console.log(arr); // 数组变为 [1, 2, 3, 6, 7], 原先数组的数字5被删除
```

好的，今天就先介绍这四种从JavaScript数组删除元素的方法，我们下期见。
---
layout:     post
title:      "JavaScript 技巧笔记"
subtitle:   "JavaScript Tips"
date:       2019-02-17
author:     "codingbro"
header-img: "img/post-banner/post-bg-js.jpg"
tags:
    - JS
    - Extensible Note
---
Below are my personal notes on how to efficiently and smartly use JavaScript functions and features.

### filter()
#### 两对象类型数组比对后，根据数组1，去除掉数组2中与数组1相同的元素
Given `array1 = [{a:2, b:2}, {a:3, b:3}, {a:1, b:1}];`, `array2 = [{a:17, b:14}, {a:1, b:1}, {a:2, b:2}, {a:3, b:3}, {a:4, b:4}];`, we want the result to be `[{a:17, b:14}, {a:4, b:4}]`  

Solution:
```
const array1 = [{a:2, b:2}, {a:3, b:3}, {a:1, b:1}];
let array2 = [{a:17, b:14}, {a:1, b:1}, {a:2, b:2}, {a:3, b:3}, {a:4, b:4}];
array2 = array2.filter(item => {
  for (const oldItem of array1) {
    if (item.a === oldItem.a && item.b === oldItem.b) {
      return false;
    }
  }
  return true;
});

console.log('final array1:');
console.log(array1);
console.log('final array2:' );
console.log(array2);
```
![oh-my-zsh](/img/in-post/20190217-js-tips/filteroutcome.png)
思考🤔：为什么下面的方法会使得`array2`一直为empty array?
```
// The following give out array2 as [], think about why?
// array2 = array2.filter(item => {
//   return array1.forEach(oldItem => {
//     if (item.a === oldItem.a && item.b === oldItem.b) {
//       return false;
//     }
//     return true;
//   });
// });
```

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

#### filter() and find()
Goal: I want to find a property based on another property's value within the same element/object
比如：
```
const jsObjects = [
   {a: 1, b: 2},
   {a: 3, b: 4},
   {a: 5, b: 6},
   {a: 7, b: 8}
];
```
我需要找到`b=6`的时候`a`的值。  
**Solution 1: Use filter()**  
[fitler() official doc on mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)  
Basically, `filter()` applies to each element in the given array, and returns a new array.
```
const result = jsObjects.filter(item => {
  return item.b === 6;
})
```
Result is:
`[ { a: 5, b: 6 } ]`  

**Solution 2: Use find()**  
`find()` finds the 1st element of the given array. So,
```
const result2 = jsObjects.find(item => {
  return item.b === 6;
})
```
`result2` is: `{ a: 5, b: 6 }`

#### 对于callback function, it can be defined implicitly or explicitly
This not only applies to `filter()` but I just use it as an example.
For the examples above, they are `fitler(cb_implicit_definition)`. Below, let me show you an explicit callback definition and invoke it for filter() using the callback function's signature.  
```
// exists() is a function in SomeClass
static exists(value: any): boolean {
  return value !== undefined && value !== null && value !== '';
}

// below statement is from another class
const rawVersionArray = this.results.map(item => item.version).filter(SomeClass.exists);
```
运行结果就是， `rawVersionArray` will not have a version which might be `null`.

那，假如rawVersionArray contains repetitive versions, what shall I do?  
Do As:
```
const dedupedVersionArray = Array.from(new Set(rawVersionArray));
```

### 数据结构
自设数据结构`MapObj`  
```
export interface MapObj<T> {
  [key: string]: T;
}

// when Use, you would import something like
import {MapObj} from '../interfaces/MapObj';
```

### JavaScript 中的OR，AND短路运算
OR Operation: The focus is on the prior part. If the prior is valid then the whole thing is valid.（重点在前，前有则有）ie. `map[key] = map[key] || [];`  

Based on this, ternary operation can be further simplified using OR Short-Circuit
```
//Originally
return (result.alternativeName) ? result.alternativeName : result.key;

//Now
return result.alternativeName || result.key;
```

AND Short-Circuit
`(some falsy expression) && expr` is short-circuit evaluated to the falsy expression.



### “弱智”错误 | Very Silly Mistakes
1. Don't over curly braces an object  
Suppose we have `studentMap = {001: {key: '001', name: 'Zhang San'}}`, then we want to mock this object, we have
```
const student1 = Student.new();
student1.key = '001';
student1.name = 'Zhang San';
```
Then, we want to assign `student1` into `studentMap`. If we do
```
const studentMap = {
  001: {student1}
}
```
大错特错！ Cuz `studnet1` is over curly-braced. We should do
```
const studentMap = {
  001: student1
}
```
cuz a JavaScript object 自带 a pair of curly braces.

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

### "this" keyword
In the code snippets below, assume there are already controllers wrapping them, and “this” keyword refers to the controllers wrapping them.

**ES5 (ECMAScript 2009) Snippet**
```
var _this = this;
$('.btn').click(function(event) {
  _this.sendData();
});
```
即需要外面有个`_this`去引用`this`然后把`this`传递进入到`click()`函数内部的callback函数。

**`bind`: Another way of writing the same ES5 snippet and getting rid of “_this”**
```
$('.btn').click(function(event) {
  this.sendData();
}).bind(this);
```

**ES6 (ECMAScript 2015) Snippet**
```
$('.btn').click(event => {
  this.sendData();
});
```
通过arrow function免去了`bind(this)`.

注意：
1. `this` keyword in a static function may cause confusion. When invoking another static function within a function, use `ClassName.StaticFunction()`
2. In TypeScript, “this” can support polymorphism, for example:
`init(version: number): this` is better than `init(version: number): AConcreteType`

### .property vs. [‘property’]
When using TypeScript, type checking cannot work for `someObj[‘someProperty’]` so it is preferable to use `someObj.someProperty`.  
But when `stringVar` is not obvious, I still have to use `sombObj[stringVar]`

### Destructuring
The mozilla doc for [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)  
Note: for `const` variables, once defined must initialized, otherwise `Error:  Missing initializer in const declaration`

#### Destructuring + Tuple
The definition of [Tuple](https://en.wikipedia.org/wiki/Tuple)  

In my example, I have an array of old names and new names. Each old name is mapped to exactly one new name to form bijection. Then, I can define an array of 2-tuples, and use destructure assignment in a callback function.
```
const nameMappingArray = [
  ['non_biased_employee_incentive', 'employee_incentive'],
  ['non_biased_employee_name', 'employee_name'],
  ['non_biased_employee_salary', 'employee_salary']
];

await nameMappingArray.forEach(async ([x, y]) => {
  await updateOldNameToNewName(x, y);
})
```
Destructuring用在了`async ([x, y])`, `[x, y]`是对原来的array的表达。`nameMappingArray`是array套嵌array，大array中的每一个小array刚好都是包含两个元素x和y。`async ([x, y])`其实就是拿小array作为parameter。

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

解答：原来是因为要用`forEach` loop解此题的话，需要用一个变量来存`forEach`过程中得到的`boolean`值。如下：
```
array2 = array2.filter(item => {
  let res = true;
  array1.forEach(oldItem => {
    if (item.a === oldItem.a && item.b === oldItem.b) {
      res = res && false;
    }
  });
  return res;
});
```
以上解法可行，但由于`forEach` loop不能马上退出，一定要让`item`跟`array1`中的所有元素都比对完以后，才会给出个`res`的结果是真是假，这样就比再上面的`for-of` loop解法累赘了。此题建议用`for-of` loop解法。

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
The collections (map, sets and weak maps) are introduced since ES6 (ES2015).

### map()
`map()` applies to an array. `map()` method creates a new array with the results of calling a provided function on every element in the calling array. And, the resulting array will always be the same length as the original array.
```
const array1 = [1, 4, 9, 16];
// const multi = x => x * 3;
// pass a function to map
// const map1 = array1.map(multi);
const map1 = array1.map(x => x * 3);

console.log(map1);
// expected output: Array [3, 12, 27, 48]
```

#### map() + join()
以下是一个`map()`与`join()`连用的例子，得到的是一条string，string中的每一个名字之间都用单引号-逗号-单引号相连（主要用于写sql）。
```
const toQueryNames = nameMappingArray.map(([key, newName]) => newName).join('\', \'');
```

### reduce()
`reduce()`是我以前认为比较难掌握的一个函数，主要因为中文中对于reduce的解释是“减少”，后来查了字典，才知reduce也有“归纳为”的意思。在JS的语境中，将`reduce()`理解为“合并”会更有帮助。BTW，“[MapReduce](https://en.wikipedia.org/wiki/MapReduce)”是一种编程模型。

Just like `map()`, `reduce()` also runs a callback for each element of an array. What’s different here is that `reduce` passes the result of this callback (the accumulator) from one array element to another.

The `accumulator` can be pretty much anything (integer, string, object, etc.) and must be instantiated or passed when calling `reduce()`. "accumulator" 我将其翻译为“累加器”。

Now let me use an example from [poka-techbolog](https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d) to illustrate how to use `reduce()`

```
假设有一组飞行员信息如下：
var pilots = [
  {
    id: 10,
    name: "Poe Dameron",
    years: 14,
  },
  {
    id: 2,
    name: "Temmin 'Snap' Wexley",
    years: 30,
  },
  {
    id: 41,
    name: "Tallissan Lintra",
    years: 16,
  },
  {
    id: 99,
    name: "Ello Asty",
    years: 22,
  }
];
```

我要求他们的飞行年数总和：
```
const totalYears = pilots.reduce((accumulator, pilot) => accumulator + pilot.years, 0);
// 这里，accumulator是累加器，前面说了。pilot是当前的pilot信息，即当前object（有时是当前value）。0是starting value.
```

假如我现在要求拿到最有经验的那个飞行员的对象(to get the most experienced pilot data), how shall I do?
```
const mostExperiencedPilot = pilots.reduce((oldest, pilot) => {
  return (oldest.years || 0) > pilot.years ? oldest : pilot;
}, {});
```
理解这个版本的reduce的难点就在于，首先它不是在做加法运算。理解的突破口在于明白`reduce(callback)`函数中的callback函数中的curObject(这里为pilot)是在不断迭代的。第0位pilot为"Poe Dameron"，由于oldest还没有定义，所以（0 > 14）不成立，那么就由当前的这个第0位pilot "Poe Dameron"的信息赋值给`oldest`。迭代到第1位pilot "Temmin 'Snap' Wexley", (14 > 30)不成立，所以`oldest`更新为 第1位pilot "Temmin 'Snap' Wexley"的信息。依次类推。最后由于`oldest`始终为 第1位pilot "Temmin 'Snap' Wexley"的信息，返回这个对象即可。

#### 利用reduce()生成一个map对象
非常像上面的`reduce()`作用于pilots的第二个例子。要生成map对象，其starting value必须是`{}`。然后，就是要搞清楚accumulator。accumulator一开始是一个空的map。那么我们就要搞清楚累加规则是怎么回事。做map,每次累加的就是一对键值对。最后，每个当前的curObject从哪里来，当然是从要被reduce的array当中来啦。
```
const fruitMap = fruits.reduce((map: MapObj<Fruit>, fruit: Fruit) => {
  let key = fruit.key;
  if (key && typeof key === 'string') {
    map[key] = fruit;
  }
  return map;
}, {});
```
注意：不可忘记`return map;` statement。因为`reduce()`函数每作用一次当前对象，就要有一个返回对象去代替原来的accumulator。`reduce()`函数就是对这个返回对象进行累加。

同样是[poka-techbolog](https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d)，作者给出了连用`filter()`, `map()`和`reduce()`的例子，有时间看看吧。

### 数据结构
#### 自设数据结构`MapObj`  
```
export interface MapObj<T> {
  [key: string]: T;
}

// when Use, you would import something like
import {MapObj} from '../interfaces/MapObj';
```

#### Map型数据结构相关
##### TS中不可用`Object.values()`怎么办？  
比如在JavaScript中，我有
```
const fruitMap = {
	"apple": {key: "apple", taste: "sweet"},
  "orange": {key: "orange", taste: "sour"}
}
```
我想得到`[{key: "apple", taste: "sweet"}, {key: "orange", taste: "sour"}]`, 只需要`Object.values(fruitMap)`

现在，在TypeScript中，没有`Object.values()`功能，怎么办？  
也没关系，我们leverage `Object.keys() + map()`就可以了。 具体做法是：
```
Object.keys(fruitMap).map(key => fruitMap[key]);
```
即：先得到keys,再去map keys对应的value。

##### See if a key name is within a map object  
```
if (!(this.latestExamVersion in examMap)) {
  examMap[this.latestExamVersion] = ExamLookup.createExamMap(latestVersionedExamLookup.data);
}
```
总之，公式是`keyname in mapObj`

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
#### Don't over curly braces an object  
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

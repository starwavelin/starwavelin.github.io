---
layout:     post
title:      "TS刷题常用API: Map与Set"
subtitle:   "TS: Map and Set for LeetCode Problems"
date:       2022-06-26
author:     "代码笔记哥"
header-img:
tags:
    - 算法
    - TypeScript
    - API
---

### 前言
类似Java的HashMap与HashSet，TypeScript中也有对应的`Map`和`Set`类。  
本文主要提供TypeScript中Map和Set类中可以用于刷题的主要方法。  
但在开始前，我们先来看下历史上TS/JS中常被用来当做Map用的类 -- Object。  


### 1. Object与Map的联系与区别

联系：  
- Object is similar to Map that allows you to
  - set key-value pairs
  - retrieve those values
  - delete keys
  - detece whether something is stored at a given key
  
区别：
- Object has a prototype so it has default keys; Map doesn't.
- The keys of Object are strings, yet there is no type limitation for the keys in Map.
- To get a size of an Object, you have to use something like `Object.keys(obj).length`, but for Map you can simply use `map.size` property.

Reference:  
https://stackoverflow.com/questions/18541940/map-vs-object-in-javascript


### 2. 假如用Object当做Map来刷题
##### 1. Shallow copy of obj, spread and Object.assign() 两种方法  

```ts
const person = {
    firstname: 'coding',
    lastname: 'bro'
}

// using spread
let p1 = { ...person };

// using Object.assign
let p2 = Object.assign({}, person);
```

在shallow copy的情况下，假如我做出 `p1.firstname = 'haha'`， `person`中的firstname会发生改变吗？  
答案是不会。原因是`person` object中的propery的值是primitive type具体在这个例子里是string类型，所以是被完全复制一份到了`p1`，然后`p1`修改它的firstname不会影响到`person`。   
但假如`person` object中的propery的值是对象类型，那么shallow copy后, `person` object中的propery是被复制一份到`p1`, 但这个property的值，也就是那个对象，是由`person` 和 `p1`的对应的同名property共享的。 假如，`p1`对`firstname`property之下的某个property进行操作，`p1`的这个操作就会在`person`中反映出来。   

Referecne:   
https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy


##### 2. Deep copy of obj, 假定obj is serializable  

```ts
let p3 = JSON.parse(JSON.stringify(person));
```

Reference:  
https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy


##### 3. 其他主要的object下使用的方法   

```ts
/* Set a key-value, get value from a key */
person[firstname] = 'someFirstName';
person[firstname]

Object.entries(person)  //[ ['firstname', 'coding'], ['lastname', 'bro'] ]

Object.keys(person) //  ['firstname', 'lastname']

Object.values(person)   //  ['coding', 'bro']

person.hasOwnProperty('firstname') // true

/* Loop through object */

for (let key in person) { } // this for...in loop is not preferred b/c it loops through the properties in the prototype chain as well

for (let key of Object.keys(person)) { }

for (let val of Object.values(person)) { }

for (let entry of Object.entries()) {
    console.log(entry[0], entry[1]) // entry[0] - key, entry[1] - value
}

for (let [key, value] of Object.entries(person)) { 
    console.log(`${key}: ${value}`)
}
```


### 3. Map及其方法的若干使用
##### 1. Create a map   

```ts
let map = new Map<number, number>(); // 设定一个key 与 value类型皆为number的Map

// Create a map with initial values
let map2 = new Map<string, number>([
    ['key1', 101], 
    ['key2', 102]
]);
```

##### 2. Add, Retrieve, Delete entries from Map  

```ts
map.set(key, val)  // adds a new entry in the map

map.get(key)      // retrives the value for a given key, if the key doesn't exist, return undefined

map.has(key)

map.size

map.delete(key)   // deletes a key-value pair using its key. If key's found and deleted, return true; ow. return false

map.clear()     // delete all entries from the map
```

##### 3. Iterating over Map  

```ts
map.keys() // to iterate over map keys
map.values() // to iterate over map values
map.entries() // to iterate over map entries
map // use object destructuring to iterate over map entries

// 跟iterating through object的写法基本没差 -- 也是4种, 无非就是每一种都用 for...of loop
for (let key of map.keys()) {}

for (let val of map.values()) {}

for (let entry of map.entries()) {
    console.log(entry[0], entry[1])
}

for (let [key, value] of map) { 
    console.log(`${key}: ${value}`)
}
```

### 4. Set及其方法的若干使用
##### 1. Create a set  

```ts
let set = new Set<number>(); 

// Create a set with initial values
let set2 = new Set<number>([101, 102]);
```

##### 2. Add, Retrieve, Delete elements from Set  

```ts
set.add(val)  // adds a new value into the set; if the val already exists then it won't be added. Return the set object with added value (or not)

set.has(val) // check if a val exists in the set

set.size

set.delete(val)   // deletes the val from the set. Return true if found and deleted; ow. return false

set.clear()     // delete all values from the set
```

##### 3. Iterating over Set  

```ts
for (let val of set) {}

set.forEach(val => {
    // deal with value
})
```


### 总结

您还有什么要补充的TypeScript刷题常用的与Map， Set相关的API或者应用吗？如果YES，请留言，不吝赐教。

---
layout:     post
title:      "Java刷题常用API之 HashMap, HashSet"
subtitle:   "Commonly used Java API for LeetCode - HashMap HashSet"
date:       2022-05-21
author:     "代码笔记哥"
header-img:
tags:
    - 算法
    - Hash
    - API
---
### 前言
本文提供根据笔记哥个人刷题经验的常用的HashMap、HashSet之下的Java API。  
方便阅读和快速理解，本文尽量提供这些API的中文注解。

### 1. HashMap类常用API

#### 基本操作   
```java
int size(): //返回HashMap中键值对(<key, value> pairs)的个数

boolean isEmpty(): //判断HashMap是否为空

V get(Object key): //通过给定key去获取对应的值，有对应值则返回值，无对应值则返回null
```

#### 针对key的一些操作  
```java
boolean containsKey(Object key): //判断HashMap是否含有给定的key

Set<K> keySet(): //将HashMap中的所有keys转化为一个集合 （因为keys是不能重复的，所以包含所有keys的collection必然是一个集合）

V remove(Object key): //假如key存在于map中，则删除这个key和其value形成的键值对，并返回value；假如key不存在于map中，返回null
```

#### 针对value的一些操作（这就多了）  
```java
V put(K key, V value): //把<key, value>键值对放入到HashMap里；如果HashMap里已经有一个由给定key对应的value，则方法中的新value取代那个旧value。注意，这个方法返回值是给定的 value

V putIfAbsent(K key, V value): //注意这个方法跟上面一般put方法的区别。这个方法是说：如果给定的key不在map当中，或者给定的key虽然在但其对应值为null，那么我们把这个键值对或者方法中的那个值value放到对应的key那里；这时候方法返回值为null。但如果给定的key已经有了一个不为null的值，那么不对已有的键值对做出改变，方法返回给定key对应的已有的值。

V getOrDefault(Object key, V value): //注意这个方法跟上面的一般get方法的区别。这个方法是说：返回map中key所对应的那个值，但假如key并不存在于map中，放回方法里的默认value.

boolean containsValue(V value): //查看map中是否包含给定的值

Collection<V> values(): //returns a Collection view of values contained in the given map. 这里的Collection是可以用特定类型来Cast的，举一个例子：return new ArrayList<List<String>>(map.values()); 这里的ArrayList<List<String>>就是具体化的Collection<V>
```

#### 针对<key, value>键值对的操作    
```java
Set<Map.Entry<K,V>> entrySet():
```

这是将给定的map转化为一个由其Entries组成的Set view。主要用于遍历一个hashMap 下面举一个例子:  
```java
for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
    // 针对遍历到的每一个entry进行操作...
}
```

#### 刷题应用举例
```java
for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
    // 针对遍历到的每一个entry进行操作...
}

for (int stop : routes[i]) { 
    map.putIfAbsent(stop, new HashSet<>());
    map.get(stop).add(i); 
}

// need to return List<List<String>>:
// the type of map.values() is Collection<List<String>>, convertion is needed:
return new ArrayList<List<String>>(map.values()); // convert
```


### 2. HashSet类常用API
* 我们可以把HashSet看成是一种特殊的HashMap<key, value>, 只是这里面的value总为一个固定值，比如为1.
* HashSet保证了其承载的元素各不相同，想想高中数学里“集合”的定义
  
```java
boolean add(E e): //把给定的元素加入到set中，成功加入返回true，否则返回false

void clear(): //删除set中的所有元素

boolean contains(E e): //判断set中是否包含元素e

boolean isEmpty(): //判断set是否为空集

boolean remove(Object o): //若对象o在set中，则将其删除并返回true

int size(): //返回set的大小
```


### 总结

您还有什么要补充的JAVA刷题常用的HashMap、HashSet类API吗？如果YES，请留言，不吝赐教。

---
layout:     post
title:      "RESTful API之\"四大要素\""
subtitle:   "The Four Properties of RESTful API"
date:       2020-01-05
author:     "代码笔记哥"
header-img:
tags:
    - 系统设计
---
RESTful API是什么？如果您上网谷歌搜索关键字“Restful API wiki”，对应找到的维基百科页面是关于“Representational state transfer”的；我给它翻译作“表现性的状态转移”。即便译成了中文，读来还是有点拗口难解。其实，对于常常在实际开发中去设计RESTful API的程序员来讲，不大需要非常深入的去知道什么是表现性的状态转移。我们的核心任务是：设计好Restful API。

基于此，本文就不咬文嚼字的从学术论文角度去理解Restful API是什么，而是从四个要素来帮助读者朋友理解Restful API。

### 要素1. 资源（Resource）
在Restful API设计的语境中，对资源的最直白的理解，就是找出那个“东西”。而这个“东西”，就是隐藏在API设计中可能涉及到的名词。

举例来讲，这个资源可能是一个文件、图片、刷题网站上的一道题目、临时服务、一系列的其他资源等等。用英语来说，就是：We can basically view a Resource as a thing, or any noun that can be found in RESTful API. For instance, we can say a document, image, a problem on LeetCode, temporal service, a collection of other resources, or a non-virtual object is a resource.

所以，“资源”这个概念可以被理解为程序员设计的超文本中索引的那个目标；在概念上这个资源会对应一系列的实体。

比如，API `leetcode.com/problems/`, 这里面的资源就是"problems"，它对应的是一系列的编程面试问题。

### 要素2. 表现性（Representational）
在Restful API概念中，表现性指的是如何去描述一个资源。在网络通信当中，表现性则更多的是指我们使用哪一种**范式**去描述一个资源。目前常见的两种范式就是`XML`与`JSON`。

大家看看下面这个HTTP Header的例子：
```
GET /api/datacenters HTTP/1.1
Accept: application/json
```

这是一段由客户端发往服务器端的HTTP GET请求。其表现出来的意思就是：服务器啊，请你告诉我你的数据中心(datacenters)在哪儿，请用JSON的格式把你的数据中心描述给我看哦。

而今，JSON这种表现范式较XML更为青睐。它胜出的原因是：它比`XML`字节少，更省（网络传输时要消耗的）资源。

### 要素3. 状态转移（State Transfer）
我们从客户端向服务器端发请求，无非就是要在服务器端进行`增删改查`这四种操作。所以，状态转移这个概念也很好理解。说白了，就是“增、删、改”这三种操作。因为这三种操作会使得资源被添加、被减少、或者被修改。资源的这些变化就叫做“状态转移”。

### 要素4. 无状态 (Stateless)
“状态转移”那个要素我笔墨比较少，但我想重点讲讲“Stateless(无状态)”是怎么一回事。

Stateless其实是针对服务器端(server)而言的，指的是服务器端不保存客户端(clients)的状态。我们还拿LeetCode网站来举例吧，先给大家看看有状态（Stateful，即不是Restul API）的API大概长什么样：

```
leetcode.com/profile
```
这个API就要求服务器记录用户端的状态，张三登录后LeetCode服务器就要给出张三的profile，笔记哥登录了服务器就要给出笔记哥的profile。 服务器是分别记住了每个来访者是谁，从而给出了相应的profile。

在笔记哥登录后过了一段时间，笔记哥的session就会过期。过期以后，Server就会忘了笔记哥是谁，从而要求我要重新log in（登录）。但在我登录后的某个短时间之内，Server是记得我是谁的。这就叫做是Stateful，是Stateless的反义词哦。

好，那今天的LeetCode网站是Stateful的API来给出用户的Profile吗？我给大家看看下面的图片：

![oh-my-zsh](/img/in-post/20200105-restful-api-1/leetcode-profile.png)

显然，LeetCode已经进化到使用RESTful API，其用的是笔记哥的用户名(codingbro)，而不是泛指的`/profile`。在这种情况下，这个URL `leetcode.com/codingbro`就是一个stateless的URL。服务器**不需要**（不代表完全不记录，这里暂不展开讲）去记录当前请求的用户codingbro是谁。

所以总结下，Stateless主要指如下三个方面：
1. 服务器端不记录访问用户状态；
2. 客户端要记录访问用户状态； 
3. 最重要的：服务器端单凭每个请求的信息就足以处理这个请求。


好的，本期就给大家介绍了RESTful API的四要素：资源、表现性、状态转移以及无状态。下次有机会，笔记哥想给大家分享下什么算“好的RESTful API设计”。
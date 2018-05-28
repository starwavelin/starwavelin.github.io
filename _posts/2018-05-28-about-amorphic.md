---
layout:     post
title:      "关于Amorphic"
subtitle:   "About Amorphic (Chinese Edition)"
date:       2018-05-28
author:     "starwavelin"
header-img:
tags:
    - Node
    - 前端
    - 框架
    - 翻译
---
Amorphic: 一个持久化同型的Node.js的前端到后端开发框架。

英文原文：[http://selsamman.github.io/amorphic-docs/](http://selsamman.github.io/amorphic-docs/)

### 欢迎来到 Amorphic
Amorphic 是一个用于Node.js网站开发的全栈同型(isomorphic)框架。

其目标是让你可以专注于业务逻辑并在如下方面投入较少时间而达到目的：

- 代码在哪儿被执行 - 代码无论在浏览器或是服务器被执行都是无缝衔接的被调用。
- 跟数据库打交道 - 对象以及它们之间的关系可以被自动存储和读取。您可以使用MongoDB或基于knex技术支持的数据库（如 Postgres）
- DOM (文件对象模型 Document Object Model) 如何工作 - 双向绑定意味着无需胶水代码

### 工作原理
你定义那些同时存活在(live on)浏览器端和服务器端的对象作为用户与服务器会话([Session](https://en.wikipedia.org/wiki/Session_(computer_science)))的一部分。你的对象方法要么定义在浏览器端执行要么在服务器端执行。你可以从浏览器端的方法去调用服务器端的方法。当你这么做的时候，所有对象的属性被同步化(synchronized)且你的方法调用是在服务器端执行。关键点在于，基于速度、是否要接近持久化存储工具或者是安全等因素，你来决定你的代码在什么地方执行（客户端或服务器端），且你的代码结构和风格无需变化（单单读取服务器端资源的代码有所例外）。

To keep track of all this you need to define your objects using Amorphic’s templating system which lets you define object, their properties and relationships to other objects. As a bonus this definition also serves as the core a database schema that is lightly augmented with an external schema file to take care of data base dependent considerations like object to table mappings and foreign keys. You can save and and retrieve objects and their relationships to any depth with a simple call with full ACID support if Postgres is chosen as the database.

Finally mapping your objects to the screen uses data-binding that is analogous to Angular except that it has tighter integration with your object definitions. For example you can define values and descriptions for a multi-valued property as part of your object template, bind that to a select control and it will automatically populate the options.

**版权声明：以上内容为代码笔记哥（Coding Bro）翻译。转载请添加这句话以及原文链接starwavelin.com/2018/05/28/about-amorphic/**

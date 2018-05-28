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

- 代码在哪儿被执行 - 代码无论是在浏览器端或是服务器端被执行都是无缝衔接地被调用。
- 跟数据库打交道 - 对象以及它们之间的关系可以被自动存储和读取。您可以使用MongoDB或基于knex技术支持的数据库（如 Postgres）
- DOM (文件对象模型 Document Object Model) 如何工作 - 双向绑定意味着无需胶水代码

### 工作原理
你定义那些同时存活在(live on)浏览器端和服务器端的对象作为用户与服务器会话([Session](https://en.wikipedia.org/wiki/Session_(computer_science)))的一部分。你的对象方法要么定义在浏览器端执行要么在服务器端执行。你可以从浏览器端的方法去调用服务器端的方法。当你这么做的时候，所有对象的属性被同步化(synchronized)且你的方法调用是在服务器端执行。关键点在于，基于速度、是否要接近持久化存储工具或者是安全等因素，你来决定你的代码在什么地方执行（客户端或服务器端），且你的代码结构和风格无需变化（单单读取服务器端资源的代码有所例外）。

为了时刻追踪这一切，你需要使用Amorphic的模板系统来定义对象。这个模板系统让你可以定义对象、对象的属性以及对象间的关系。另有个加分项是，这类定义也作为一类数据库模式的核心为其服务。这类数据库模式是使用外置的Schema文件来管理诸如对象与数据库表的映射、外键等数据库依赖关系的考量。如果Postgres是您使用的数据库，您只需用一个很简单的调用加上ACID（原子性、一致性、隔离、持久）支持就能实现到任一深度的对象及对象间关系的存储与读取。

最后，将你的对象映射到前端视图用的是类似于Angular的数据绑定技术。与Angular不同的是，我们Amorphic用的技术对你定义的对象有更紧密的集成。举例来讲，你可以定义值和描述作为一个多值的(multi-valued)属性，且将这个属性作为你对象模板的一部分。而后你将这个对象模板绑定到前端视图的一个下拉菜单元件，这个下拉菜单元件就会自动的被填充上所有选项值了。

### 模型、视图、控制器

![mvc-amorphic](https://github.com/selsamman/amorphic-docs/blob/gh-pages/img/mvc.png?raw=true)

Amorphic 是基于MVC模式设计的
* 模型(Model) - 用于表达你的数据和数据库中的模型的对象
* 视图(View) - 以数据绑定或Directive的形式将HTML映射到你的模型中的属性或者是控制器
* 控制器(Controller) - 起到你的session的作用。同时也提供数据绑定到视图的根域(root scope)。你可以构造更具粒度性(granular)的控制器来实现模块化。

以下 Amorphic 的部件是对这种MVC结构的支持：
* 超级类(Supertype) - 这是一个可以支持丰富定义对象、对象属性、对象间的关系且具有传统的继承关系(inheritance)支持的类系统。正是因为Amorphic对你的数据有具体的了解，它才能够实现浏览器端与服务器端的同步化来持久化你的数据。
* Semotus - 这是浏览器端与服务器端传输与同步化的机制。
* 绑定器(Bindster) - 这是数据绑定和包含了路由功能的模板系统。
* 持久器(Persistor) - 这是能让你的数据持久化且管理数据的读取的对象关系映射或者非关系型映射(如 MongoDB)工具。

**版权声明：以上内容为代码笔记哥（Coding Bro）翻译。转载请添加这句话以及原文链接starwavelin.com/2018/05/28/about-amorphic/**

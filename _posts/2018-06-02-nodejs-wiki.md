---
layout:     post
title:      "Node.js维基百科页面翻译"
subtitle:   "The Chinese Version of Node.js Wikipedia Page"
date:       2018-06-02
author:     "starwavelin"
header-img: "img/post-banner/post-bg-nodejs.jpg"
tags:
    - Node
    - 翻译
    - Extensible Note
---
Node.js是我在下一阶段工作中要大量用到的JavaScript语言的服务器端运行环境。和上一篇博文一样，本翻译的主要目的是让自己对这个运行环境有一个概览，并不刻意添加Node.js在中文使用地区（中国大陆、香港、台湾、新马等地）的情况。
本翻译参考版本为2018年6月2日读取的
[https://en.wikipedia.org/wiki/Node.js](https://en.wikipedia.org/wiki/Node.js)。英文人名、地名、公司名等不刻意翻译，谢谢。

**以下为翻译正文**

Node.js是一种开源跨平台的JavaScript运行环境。该运行环境可以在服务器端执行JS代码。历史上，JavaScript主要是做为客户端脚本语言，用于嵌入到网页HTML当中并在用户的浏览器端运行。Node.js让开发者可以在服务器端写可执行的JavaScript代码使得在将网页发送到用户的浏览器之前就能生成动态的网页。如此，Node.js就成了“JavaScript处处存在”的范式，将整个网站的前后端开发都整合成了单一的语言--JavaScript。

尽管```.js```是传统上的JavaScript代码的扩展名，“Node.js”这个名字并不是指某个特定的JavaScript文件，而是单指这个叫“Node.js”的产品。Node.js的事件导向型架构利于它处理异步IO（异步化的输入输出）。这些个在设计上的选择的目的是要优化网站程序使之能很好的处理高IO吞吐量的请求、高规模的扩展性，以及很好的服务于实时性的网页程序（比如，实时的信息交流系统，网页浏览器端游戏，等等）。

Node.js的分布式的开发项目是由Node.js基金会来运作的。这个基金会是由Linux基金会帮助建立起来的。

使用Node.js的有名公司如下：GoDaddy，Groupon，IBM，领英，微软，Netflix，PayPal, Walmart, 雅虎等等。

- [历史](#历史)
- [概览](#概览)
  - [平台架构](#平台架构)
  - [业界支持](#业界支持)
- [发布](#发布)
- [技术细节](#技术细节)
  - [线程](#线程)
  - [V8](#v8)
  - [包管理](#包管理)
  - [联合API](#联合api)
  - [事件循环](#事件循环)
- [项目管理](#项目管理)

### 历史
2009年 Ryan Dahl 发明了Node.js。其发明的背景如下：

当2009年Node.js被发明出来时，距离上一个（也是第一个）服务器端的JavaScript运行环境被开发出来已经过去13年了。世界上第一个服务器端的JS运行环境是1996年网景公司开发的LiveWire Pro Web。回到Node.js这个话题。Dahl开发Node的灵感源于一次在Flickr上观看文件上传的进度条。由于浏览器无法得知文件的多大比例已经上传完成，所以为准确显示进度条进展过程，浏览器要不断的给后端服务器发请求。Dahl觉得这个方法太low了，应该要有更好的方法。此外，Dahl也批评当时很流行的阿帕奇HTTP服务器的局限性。阿帕奇服务器至多处理10000+的并发连接请求，超标了就会有雪崩效应。这是因为阿帕奇服务器对每进来一个请求就开一个线程，线程之间是阻塞的（一个线程在占用IO资源时，其他线程要等待）。

*维基百科没有写 Dahl 如何努力地开发出了Node.js。话锋一转，便是*

2009年11月8日，Dahl将他的Node.js项目在欧洲JavaScript大会上进行了展示。Node.js是结合了谷歌的V8 JavaScript引擎、一个事件循环队列以及一个低级别的IO API。

2010年1月：Node.js引进了包管理系统```npm```

2011年6月：微软和Joyent实现了原生Windows版Node.js

2012年1月：Dahl退居二线，让他的同事也是npm的发明者Isaac Schlueter管理Node项目。

2014年1月：Isaac Schlueter宣布由Timothy J. Fontaine接管Node项目。

中途杀出个程咬金，叫io.js, io.js是fork node.js项目得到的。

2015年9月，Node.js v0.12版本与 io.js v3.3版本合并为Node v4.0版本。这次合并使得V8引擎JavaScript ES6的功能被添加入Node.js，并进入了Node长期支持版的开端。

至2016年，io.js的官方网站推荐开发者选用Node.js并告诉开发者以后将不再有新的io.js发布--因为已经跟Node.js合并了嘛。

### 概览

_今天先翻译到这里 2018/6/2 4:09pm_

Node.js allows the creation of Web servers and networking tools using JavaScript and a collection of "modules" that handle various core functionality.[28][31][44][45][46] Modules are provided for file system I/O, networking (DNS, HTTP, TCP, TLS/SSL, or UDP), binary data (buffers), cryptography functions, data streams, and other core functions.[31][45][47] Node.js's modules use an API designed to reduce the complexity of writing server applications.[31][45]

Node.js is officially supported on Linux, macOS, Microsoft Windows, SmartOS, FreeBSD, and IBM AIX.[3] The provided source code may also be built on similar operating systems or be modified by third parties to support others such as NonStop[48] and Unix servers. Alternatively, they can be written with CoffeeScript[49] (a JavaScript alternative), Dart or TypeScript (strongly typed forms of JavaScript), or any other language that can compile to JavaScript.[49][50]

Node.js is primarily used to build network programs such as Web servers.[44] The biggest difference between Node.js and PHP is that most functions in PHP block until completion (commands execute only after previous commands finish), while Node.js functions are non-blocking (commands execute concurrently or even in parallel,[51][52] and use callbacks to signal completion or failure).[44]

#### 平台架构

#### 业界支持

### 发布
原文 [https://en.wikipedia.org/wiki/Node.js#Releases](https://en.wikipedia.org/wiki/Node.js#Releases) 中有个图表总结了Node的每一期发布。笔者就不赘述翻译了。笔者查了下，自己机器上的Node版本为v8.9.4，属于Carbon系列。查Node版本的命令```$ node --version```
### 技术细节

#### 线程

#### V8

#### 包管理

#### 联合API

#### 事件循环

### 项目管理


**版权声明：以上内容为代码笔记哥（Coding Bro）翻译。转载请添加这句话以及原文链接starwavelin.com/2018/06/02/nodejs-wiki/**

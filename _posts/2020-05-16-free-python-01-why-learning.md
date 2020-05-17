---
layout:     post
title:      "免费Python小课01：为什么要学习编程"
subtitle:   "Free Python Course 01: Why learning programming?"
date:       2020-05-16
author:     "代码笔记哥"
header-img:
tags:
    - Python
    - 教程
---
### 上一节课
[免费Python小课00：搭建Python的开发环境](https://mp.weixin.qq.com/s/7ZHzkRseMwVl1XfiiGSSxg)

### 前言
笔记哥提供的这个免费Python小课，是开发自美国密歇根大学(University of Michigan)的 **“为每个人准备的Python” (Python for Everybody)** 课程，并加入了笔记哥从网上搜集到的其他一些Python学习材料和素材，以及一些适合中文学习者的文化背景元素。所以，这个课程自然是中文讲解啦，适合一位毫无编程经验的愿意了解编程的人士开始学习。当然，目前这个课程可能不太适合小朋友，因为此课程暂不包含游戏编程这个模块。但假如一位小朋友不介意听到“变量”“表达式”“函数”这类词汇，我很欢迎小朋友也来看我的Python教程，并提出你的宝贵意见!

好嘞，言归正传，目前计划这个教程分为五个大的模块：  
I. Python基础  
II. Python数据结构  
III. 用Python爬取网页数据  
IV. Python连接数据库  
V. 数据可视化  

其中，第一部分“Python基础”包含五个章节：
1. 为何学编程 (Reasons you should learn programming)
2. 变量、表达式和语句 (Variables, expressions, and statements)
3. 条件执行 (Conditional execution)
4. 函数 (Functions)
5. 迭代 (Iterations)

这篇文章就来讲讲第一个章节：  
`为何学编程 （Reasons you should learn programming）`

### 创意与动机
很多人认为学习编程需要有很强的创意感，比如你必须是一个从小就喜欢拨弄东西甚至搞点小发明的人。对这样的说法，笔记哥认为不完全正确。诚然，如果你是一个很热爱搞点小发明的人，那我认为你在学习编程方面十有八九就有天赋。但假如你不是这样的人，而你仍然可能被手机上的APP所迷住，比如美图秀秀、抖音、饿了么等等。似乎一打开手机，每一个APP都在对你默默呐喊“点我吧”，“点我吧”。然后，你对你所常用的APP的功能翻了个底朝天，你的脑子里始终萦绕着要自己写一个帮助自己生活的APP的念想。那么，我认为你就是位有一定创意的朋友，值得跟着这门课一起学习一个编程语言，帮助你构建编程的基本框架和概念。

![apps](/img/in-post/20200516-free-python-01/apps.png)
<small class="img-hint">呐喊"点我吧"的APP们</small>

另一方面，动机也是你能持续学习这门课的重要因素。想必读者朋友们大部分是成年人了，没有人会逼着你去学习什么新生事物，比如编程。但是，也许你知道目前不论在中国还是美国，编程方面的工作总是不缺机会。特别是在新冠疫情的这段时间，美国有很多的公司企业裁了员，但美国的几个科技巨头公司却岿然不动，不怎么受疫情的影响。类似的，想必国内的BAT等大公司，相比于制造业、餐饮业、旅游业等行业，受影响的层面较小。所以，我们如果坦然从金钱和寻求更好生活的职场跑道的角度来考虑，用一些时间来学习这门免费的Python课程，今儿换到可能的职场前景（不需要转行做程序员，比如你可以在现有工作中利用Python做些数据分析，高效完成工作指标），是否是一个不错的投资呢？

### 计算机组成的简要科普
说到这里，我们就先来看看我们用于编程的机器，也是我们大部人日常接触的电脑，从架构上可以分为几个部分。我们所写的程序，又是在电脑中的哪些部分运作的。

先给大家看一张简要的电脑硬件组成图：

![apps](/img/in-post/20200516-free-python-01/simple-architect.png)
<small class="img-hint">图片来自《Python for Everybody》一书，作者 Dr. Charles R. Severance</small>

由于现代计算机最早起源于美国（第一台计算机，诞生于宾夕法尼亚大学，取名“艾尼阿克”，1946年），且如今大部分前沿的计算机科学学习材料是英语写成的，所以难免在学习这门课的过程中碰到一些英文单词。但是没有关系，只要笔记哥时间精力许可，都尽量给大家做个翻译。当然啦，大家也要勤于动手搜搜，搜谷歌（如果你会搭梯子），搜Bing，搜百度，搜有道词典，相信都会有所获。

好，这里就来讲一下上面的简要的电脑硬件组成图中设计的几个元件的单词：

* **The Central Processing Unit (or CPU)**: 中文语言里好像也可以直接叫CPU，或者长一点的翻译就是“中央处理器”。它是整个计算机的核心部件，其任务就是不断的发问：“咱们下一步做什么？我们下一步做什么？”总之就是快速的向内存寻求下一步要执行的指令。譬如说一台电脑的CPU执行效率是3.0G赫兹每秒。这个意思就是它的CPU一秒钟内会询问内存“我们下一步做什么？”这个问题30亿(3.0*10^9)次。
* **Main Memory**: 主存储器，或者叫内存。这里存着CPU直接需要访问的信息。就是要被CPU每秒钟问破头的那个地方。显然，数据在内存里面的运行速度需要跟CPU差不多快，才能满足CPU的要求。自然，内存的造价也就比下面要提到的二级存储器来得高。而且，内存中的数据有个特点，就是电脑断电后，数据自动消失，不予以保留。
* **Secondary Memory**: 二级存储器。主要就是包括了你电脑的硬盘，手机的主要容量的存储器，甚至你的移动硬盘，网络远端的云存储空间等等。二级存贮器的优点就是，数据长期储存，电脑的电源切断对其基本无影响。缺点就是离CPU越远，调用速度越慢。比如，从移动硬盘读数据肯定不如直接从你的PC本机硬盘读数据来得快。
* **The Input and Output Devices**: Input Device 是输入设备的意思，Output Device 是输出设备的意思。输入设备包括我们常见的键盘、鼠标、手机或者平板电脑的触摸屏等等。输出设备则包括了PC的显示器。对于手机和平板电脑而言，触摸屏既是输入设备也是输出设备。
* **Network**: 网络。最著名的网络自然就是我们常用的互联网（又叫因特网、万维网）。此外，电脑也可以只连接某个局域的网络，比如阿里巴巴公司的内网，清华大学校园网，等等。

好。看到这里，读者你只需了解，我们即将写的Python程序，以及在模块一. Python基础和模块二. Python数据结构中要写的Python程序，只会在CPU和内存当中运行。之后涉及到爬网页的部分，我们会涉及到Network。然后把爬到的数据存到硬盘的数据库里，我们会用到二级存储结构--硬盘。

### 从日常说话来理解编程
编程其实就像我们的日常说话，只是不同于人与人之间对话，编程是人向电脑说话。再者，人和人之间的对话是可以比较随意的，但编程中对电脑说话一定要符合电脑程序所能理解的逻辑以及关键词。

举个栗子，小王对他女票说：“520我带你去本杰明牛排店搓一顿吧。”这是日常随性对话。

如果要弄得逻辑一点，小王应该这么说：“如果今天是5月20日，我就带你去本杰明牛排店吃牛排。”这就像我们的小学生造句--“如果（怎样怎样），就（怎样怎样）”。从自然语言的语法角度分析，这句话是具备了条件状语“如果（怎样怎样）”。

好，用Python编程语言模拟上面的有条件状语句子，大致就是:
```python
if today == 'May 20':
    print('Bring my girlfriend to Benjamin Steak')
else:
    print('Do Nothing')
```

在这段Python代码中，`if`就是“如果”的意思，`today == 'May 20'`是简要的表示先前已经给定的一个名为`today`的变量，当它等于`'May 20'`这个形态的时候，表示“今天是5月20号”了。那5月20号要做什么呢，`print('Bring my girlfriend to Benjamin Steak')`用来表示“带女朋友去本杰明牛排店搓一顿”这个举动。`print`就是“打印”的意思，它会把单引号里面的东西打印出来到你的Atom的Console区域，或者你在终端(Terminal)运行代码的话就会打印在你的终端。【关于Atom这个免费软件等信息参看免费Python小课第0课的内容】

以上只是一个从概念上的对人类的一句话的Python举例，假如你无法在Python环境敲上面的代码并运行，不用着急。我只是想说，有时候人跟Python对话比人跟人对话还要容易，尤其当你在外国工作生活的时候，用的是你的第二语言--英语。要知道，英语当中至少有17万多的词汇。

![apps](/img/in-post/20200516-free-python-01/english-words.png)
<small class="img-hint">来源：谷歌搜索</small>

而你要跟Python对话，主要会用到如下图的Python保留词
![apps](/img/in-post/20200516-free-python-01/reserve-words.png)
<small class="img-hint">Python3的30个保留词，来源：《Python for Everybody》一书</small>

Python的词汇量，是不是比英语小了很多呢！自然，应该比英语更好学。

### 第一个Python程序
下面，激动人心的时刻到了，我们要写第一条Python代码了。

由于是第一个Python程序，很简单，我们没有必要用复杂的Atom进行语法检查什么的。所以，请直接打开你Mac电脑中的终端(Terminal)App，输入
```
$ python3
```
一般我用"$"来表示你打开终端App后看到的光标前面的一大串字，比如我的是`codingbro@Code's-MacBook:~/Documents/python-little-course/`。哎，太长了，还是用一个`$`表示来得省事。  
总之，输入完`python3`摁回车键，你应该会看到类似如下的信息
```
Python 3.7.2 (default, Jan 13 2019, 12:50:01)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
光标就停留在`>>>`符号的后面。

这段信息基本告诉你，Python的解释器已经启动了，用的是Python 3.7.2版本（你的版本只要是3.x.x就能完成本课程，比我的版本高或低一点都无所谓）。你可以在**`>>>`符号的后面开始写你的Python代码了**。

然后，请你打下如下字符，并按回车：
```python
print('你好,Python')
```

你看到了什么？首先，Python3是支持打印中文文字的。当然，关键是在你打完上述代码的下一行，Python解释器输出了“你好,Python”的字样。

![apps](/img/in-post/20200516-free-python-01/ex1.png)
<small class="img-hint">如果你的Python解释器返回给你如图所示结果，说明你做对了</small>

好，恭喜你，你已经完成了你的第一个Python程序！！

那，下一步干什么？比如，你可以试着把引号内的内容换成别的什么东西，看一看会得到什么结果。

也许你会问，这门课就这么简单吗？

别骄傲哦，这才是刚开始，我给你看看这门课学到第10课你会写出来的代码大概长什么样：
```python
file_name = input('Enter a text file name:')  # ie. '../files/mbox.txt'
try:
    file = open(file_name)
except FileNotFoundError:
    print(file_name, 'does not exist!')
    exit()

map = dict()
for line in file:
    line = line.rstrip()
    if line.startswith('From '):
        words = line.split()
        time = words[5]
        hour = time.split(':')[0]
        map[hour] = map.get(hour, 0) + 1

lst = list()

for hour, freq in map.items():
    lst.append((hour, freq))

lst.sort()

for item in lst:
    print(item[0], item[1])
```

是不是看不懂了？不过没有关系，持之以恒，跟着笔记哥学习下来，不需多时你就会明白上面的代码了。

### 总结
好，总结一下。这一章的内容主要就是激发读者学习编程的兴趣，解除编程的神秘感，带读者朋友们写出第一个Python程序！  
喜欢我内容的朋友可以在YouTube或微信公众号搜索**“代码笔记哥”**订阅我。

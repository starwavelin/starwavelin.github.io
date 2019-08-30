---
layout:     post
title:      "从4种大脑储备知识的结构看如何从学渣到学神"
subtitle:   "The Mind Structure of Smart Study People"
date:       2019-07-10
author:     "starwavelin"
header-img:
tags:
    - 学习方法论
---

今晚本想刷一道题目的，但想到刷题的本质是什么，目的是什么，就觉得有必要把之前从知乎上读到的一篇关于学渣、学弱、学霸、学神的大脑知识结构图谱整理出一个笔记来。原文我已经忘记在哪儿了，就凭自己的记忆，复构一下对自己有帮助的要点。

然后，那篇文章的一个重点，我先敲一下黑板！
学渣、学弱、学霸、学神的关系并不是固定不可变的，而是可以从学渣->学弱->学霸->学神进行转变的！

![oh-my-zsh](/img/in-post/20190710-mind-structure/quadrantal_diagram.png)
<small class="img-hint">曾有一个硅谷的培训机构把学渣、学弱、学霸、学神这4个名词画了一个象限图，不知道你同意吗？</small>

### 学渣的大脑 - 散点图
对于知识，学渣只是满足于完成任务不得不学。假如把一个一个的知识点画作小球的话，学渣的大脑知识图谱就像是一个一个散点的小球。是的，他所做的就是把知识球往脑子里放入，就行了。其他的，就都不管了，假如忘记了，还要再放。

![oh-my-zsh](/img/in-post/20190710-mind-structure/xuezha.png)
<small class="img-hint">大家看看这个图，我们且先不谈"忘记"这样的情况。我就说我现在要查找A<sub>1</sub>，是不是很费力啊？？！！</small>

### 学弱的大脑 - 箱子图
学弱的情况就好一些，他会把相同类型的知识点，放到同一个箱子里面。比如A系列的，进一个箱子，B系列的，进入另一个箱子，诸如此类。

![oh-my-zsh](/img/in-post/20190710-mind-structure/xueruo.png)

### 学霸的大脑 - 树状图
学霸则更进一步，每一个箱子里面的知识点，都做了一个抽象。那么，同一个箱子里的知识点们，就可以与这个新抽象出来的知识点进行连接，从而每一个箱子都转化成了一个树状图。

![oh-my-zsh](/img/in-post/20190710-mind-structure/xueba.png)

这样的好处就是，查找起来快了很多。对于某些特定知识，他只需要首先知道这个知识的抽象点，然后顺藤摸瓜就找到了。

### 学神的大脑 - 多连通图
学神的大脑则再进一步，树状图使每一个类型的知识都有了一个抽象点进行连接，但学神能够将表面上非同一类型（或者不是表面上，而是本质上属于弱连接类型的知识点们）构建起连接。因此，他的大脑就成了多连通图，有了立体的感觉。原本在上图中不相连的点A<sub>1</sub>与B<sub>2</sub>与C<sub>3</sub>等等，建立起了连接。

![oh-my-zsh](/img/in-post/20190710-mind-structure/xueshen.png)

比如，学神要搜索C<sub>3</sub>的时候，他可以通过C搜索到C<sub>3</sub>；还可以通过A<sub>1</sub> -> B<sub>2</sub> -> C<sub>3</sub>；还可以通过B搜索到C<sub>3</sub>。多条路径得到同一个知识点，同一个知识点可以发散出多条路径。知识的查找与应用效率倍增。

### 从学渣到学神 - 以算法题为例的讲解
所以，原来从学渣到学神的路径没有那么地难，只要按照👆四幅图的步骤，一步一步的改造自己大脑的知识结构就可以了。

但话说回来，也很难，因为单单从学渣到学弱的路，一个学渣首先就要客服懒惰。至少，您要对自己有的知识点，进行装箱整理吧。至少，该装箱知识点的时候，你的微信、抖音这类的App，你该不要去碰了吧？或者，把手机放在一边不理它更好。

从学弱到学霸，就是要学习抽象整理的能力，把类同的知识抽象出共同点来。比如，我以前的一位同事就提醒我，说面向对象程序设计的SOLID法则，让我不要去从Java语言的角度去想为什么有SOLID法则，毕竟SOLID可以应用在其他语言嘛，比如TypeScript，比如Python。他要我去想SOLID法则本身的意思与应用。

最后，学霸到学神，我的理解是，这需要更多的观察和积累，找到知识点的连通性。这种知识的连通能力的获得有时候无法通过闭门造车得到，需进入到某些特定的社群找到高手帮助点拨才行。

**OK，以算法题集为例**

其实LeetCode上的Tag已经帮我们做了装箱的一些工作。每一道题目，属于哪一个类型，比如 Array类型、String类型等等按照题目的输入条件进行分类的，我们也可以先仿照LeetCode已有的分类进行装箱。当然，我更鼓励您按照你自己刷题的一定积累与心得，对你做过的题目进行分类。不一定要按照输入条件进行分类。也有可能按照解法进行分类，对吧，比如双指针类型的题目。

做好分类这一关以后，我们就可以从每一类当中提纲挈领出一些解题常见规律。举个栗子，比如你把所有的二叉树类型的题目都归为”二叉树类“，那么你至少能提炼出它们的一些共同解法：分治法、深度优先搜索法、广度优先搜索法（比如层序遍历）。做到这一步，你应该已经有了自己的树状图了。

最后，我们还可以看看那些表面上不同的题目，实质上有什么弱联系，加以融会贯通。比如Array类型、String类型、链表类型题，它们中的一部分题目还有一个共同的本质，就是这类题的输入空间是线性的，解空间也可以是线性的，也许它们都适用于双指针或者多指针应用的解法。再比如，树的深度优先搜索、图的深度优先搜索、动态规划的部分题目、甚至像反转链表这样的简单题目，都可以通过深入理解“递归”这个概念，加以关联起来。

### 刷题的本质是什么，目的是什么
最后，时间不早了。这个假如要展开讲的话，可以写一篇鸡汤软文了。笔记哥今晚的理解是：
刷题的本质是掌握计算机算法和数据结构的核心知识，目的是为了找更好的工作。毕竟，国内的BAT、头条等以及美帝的FAUG（Facebook, Apple, Amazon, Airbnb, Uber, Google）等面试都要考算法题的。
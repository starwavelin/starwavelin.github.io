---
layout:     post
title:      "Mac上配置Python3虚拟开发环境"
subtitle:   "Configure Python3 Dev Environment on Mac with Virtualenv"
date:       2019-01-25
author:     "starwavelin"
header-img: "img/post-banner/post-bg-python3.jpg"
tags:
    - Config
    - Mac
---

### 自带的python2
首先，当你在Mac的命令行下敲`python`回车后，你一般会看到如下信息
```
Python 2.7.10 (default, Aug 17 2018, 19:45:58)
[GCC 4.2.1 Compatible Apple LLVM 10.0.0 (clang-1000.0.42)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
这说明Mac自带python2  
再敲`quit()`回车，退出python2的命令行。我们今天要讲的是如何安装python3并搭建起开发环境。

### 通过Homebrew安装python3
在Mac尚未安装python3的时候，你如果在Mac的命令行下敲`python3`回车，得到的只能是如下信息
```
zsh: command not found: python3
```
笔者用的是zsh,你可能是看到`bash: command not found: python3`,但本质都一样，python3尚未安装。

由于是Mac机子，我们可以用Homebrew安装python3。Homebrew是Mac下非常好用的包管理器(package mamnager)。假定您还没有安装Homebrew，请走以下步骤。

1. 进入Homebrew的官网[https://brew.sh/](https://brew.sh/),复制黏贴其安装命令到您的命令行，按回车。
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. 可以用如下两个命令，确认homebrew安装正确
```
$ brew list
$ brew cask list
```
比如，运行完`brew list`，您可能看到homebrew的五个组件“gettext		libidn2		libunistring	openssl		wget”

3. 然后，我们终于可以用homebrew安装python3啦，运行命令
```
$ brew install python3
```
安装完成后，在命令行内输入`python3`，您应该能看到类似下面的内容
```
Python 3.7.2 (default, Jan 13 2019, 12:50:01)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
说明安装python3成功了！是不是很简单？

### 用virtualenv实现不同Python项目分开管理
做为python开发者，我从网上找到了三大神器的说法：virtualenv, fabric, pip。  
其中pip最为常见，它是python的包管理系统，用于安装和管理所有用python语言写成的软件包。  
fabric则是一个高级的python库，用于通过SSH远程执行shell脚本命令并返回python对象。笔者倒觉得这个没那么常用。  

不管怎么说，本文要用到的是vrtualenv，它就是一个python的虚拟环境，中文也叫虚拟沙盒。它能把项目放在一个虚拟的环境里边，在这个环境里你使用的python版本以及安装的依赖都不会影响环境外的项目。

举个栗子来讲，很多数据科学的项目用到的包，比如numpy, panda还是基于python2系列的。但我后来又想开发网站，想用最新的python3以及它所对应的django。我不希望这两个项目有包依赖的冲突，更不希望这两个项目跟Mac本身default的python配置环境有所冲突。怎么做到？用virtualenv就可以。

**安装virtualenv**  
由于我们刚刚已经安装了python3，在python3下对应的pip是pip3。因此安装virtualenv，只需执行命令
```
$ pip3 install virtualenv
```
如果命令行中看到如下字样，则说明virtualenv安装成功
```
Installing collected packages: virtualenv
Successfully installed virtualenv-16.3.0
```

**创建虚拟环境**  
virtualenv命令的用法是`virtualenv [OPTIONS] DEST_DIR`,其中DEST_DIR就是你要创建的虚拟环境项目的名字，`[OPTIONS]`就是命令参数，有一个命令参数叫`--no-site-packages package`。virtualenv默认是会依赖你已经装有的第三方的包的，假如你希望该虚拟环境项目绝对不依赖已有的第三方包，你可以在建立该虚拟环境的时候加上`--no-site-packages package`。

我们建一个虚拟环境项目试试，比如我要搞一个python3写的网页项目，名叫"py3_web_toy",我就
```
$ virtualenv py3_web_toy
```

我得到如下信息在命令行中
```
Using base prefix '/usr/local/Cellar/python/3.7.2_1/Frameworks/Python.framework/Versions/3.7'
New python executable in /Users/starwavelin/py_workspace/py3_web_toy/bin/python3.7
Also creating executable in /Users/starwavelin/py_workspace/py3_web_toy/bin/python
Installing setuptools, pip, wheel...
done.
```

检测目录，我发现我的当前目录下派生出了"py3_web_toy"文件包，文件包具备如下结构
```
├── bin
├── include
│   └── python3.7m
├── lib
│   └── python3.7       //所有的新包会被存在这
│       ├── distutils
│       ├── site-packages
│       ├── lib-dynload
│       └── ......      // 这个python3.7文件夹下还有很多文件，省略不列
```

OK。这么一个默认使用python3.7版的虚拟开发环境就做成了。

**启动虚拟环境**  
在"py3_web_toy"这个目录下，输入命令
```
$ source ./bin/activate
```

你会发现成功启动后，命令行的前面会带上有括号的"py3_web_toy"字样。
```
(py3_web_toy) someUser@Some-MacBook:~/py_workspace/py3_web_toy$
```

你再用`pip list`一测试，就会发现项目依赖都是基于python3的独立于"py3_web_toy"内部的了。我的可见依赖是：
```
Package    Version
---------- -------
pip        19.0.1
setuptools 40.6.3
wheel      0.32.3
```

**退出虚拟环境**  
```
$ deactivate
```

**搭建一个python2项目**  
我们再来试试，假如我现在要再搞一个数据科学的项目，要用python2来写，怎么办？

我可以退出"py3_web_toy"虚拟环境。然后，在`virtualenv`命令中通过使用`--python`参数指定python版本创建一个基于python2的虚拟环境。

```
$ virtualenv py2_data_sci --python=/usr/bin/python2.7
```

进入"py2_data_sci"文件夹下的"lib"文件夹，我们发现对应的python版本的确为2.7了。BINGO！！

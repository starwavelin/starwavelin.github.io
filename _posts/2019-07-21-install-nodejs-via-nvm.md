---
layout:     post
title:      "Install Node.js via NVM"
subtitle:   "通过nvm安装Node.js"
date:       2019-07-21
author:     "代码笔记哥"
header-img: "img/post-banner/post-bg-nodejs.jpg"
tags:
    - Node
---

### Install nvm first
NVM stands for Node Version Management. Before you install node.js, you can install nvm first.
```
$ curl https://github.com/creationix/nvm
```

### (Optional) For oh-my-zsh user
For oh-my-zsh user, please add the following lines into `~/.zshrc`
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

### Install the node
If you just wanna install the latest node, issue command:
```
$ nvm i node
```

If you'd like to install a specific version of node, do
```
$ nvm i [specifi node version]
```
ie. `$ nvm i v10.7.0`

### Use a specific version of node
```
$ nvm use [specifi node version]
```

### If you wanna specify the node version of a project
Then, you need to create `.nvmrc` file in the root of your project directory.
And you put a line specifying node version into `.nvmrc` file, for instance:  
`10.15.0`

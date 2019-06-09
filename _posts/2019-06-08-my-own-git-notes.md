---
layout:     post
title:      "My Own Git Notes"
subtitle:   "个人Git笔记"
date:       2019-06-08
author:     "starwavelin"
header-img:
tags:
    - 其他技术
    - Extensible Note
---
### Useful Commands
- `$ git commit -n`  
`$ git commit -n`, the `-n` is not a supported argument, if you look into [https://git-scm.com/docs/git-commit/1.5.5](https://git-scm.com/docs/git-commit/1.5.5). But my company uses it to do enforced es-linting on staged files only. It is quite useful when there are some linting rule changes and you just want to apply es-linting on staged files that appearing after issuing command `git merge <branch>`.  
Ex.  
```
$ git commit -n -m 'brought master branch in'
```
Explanation: `-n` is the enforcing es-linting on staged files only and `-m` is for issuing commit message.

- `$ git revert <certain_commit_hash>`  
This will undo the changes in the "certain_commit_hash" but preserve the changes **before and after** the "certain_commit_hash".  

### Generating New SSH Key Pair  
Please read [here](https://docs.gitlab.com/ee/ssh/#generating-a-new-ssh-key-pair).  
When you need to clone and work on a project in a new machine, and you use SSH key pairs as you r way of authentication, you would want to generate a new SSH key pair. Basically, the link above uses GitLab as an example, but it should be similar to do it in GitHub.

### How could I specify multiple users for myself in gitconfig?
Assume you have a default username and user email and a customized username and user email for GitHub. Then, you can specify when to use what as following:
- For your default user / email, please configure them in your `~/.gitconfig`
```
git config --global user.name "Your Default Name Here"
git config --global user.email your_default_name@email.com
```
- For an individual repo that you want to use your customized user / email address, which overrides the global configuration, please, from the root of the specified repo, run
```
git config user.name "Your Customized Name Here"
git config user.email your_customized_name@email.com
```

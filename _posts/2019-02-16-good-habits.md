---
layout:     post
title:      "编程好习惯"
subtitle:   "Good Programming Habits"
date:       2019-02-16
author:     "codingbro"
header-img: "img/post-banner/post-bg-github-blog.jpg"
tags:
    - Extensible Note
---
以下是我总结的一些编程好习惯

### DRY (Don't Repeat Yourself) Rule
#### 利用添加parameters的方法实现DRY
```
getPresidencyTerm(isWholeLife: boolean, term: number) string {
  if (isWholeLife) {
    return "终身制";
  }
  else if (term) {
    return `${this.selectedPresident.term} years`;
  }
  return "Not a president";
}
```
`isWholeLife: boolean` is an added parameter, though it looked a little odd at the beginning that a boolean param is added with a string param :)

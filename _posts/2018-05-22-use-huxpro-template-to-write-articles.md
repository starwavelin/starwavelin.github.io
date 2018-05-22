---
layout:     post
title:      "How to Use Huxpro Template to Write Articles"
subtitle:   "用Huxpro模板写文章"
date:       2018-05-22
author:     "starwavelin"
header-img: "img/post-banner/post-bg-mosaic.jpg"
tags:
    - 其他技术
---
### Table of Contents
- [Preface](#preface)
- [Writing a journal](#writing-a-journal)
- [Adding a table of contents](#adding-a-table-of-contents)
- [Apply your own domain to your tech blog](#apply-your-own-domain-to-your-tech-blog)   

### Preface
Firstly I would like to sincerely thank Mr. Xuan Huang (黄玄 | [Huxpro](https://github.com/Huxpro)) for providing this convenient Jekyll template.
He actually supplies two templates for the general public to use:
1. [boilerplate version](https://github.com/Huxpro/huxblog-boilerplate)
2. [his personal advanced version](https://github.com/Huxpro/huxpro.github.io)

What I am using for myself (Coding Bro 📒代码笔记哥）is the boilerplate version.

### Writing a journal
To write a journal for your blog, create a markdown file in ``_posts/`` directory with format "yyyy-mm-dd-{your-journal-title}.md", in which you can replace {your-journal-title} with any article name you want.  

Then, within the ``.md`` file, the header should be coded in a somehow fixed format. Here I'd like to show you two screenshots and I guess after viewing them, you will know how to code your article.

![header-code](/img/in-post/180522-use-huxpro-template/header-code.png)
<small class="img-hint">in this 10-line header code of a markdown file, just make sure the layout should be "post", other fields can be customized or omitted</small>
![header-outcome](/img/in-post/180522-use-huxpro-template/header-outcome.png)
<small class="img-hint">corresponding outcome of the 10-line header code</small>

And, Huxpro template also provides an automatically generated summary of an article you post.
![summary-on-index](/img/in-post/180522-use-huxpro-template/summary-on-index.png)


### Adding a table of contents
You can also add a table of content to your journal if you think necessary. To do so, you need a tool called [gfm-toc](https://github.com/starwavelin/AlgorithmPractice/blob/master/gfm-toc)  
And I already wrote an instruction on [how to use gfm-toc](https://github.com/starwavelin/AlgorithmPractice/blob/master/gfm-toc-usage.md)

![toc-issue](/img/in-post/180522-use-huxpro-template/toc-issue.png)
<small class="img-hint">Hmm, seems like directly apply the gfm-toc tool above did not give what I want</small>
No worries. I worked around to get it work. The error was actually because I set all the headers of each section in this journal to be h3 (header size 3, in markdown which is 3 hashes). Therefore, gfm-toc tool auto made 2 indentations to represent h3 header, like below.
![error](/img/in-post/180522-use-huxpro-template/error.png)

Once I removed the redundant indentations to make the code as below
![fix](/img/in-post/180522-use-huxpro-template/fix.png)

The problem resolved.

### Apply your own domain to your tech blog

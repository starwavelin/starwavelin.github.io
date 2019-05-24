---
layout:     post
title:      "Bug Fixes on my Blog"
subtitle:   "博客修bug📝"
date:       2018-05-24
author:     "starwavelin"
header-img: "img/post-banner/post-bg-debug.jpg"
tags:
    - 前端
    - Extensible Note
---

### 2018-05-23
总的来讲做了这一件事：Improve the content delivery network of font-awesome (or other libraries as well) from CDN to CDNJS  
具体见下

**CDN**  
What libraries are using CDN for now?
1. **highlight.js v.8.6** (commented in the given template)
2. **fastclick v.1.0.6**  
https://cdn.bootcss.com/fastclick/1.0.6/fastclick.min.js
3. **font-awesome v.4.2.0**  
https://cdn.staticfile.org/font-awesome/4.2.0/css/font-awesome.min.css
4. **html5shiv v.3.7.0** & **respond.js v.1.4.2**  
these two are for browsers lower than IE9, already in commented mode
5. **anchor-js v.1.1.1**  
https://cdn.bootcss.com/anchor-js/1.1.1/anchor.min.js  

The only one I found different from others is the one for font-awesome 4.2.0, which is supplied from ```https://cdn.staticfile.org/font-awesome/4.2.0/css/font-awesome.min.css```. The original author left a comment saying *Hux change font-awesome CDN to qiniu*. So this CDN is actually from 七牛云 for the convenience of viewers in mainland China.

Now let me just change this back to ```http://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css``` and see if the page loading speed would improve.  

And Yes, the loading speed has been dramatically improved to 1.35 second.
![loading-speed](/img/in-post/180524-bug-fixes/180524_loadspeed.png)

*Note:*  
For people from mainland China, if you have difficulty viewing the SNS icons as below,
![sns-icons](/img/in-post/180524-bug-fixes/SNS_icons.png)
please use Disqus (if available to you) or any other SNS/contact method to let me know. I will do my best to balance the services to my audiences. Thanks!

### 2018-05-21  
1. Updated the ```baseurl:``` in ```_config.yml``` file from "/huxblog-boilerplate" to "" and served my blog from the root directory of ```GITHUB_USERNAME.github.io```
2. Fixed the issue of [cannot display SNS Zhihu and GitHub icons](https://github.com/Huxpro/huxblog-boilerplate/issues/17) based on [pull request #21](https://github.com/Huxpro/huxblog-boilerplate/pull/21/commits/207a48449f06b3a509c861a4622d92e48855c698)

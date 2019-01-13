---
layout:     post
title:      "Bug Fixes and Feature Adding on my Blog"
subtitle:   "博客加功能、修bug📝"
date:       2018-05-24
author:     "starwavelin"
header-img: "img/post-banner/post-bg-train-track.jpg"
tags:
    - 前端
    - Extensible Note
---

### 2018-05-28
**Configure Disqus on my blog**  
Besides adding my disqus shortname to ```_config.yml```, I also need to follow hints [here](https://github.com/Huxpro/huxpro.github.io/issues/157)  
Basically, it means on [this page](https://disqus.com/profile/signup/intent/),
I need to select the option "I want to install Disqus on my site"



### 2018-05-23
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

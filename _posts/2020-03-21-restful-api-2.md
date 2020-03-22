---
layout:     post
title:      "RESTful API之\"好的RESTful API设计\""
subtitle:   "Good RESTful API Design"
date:       2020-03-21
author:     "代码笔记哥"
header-img:
tags:
    - 系统设计
---
上期回顾：[RESTful API之"四大要素"](../../../../2020/01/05/restful-api-1/)  

好的Restful API设计，总结起来，应尽量满足如下七点。

### 1. 一个URL唯一确定一个资源
这个其实不是一个尽量要满足的点，而是一个硬性规定了。要知道，如果这一条不能满足，那么那个URL就不能算是API了。  

举例：`GET http://starwavelin.io/api/v1/articles/1024`  
这个API翻译成普通汉语，可以理解为“获取 版本1第1024号文章”，这版本1当中的第1024号文章必然是一个唯一确定的资源。

### 2. URL应包含名词而非动词
下面这个例子的场景是在一个请求(request)当中去添加该请求所包含的所有股票(shares)的信息。它是一个RESTful API   
`POST http://starwavelin.io/api/v1/requests/318/shares`  
把第318号请求当中所包含的所有股票信息都给我发到服务器端。

上面是一个符合好的Restful API设计的例子。再举一个不符合的例子，比如  
`POST http://starwavelin.io/api/v1/requests/318/create`  
这个`create`就是一个动词，取代了原先`shares`这个复数名词，这样的URL也能工作，但就不能算是Restful API了。

### 3. 仅使用HTTP动词来进行操作
HTTP verbs主要包含GET, POST, PUT, DELETE四种。好的Restful API就应当纯粹利用HTTP动词对群体或个体进行操作。举一个跟狗狗有关的例子，假定一个网站服务器要存很多跟宠物狗有关的信息，那么，Restful API对所有的宠物狗，或单一的某一只宠物狗，可以有如下表格的操作。

| HTTP METHOD | POST   | GET  | PUT  | DELETE |
| ----|-----------|-------------|-------|--------|
| 增删改查操作类型	| CREATE 增 | READ 查 | UPDATE 改 | DELETE 删 |
| /dogs	| Create new dogs | list dogs | Bulk update | Delete all dogs |
| /dogs/1024	| ERROR | Show BeauBeau | If exists, update BeauBeau's info, otherwise, error | Delete BeauBeau|

解释一下`/dogs/1024`这一行。如果我们要添加一只名字叫BeauBeau（法语词，汉语发音近似“波波”）的狗，我们是不能从客户端事先给定一个ID给它的。RESTful API的设计要求我们，通过`POST /dogs`的操作，往服务器去添加一只新的狗的信息。所以，如果想在RESTful API的设计下刻意去`POST /dogs/1024`，就会出错。

### 4. 好的RESTful API 的URL 名词皆用复数
这个在第2点请求和股票的那个例子中就有体现，不赘述。

### 5. 不应太过深入才能得到资源
“不应太过深入才能得到资源”， 英语 Shouldn’t go deeper than resources/identifier/resources 这是什么意思呢？  

我们再举第2点中提到的请求与股票的例子。假定我已通过HTTP POST方法，(ie. POST http://starwavelin.io/api/v1/requests/318/shares)在服务器端生成了第318号请求的所有股票。然后，我要去访问第1083号股票信息，且第1083号股票刚好是由第318号请求生成的，那么，我需要用 ` GET http://starwavelin.io/api/v1/requests/318/shares/1083 ` 去得到第1083号股票吗？

这样设计的API可以得到我要的信息，但这个不符合好的Restful API设计。好的方法应当是，股票的ID本身就应当是独一无二的定义了股票信息。所以，好的API应当是用 ` GET http://starwavelin.io/api/v1/shares/1083 `就可以了。

所以，好的Restful API设计告诉我们，我们不要用URL去体现数据的逻辑关系或存储结构。也许在逻辑关系上，shares是在requests之下的，但好的Restful API设计告诉我们，尽可能在不要深入太多层级的情况下，就把返回给用户他所要的资源。

### 6. 在API的base URL中加入版本号
这是一个重要的好习惯，因为我们不能保证API的版本是一定能向后兼容的。特别是在团队合作使用微服务互相call来call去的情况，当作为服务器的那一方的API版本升级了，就要使用一个新的版本号，并维持旧版本的服务一段时间，并养成好习惯通知作为客户方的团队。当然，不通知，客户方也可能通过查看你服务器方的API文档也能发现升级，自己也需要做相应的与服务器方团队的沟通和修改。但，假如服务器方不使用版本号，修改升级了，又没有通知客户方的团队，那就会出现bug!！务必要养成好习惯，在API的base URL中加入版本号。

### 7. 在URL链接中用optional fields来请求个别的资源
比如说我要找Economist第98号杂志中的标题为xxx的文章，那么我可以使用
`GET  http://www.economist.com/api/v2/magazines/98?title=xxx`  
这个URL中的title就是一个optional field。

OK，以上就是总结的7个好的Restful API设计的要点。大家如果有什么要补充的或纠错的，评论区留言吧。

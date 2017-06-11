---
title: hexo 创建一篇文章
layout: post
date: 2017-05-16 15:19:08
comments: true
tags: 
	- hexo
	- blog
keywords: hexo,blog
categories: Hexo学习
description: 生命在于折腾，又把博客折腾到Hexo了。给Hexo点赞。

---
#### 一.创建文章
1.hexo new "postName" #新建文章
#### 二.设置文章头部(文件被放在source/_posts)
<!--more-->
1.先用`markdown`编辑器打开文件
2.设置表头:
```
title: hexo 创建一篇文章
layout: post
date: 2017-05-16 15:19:08
comments: true
tags: [Hexo]
keywords: hexo,blog
```
3.正文
#### 三.发布到githup
1.先清除缓存
`hexo clean`
2.发布
`hexo d -g`
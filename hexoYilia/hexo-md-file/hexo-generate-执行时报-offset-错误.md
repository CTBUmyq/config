---
title: hexo generate 执行时报 offset 错误
layout: post
date: 2017-05-24 02:05:17
comments: true
tags:
	- hexo
	- error
categories: Hexo报错
keywords: hexo,error
description: Cannot read property 'offset' of null

---
####  一、hexo g 出错
截图： <img src="/imgs/timezone.png"/>
原因：我在_confing.yml下 timezone配置错了  
<!--more-->
错误配置： timezone： ChongQing

如果设置cheng +08:00 后 momentjs解析会报异常
需要将timezone配置成 时区名称：
<img src="/imgs/timezone1.png" />
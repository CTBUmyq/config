---
title: hexo 建站分享
layout: post
date: 2017-05-16 16:50:21
comments: true
keywords: hexo,建站
reward: true
tags:
	- hexo
	- 静态建站
categories: Hexo
description: 建站分享和一些自己总结的没有的东西
---
### 一.建站连接分享
`link` [手把手教学Hexo+Githup pages搭建个人博客][1]
`link` [ markdown半小时入门分享][2]
<!--more-->
### 二.建站遇到的问题
当hexo d -g出错，找不到git时，看我之前的一篇[hexo -d错误解决][3]。
<!--more-->
### 三.一些其他文章没有的东西
**1.首页文章截断功能**
在默认情况下，首页会显示全部文章，不会对文章进行阶段。现在介绍两种文章截断的方式
(1).在文章中使用`<!--more-->`，会自动阶段到该位置。
在markdown头部的Front-matter里面加入description字段。优先会使用(2).description字段的内容。
**2.修改样式的办法**
(1).右键，检查，点击元素，观察它的样式和所属文件，在本地文件夹找到后直接修改粗暴。
**3.文章首行缩进**
(1).&emsp;
(2).&nbsp;
[1]: https://segmentfault.com/a/1190000004947261
[2]: https://www.zybuluo.com/mdeditor
[3]: https://ctbumyq.github.io/2017/05/16/hexo-d-%E5%87%BA%E9%94%99/

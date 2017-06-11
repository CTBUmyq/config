---
title: hexo d 出错
layout: post
date: 2017-05-16 16:33:07
comments: true
keywords: hexo,error
tags:
	- hexo
	- error
categories: Hexo报错
	
---
#### 一.找不到git部署
`error` ERROR Deployer not found: git
``原因`` 没有部署hexo-deployer-git
<!--more-->
``解决方案`` npm install hexo-deployer-git --save
#### 二.当我们首次安装hexo时修改了hexo的_config.yml时不生效
解决方案同上

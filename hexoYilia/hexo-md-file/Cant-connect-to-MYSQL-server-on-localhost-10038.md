---
title: Cant connect to MYSQL server on localhost(10038)
date: 2017-05-26 16:34:20
layout: post
comments: true
tags:
	- mysql
	- error
categories: MysqlError
keywords: mysql,error

---
### 一、错误原因
When Navicate connect Mysql，this Service is off.
<img src="/imgs/mysqlErrorNotConnect.png" />
<!--more-->
### 二、解决方案
#### 1.打开任务管理器并切换选项卡到服务
<img src="/imgs/taskManage.png" />
#### 2.点击服务
<img src="/imgs/service.png" />
#### 3.选择MYSQL并右键启动即可
<img src="/imgs/allService.png" />
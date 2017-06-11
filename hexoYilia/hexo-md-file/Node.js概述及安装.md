---
title: node.js概述及安装
layout: post
reword: true
comments: true
date: 2017-06-04 23:19:10
tags:
	- Node.js
	- Node.js安装
categories:
	- Node.js
keywords: node.js

---
### 一、Node.js是什么&emsp;
&emsp;Node.js不是一门独立的语言，与PHP、java、.net及是开发语言也是平台不同，也不是javaScript的框架jquery等，更不是浏览器库ExtJs,不能与ExtJs相提并论。Node.js是一个让JavaScript运行在服务器端的开发平台。
### 二、Node.js能做什么?
<!--more-->
&emsp;JaveScript是由客服端而产生，Node.js为网络而生。
&emsp;应用:
```
1.复杂逻辑的网站
2.社交网络的大Web的应用
3.b Socket服务器
4.P/UDP套间字应用程序
5.行工具
6.式终端程序

```
### 三、异步I/O与事件驱动
&emsp;Node.js最大的特性就是采用异步式I/O与事件驱动的架构设计。对于高并发的解决方案，传统的架构是多线程模型，也就是为每个业务逻辑提供一个系统线程，通过系统线程切换来弥补同步式I/O调用时的时间开销。Node.js使用的单线程模型，在执行的过程中会维护一个事件队列，程序在执行时进入时间循环等待下一个事件的到来。
```
普通: 
res=db.query("select * from user");
res.output();
Node.js:
res=db.query("select * from user",function(res){
	res.output();
}):
```
程序会自动向下执行
### 四、浏览器引擎革命
Google Chrome的引擎是V8。Node.js的引擎引用的就是V8。所以它块，为什么ExtJs在Chrome如此的快，就是因为它。
### 五、部署Node.js的环境
Node.js官方：http://nodejs.org
各种操作系统安装步骤:http://www.runoob.com/nodejs/nodejs-install-setup.html
`注意:想要在任何地方运行一定要配置环境变量`

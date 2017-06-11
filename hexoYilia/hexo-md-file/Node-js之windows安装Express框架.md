---
title: Node.js之windows安装Express框架
date: 2017-06-08 09:19:59
reword: true
comments: true
tags:
	- Node.js
	- Express
categories:
	- Node.js
	- Express
keywords: Node.js,Express
description: windows安装Express的过程

---
### 一、基础条件
在你的windows上已经安装了node.js的基础上再安装express
### 二、安装Express
**第一步**:执行 ``npm install -g express-generator ``
note:必须安装这个,不然创建express项目的时候会提示express命令没有找到
**第二步**:执行 ``npm install -g express``
**第三步**:执行`` express -V``(有些可能不支持)
note:'V'是大写的,如果express安装成功会显示版本号
### 三、创建一个Express项目
**第一步**:执行 `express youProjectName`
note:youProjectName是你的项目的名称,按照自己的要求选择合适的项目名称

**第二步** :进入你的项目:`cd youProjectName`

**第三步**:在你的项目的目录下执行 `npm install`

**第四步**:启动你的项目,执行 `npm start`

### 四、最后在浏览器中访问你的项目

打开你的浏览器,在地址栏中输入:http://127.0.0.1:3000

然后你会看到:express的欢迎信息 
### 五、建议
为了降低学习难度，我建议使用`express ejs yourProjectName`;
不建议使用`Jade`;

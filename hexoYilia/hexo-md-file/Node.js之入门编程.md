---
title: node.js之入门编程
layout: post
comments: true
date: 2017-06-05 00:07:48
tags:
	- Node.js
	- Node.js入门编程
categories:
	- Node.js
reword: true
keywords: Node.js，Node.js入门编程

---
### 一、Hello World
打开一个文本编辑器，在其中输入
console.log('Hello World');
<!--more-->
并保存问helloworld.js。打开dos窗口进入该文件的目录
运行node helloworld.js执行则可以看到输出的helloworld
### 二、Node.js命令行工具
node -v版本
1.node -e eval scipt eval("console.log("呵呵")")；
例如:
```
node -e "console.log("hello world")";直接执行
```
2.输入node直接进入编译模式
```
console.log("hello world");
```
第一行是输出，第二行则是返回值
### 三、建立Http服务器
创建一个app.js
```
var http = require("http");
http.createServer(function(req,res){
	res.writeHead(200,{"Content-Type":"text/html"});
	res.write('<h1>Node.js</h1>');
	res.end('<p>PCAT</p>');
}).listen(3000); 
console.log('HTTP server is listening at port 3000.');
```
接下来node app.js打开浏览器访问http://localhost:3000 即可。这样就部署了一个web。比tomcat、resin更加方便。
### 四、调试代码(supervisor)
`supervisor:不必每次修改代码之后重启服务，相当与Ider的热部署`
安装Node.js调试模块：
`全局`：执行`npm  install  <模块的名字>  -g（ps:linux请加上sudo增加权限）` 就会将模块装在全局路径下，当用户在程序中require(<模块的名字>)的时候不用考虑模块在哪，如果不修改全局路径，用户下载的模块会默认在`C:\Users\Administrator\AppData\Roaming\npm`这个路径下。
`局部`：执行`npm  install  <包的名字>（注意少了-g）`就会将模块安装在dos窗当前指向的路径下,这时候其他路径项目无法引用到该版本的supervisor模块！
`如果你想修改全局默认模块可以看这里·(不像想造成更多的麻烦最好不要修改)`
http://www.cnblogs.com/GeoChen/p/5496322.html
### 五、安装supervisor遇到的问题（之后安装其他模块也许也会遇到）
#### 1.我是全局安装为什么我还是用不起该命令
答:虽然是安装在全局路径，但是安装配置文件中不允许
#### 2.为什么我是全局路径，我在Dos里面只有在安装目录可以使用，而在其它地方不能使用
答:未在计算机上配置环境变量，导致不能被使用
``ps:由于没有bin目录，我将全局安装目录C:\Users\myq\AppData\Roaming\npm放入了环境变量之中，这样后面所有安装在该目录下的模块就都可以不用配置了``
#### 3.为什么我用git bash在任何地方都不能使用该命令，即使是安装目录
答：我没有找到答案，知道的希望分享一下，但是我配置了环境变量之后就可以使用了。
---
title: windows下用cmd命令新建用户
layout: post
date: 2017-05-24 21:35:01
comments: true
keywords: windows,cmd
tags:
	- windowsCmd
categories: WindowsCmd
	
---
### 一、打 开DOS操作窗口，点击“开始”菜单，选择“命令提示符”
`快捷键`: windows+r 然后输入cmd
### 二、添加账号net user test test123 /add
<!--more-->
<img src="/imgs/useradd.png" />
### 三、添加管理员权限net localgroup Administrators test /add
<img src="/imgs/poweradd.png" />
### 四、查看用户权限net localgroup administrators或者net user test
<img src="/imgs/powerStatus1.png" />
或者
<img src="/imgs/powerStatus2.png" />
### 五、删除权限net localgroup administrators test /del
<img src="/imgs/powerdel.png" />
### 六、删除账号net user test /del
<img src="/imgs/userdel.png" />
### 七、查看账号net users
<img src="/imgs/userStatus.png" />

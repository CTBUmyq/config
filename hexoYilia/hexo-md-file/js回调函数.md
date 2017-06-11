---
title: js回调函数
date: 2017-06-06 16:17:08
comments: true
keywords: hexo,建站
reward: true
tags:
	- Js
	- Js回调函数
categories: Js
description: 一些基本的Js回调函数
---

`回调函数的传递`
<!--more-->
```
$.get('myhtmlpage.html', myCallBack);//这是对的
$.get('myhtmlpage.html', myCallBack('foo', 'bar'));//这是错的，那么要带参数呢？
$.get('myhtmlpage.html', function(){//带参数的使用函数表达式
myCallBack('foo', 'bar');
});
```
`基本方法:`

```
<script language="javascript" type="text/javascript">
function doSomething(callback) {
// … 
// Call the callback
callback('stuff', 'goes', 'here');
} 
function foo(a, b, c) {
// I'm the callback
alert(a + " " + b + " " + c);
} 
doSomething(foo); 
</script>
```
`用匿名函数的形式`
```
<script language="javascript" type="text/javascript">
 function dosomething(damsg, callback){
  alert(damsg);
  if(typeof callback == "function") 
  callback();
 } 
dosomething("回调函数", function(){
  alert("和 jQuery 的 callbacks 形式一样!");
 }); 
</script>
```
`使用javascript的call方法`
```
<script language="javascript" type="text/javascript">
function Thing(name) {
this.name = name;
}
Thing.prototype.doSomething = function(callback) {
// Call our callback, but using our own instance as the context
callback.call(this);
}
 
function foo() {
alert(this.name);
}
 
var t = new Thing('Joe');
t.doSomething(foo); // Alerts "Joe" via `foo`
</script>
```
---
title: Node.js作用域与上下文
date: 2017-06-05 13:58:29
comments: true
keywords: 作用域，上下文
reward: true
tags:
	- Js作用域
	- Js上下文
categories: 
	- Js作用域与上下文
description: Node.js潜入理解作用域与上下文

---
### 一、作用域
我理解我变量或者函数的作用范围
&emsp;``作用域:``一个变量可以被定义在局部或者全局作用域中，这建立了在运行时（runtime）期间变量的访问性的不同作用域范围。 任何被定义的全局变量，意味着它需要在函数体的外部被声明，并且存活于整个运行时（runtime），并且在任何作用域中都可以被访问到。 在ES6之前，局部变量只能存在于函数体中，并且函数的每次调用它们都
<!--more-->
拥有不同的作用域范围。 局部变量只能在其被调用期的作用域范围内被赋值、检索、操纵。
```
function func() {
if (true) {
var tmp = 123;
}
console.log(tmp); // 123
}
```
之所以能够访问，是因为var关键字声明的变量有一个变量提升的过程。而在ES6场景，推荐使用let关键字定义变量：
 从ES6开始，你可以通过let关键字来定义变量，它修正了var关键字的缺点，能够让你像Java语言那样定义变量，并且支持块级作用域
 ```
 function func() {
if (true) {
let tmp = 123;
}
console.log(tmp); // ReferenceError: tmp is not defined
}
 ```
 这种方式，能够避免很多错误。
### 二、上下文
我理解我this关键字的指向
&emsp;上下文通常取决于函数是如何被调用的。当一个函数被作为对象中的一个方法被调用的时候，this被设置为调用该方法的对象上：
```
var obj = {
foo: function(){
alert(this === obj); 
}
};
obj.foo(); // true
```
&emsp;这个准则也适用于当调用函数时使用new操作符来创建对象的实例的情况下。在这种情况下，在函数的作用域内部this的值被设置为新创建的实例：
```
function foo(){
alert(this);
}
new foo() // foo
foo() // window
```
当调用一个为绑定函数时，this默认情况下是全局上下文，在浏览器中它指向window对象。需要注意的是，ES5引入了严格模式的概念， 如果启用了严格模式，此时上下文默认为undefined。
### 三、作用域链
&emsp;当代码在一个环境中执行时，会创建变量对象的一个作用域链（scope chain）。作用域链的用途是保证对执行环境有权访问的所有变量和函数的有序访问。 作用域链包含了在环境栈中的每个执行环境对应的变量对象。通过作用域链，可以决定变量的访问和标识符的解析。 注意，全局执行环境的变量对象始终都是作用域链的最后一个对象。我们来看一个例子：
```
var color = "blue";
function changeColor(){
var anotherColor = "red";
function swapColors(){
var tempColor = anotherColor;
anotherColor = color;
color = tempColor;
// 这里可以访问color, anotherColor, 和 tempColor
}
// 这里可以访问color 和 anotherColor，但是不能访问 tempColor
swapColors();
}
changeColor();
// 这里只能访问color
console.log("Color is now " + color);
```
### 四、闭包
&emsp;闭包是指有权访问另一函数作用域中的变量的函数。换句话说，在函数内定义一个嵌套的函数时，就构成了一个闭包， 它允许嵌套函数访问外层函数的变量。通过返回嵌套函数，允许你维护对外部函数中局部变量、参数、和内函数声明的访问。 这种封装允许你在外部作用域中隐藏和保护执行环境，并且暴露公共接口，进而通过公共接口执行进一步的操作。可以看个简单的例子：
```
function foo(){
var localVariable = 'private variable';
return function bar(){
return localVariable;
}
}
var getLocalVariable = foo();
getLocalVariable() // private variable
```
模块模式最流行的闭包类型之一，它允许你模拟公共的、私有的、和特权成员：
```
var Module = (function(){
var privateProperty = 'foo';
function privateMethod(args){
// do something
}
return {
publicProperty: '',
publicMethod: function(args){
// do something
},
privilegedMethod: function(args){
return privateMethod(args);
}
};
})();
```
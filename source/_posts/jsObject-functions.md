title: "jsObject_functions"
date: 2015-05-19 10:53:49
categories: js 相关笔记
tags: js 相关笔记
---
今天主要是弄了js相关函数的一些东西。整理如下：
<!--more-->
##Object函数
**1.object.hasOwnProperty(name) 函数的使用**
如果这个object包含了一个名为name的属性，那么该方法返回true。原型链中的同名属性是不会被检查的。这个方法对name就是hasOwnProperty时不起作用，此时会返回false。
```
if(typeof Object.beget !== 'function') {
	Object.beget = function(O) {
		var F = function() {};
		F.prototype = O;
		return new F();
	}
}
```
```
function hasOwnProperty1() {
	var a = {member: true};
	var b = Object.beget(a);
	var t = a.hasOwnProperty('member');
	var u = b.hasOwnProperty('member');
	var v = b.member;
	console.log(b);//b 是 {}
	console.log(t);//t 是 true
	console.log(u);//u 是 false
	console.log(v);//v 是 true
}
```

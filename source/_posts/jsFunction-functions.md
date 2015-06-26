title: "jsFunction_functions"
date: 2015-05-19 10:53:34
categories: Js 相关笔记
tags: Js 相关笔记
---
今天主要是弄了js相关函数的一些东西。整理如下：
<!--more-->
##Function 函数
**1.function.apply(thisArg,argArray) 函数的使用**
该方法调用函数function,传递一个将被绑定到this上的对象和一个可选的参数数组。apply方法被用在apply调用模式中。
```
Function.prototype.method=function(name,func){
	this.prototype[name] = func;
	return this;
}
```
```
Function.method('bind',function(that){
	//返回一个函数，调用这个函数就像它是那个对象的方法一样。
	var method = this,
		slice = Array.prototype.slice;
		args = slice.apply(arguments,[1]);
	return function() {
		return method.apply(
			that,
			args.concat(slice.apply(arguments,[0])));
	};
});
```
```
var x = function() {
	return this.value;
}.bind({value:666});
console.log(x());
```


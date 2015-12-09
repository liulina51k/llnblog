title: "Js-Dom编程概述"
date: 2015-06-26 15:43:54
categories: Js 相关笔记
tags: Js 相关笔记
---
为什么学习Dom编程？
原因如下几点：
1.  Dom编程 重要的作用是可以让用户对网页元素进行`交互`操作。
2.  Dom编程 用来做一些`网页游戏`
3.  Dom编程也是`ajax`的重要基础
<!--more-->
![Dom编程简介](/images/dom/dom1.png)
Dom的原理图：
![原理图](/images/dom/dom2.png)
从dom编程的角度，就会把该html文档，当做`dom树` 如下图：
![Dom树](/images/dom/dom3.png)
Bom------(BrowserObjectModel)浏览器对象模型
因为做浏览器的厂家很多，W3C定义了一个做`浏览器的规范`，规定：
![Bom简介](/images/dom/dom4.png)
![Dom对象简介](/images/dom/dom5.png)
![Dom对象一览图](/images/dom/dom6.png)
## Window 对象
![Window对象](/images/dom/dom7.png)
![Window属性](/images/dom/dom8.png)
## History对象
作用：该对象包含了`客户端访问过`的`URL`信息
![History对象](/images/dom/dom9.png)
## Location对象
该对象表示浏览器 loaction
Location 包含了`当前 URL `的信息。
![Location对象](/images/dom/dom10.png)
## Screen对象
![Screen对象](/images/dom/dom11.png)
![Screen属性](/images/dom/dom12.png)
## Navigator对象
![Navigator对象](/images/dom/dom13.png)
## 关于绑定事件的细节
![事件](/images/dom/dom14.png)
![事件对象](/images/dom/dom15.png)
![监听](/images/dom/dom16.png)

以上是对`Dom编程`的概述

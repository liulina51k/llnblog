title: "会话技术初识"
date: 2015-07-02 15:49:52
categories: Php 学习笔记
tags: Php 学习笔记
---
会话技术是php中必须掌握的技术，下面做下简单的介绍。。。
<!--more-->
##登陆状态验证 – 会话技术

在验证用户是`合法用户`后，`分配`一个`标识`，如果该操作需要登陆后才能执行，则先判断浏览器用户`是否携带登陆标识`。

![](/images/session/01.png)

上图中，绿色部分需要完成即可！

问题：标识是什么？
就是一个`特殊数据`而已。
需要将该标识，保存在哪里？
一定`要与浏览器`相关。

应该使用`会话技术`保存上面的登录标识数据；
`浏览器`与`服务器`在会话。
浏览器在于服务器的的`交互过程`中，处于`无状态`的情况下。`所谓无状态`，指的是`每个请求周期`（`请求-响应`）之间是`没有任何联系`的，`记录不下来`上次请求所处理的数据。

而`会话技术`，就是需要在`浏览器与服务器`的`多次请求响应周期`内，将`数据保存下来`的一门技术。
实现两种典型的：
cookie，session

##Cookie

直接将数据保存在`浏览器端`，浏览器在`发出请求`时，`携带`所保存的数据。服务器就可以在`每次执行`时，`获得上次所保存的数据`，从而`保证`会话期内的数据不丢失。

语法

setcookie()设置cookie数据的函数
$_COOKIE数组变量

如果需要`设置`（`增`，`删`，`修改`）一个cookie变量，使用函数`setcookie()`;
参数：setcookie(名字， 值)
如果需要获得设置的cookie数据，则需要`$_COOKIE数组`变量，`一个cookie数据`，就是$_COOKIE数组内个`一个元素`。

```
setcookie('admin','PHP');
var_dump($_COOKIE['admin']);
```

###实现原理

cookie保存在`浏览器端`，同时`PHP`是`利用cookie技术`保存数据，需要将`数据`由`服务器端`传递到`浏览器端`。
浏览器`请求时`将`cookie携带`。

`响应设置`

```
setcookie('admin','PHP');
```

数据在相应数据内，传递到浏览器端，浏览器依据该信息，`保存cookie变量`：

![](/images/session/02.png)

浏览器中可以查看到该数据：

![](/images/session/03.png)

`请求携带`

```
var_dump($_COOKIE['admin']);
```

在请求数据内，携带cookie变量：

![](/images/session/04.png)

此时服务器接收到请求，将`携带的cookie整理好`之后，`放入到$_COOKIE数组变量`内，`供PHP代码使用`。

`tip`
cookie是`浏览器上`保存数据的技术，PHP支持cookie技术，意味着，`PHP可以操作cookie而已`。

##Session

将数据保存在`服务器端`，同时为`数据分配一个唯一标识`，`浏览器`去`保存该唯一标识`。浏览器在`每次请求携带标识`过来，就可以查看到`属于该浏览器`的`特殊数据`。

语法

session_start();
$_SESSION数组

如果需要使用session技术，则先`开始session机制`。使用`session_start()`;
每个session数据，都是$_SESSION数组的内的一个元素，常规的操作`$_SESSION数组`，就`完成session数据`的处理。

`判断管理员已经合法`

![](/images/session/05.png)

`判断浏览器用户是否已经登陆`

![](/images/session/06.png)

###Session技术的实现原理

session数据保存在`服务器端`
数据具有`唯一标志性`
浏览器需要保存该标识，请求时携带，因此`典型的使用cookie保存该标识`。

![](/images/session/07.png)

当浏览器没有携带标识sessionID对服务器发出请求时
服务器会生成`唯一的sessionID标识`，并在响应时，`将标志传递给浏览器`，以`cookie的形式`进行保存。

```
session_start();
$_SESSION['data'] = yes;
var_dump($_SESSION['data']);
```

![](/images/session/08.png)

`tip`：
sessionID的`cookie变量名`为`PHPSESSID`，称之为`sessionName`。
`值为md5算法散列值`。

此时，会在服务器端上为该浏览器（会话）`生成`一个保存数据的独立并具有唯一标识的`空间`
默认的，PHP`以文件的形式`保存session数据，并保存在`系统的临时目录内`。

![](/images/session/09.png)

查看内容可知，session数据是`以序列化的形式`保存在文件中的：（可想而知，可以`保存任意类型`）

![](/images/session/10.png)

当浏览器存在sessionID发出请求时

![](/images/session/11.png)

此时服务器，得到sessionID，确定session数据的保存文件，可以获取之前所保存的session数据，`反序列后`，`存入$_SESSION数组内`，`供PHP程序处理`。

在后面还会向大家介绍
`cookie的高级操作`（`有效期`，`有效范围`，`有效域`）
`session高级操作`（`配置`，`入库`）

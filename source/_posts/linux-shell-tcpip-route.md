title: "linux之shell以及tcp ip以及包路由详解"
date: 2015-07-16 18:38:06
categories: Linux 学习笔记
tags: Linux 学习笔记
---
今天主要介绍linux中的`shell`，以及`tcp ip`基础，以及`ip地址`和`包路由`以及`网络环境配置`等相关内容。
<!--more-->
## shell的介绍

### shell概述

每个人在成功登陆linux后，系统会出现不同的提示符号，例如$、~、#等，然后你就可以开始输入需要的命令，若是命令正确，系统就会依据命令的要求来执行，直到注销系统为止；在`登录到注销`期间，输入的每个命令都会经过`解释及执行`。而这个负责的`机制`就是`shell`

### shell编程

其实作为命令语言互动式地解释和执行用户输入的命令只是`shell功能的一个方面`。shell还可以用来进行`程序设计`。它提供了`定义变量`和`参数`的手段以及丰富的`程序控制结构`。使用`shell编程`类似于`DOS中批处理文件`，称为`shell script`，又叫`shell程序`或`shell命令文件`

### shell的分类

| Shell名称    |  开发者    | 命令名称 |
| :--------    | --------:  | :--:     |
| Bourne       | S.R.Bourne |  /bin/sh |
| C            | Bill Joy   |  /bin/csh|
| Korn         | David      | /bin/ksh |

### shell的修改

`chsh –s` 输入新的shell

查阅历史记录
`history`，查看使用过的命令的历史记录
`history 5`，此项说明会显示最近使用的5个命令
`!5`，此项说明执行历史编号为5的命令
`!ls`，此项说明执行最后一次以“ls”开头的命令

环境变量的说明: env、set 可以用这两个命令查看一些环境变量的说明，直接输入即可

## tcp.ip基础

### 概述

`TCP/IP`是unix/linux世界的`网络基础`，在某种意义上，`unix网络`就是`TCP/IP`，而且`TCP/IP`就是网络互联的`标准`。它不是一个独立的协议，而是`一组协议`（`TCP`、`IP`、`UDP`、`ARP`等协议）.

每个Internet上的`主机和路由器`都有一个`IP地址`，它包括`网络号`和`主机号`，现在所用的IP地址都是`32`位的。`IP地址`按照国际标准划分为`A、B、C、D、E`五种类型

![](/images/linux/03.jpg)

![](/images/linux/04.jpg)

qq1 发送给 qq2 ，消息之间的通信过程如下：

![](/images/linux/05.jpg)

![](/images/linux/06.jpg)

## 网络环境配置

### 第一种方法

-用root身份登录，运行setup命令进入到text mode setup utility对网络进行配置，这里可以进行IP、子网掩码、默认网关、DNS的配置
-这时网卡的配置没有生效，运行/etc/rc.d/init.d/network restart命令我们刚才做的设置才生效
-ifconfig

### 第二种方法

-ifconfig eth0 x.x.x.x 对网卡进行设置
-ifconfig eth0 network x.x.x.x 对子网掩码设置
-对广播地址和DNS使用默认的
`Note`：这样配置网络将会立即生效，但是是临时生效

### 第三种方法

-修改/etc/sysconfig/network-scripts/ifcfg-eth0这个文件里各个属性可以修改，包括IP、子网掩码、广播地址、默认网关等
-这时网卡的配置没有生效，运行/etc/rc.d/init.d/network restart命令我们刚才做的设置才生效
`Note`：
-这种方法是最底层的修改方法
-在linux中，所有设备都是文件
-Tracert +”ip” 可以查看,访问所经过的路由器

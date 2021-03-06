title: "初识linux"
date: 2015-06-25 13:29:51
categories: Linux
tags: Linux
---
由于之前一直都是windows上开发，有人给我讲，真正想提高自己的编程水平，必须`从linux起步`，那才是`真正的编程`，一直都把linux放在一边了！我想从现在开始，一点点的将linux带入自己的编程中。慢慢的一点点提高自己。下面我将介绍linux的一些相关的基本知识。。。
<!--more-->
## linux的简介

linux 通过`minix`而来，minix通过`unix`而来。创始人是`Linus Torvalds`. `1991年`发布。linux 在`服务器领域`达到`80%`左右。

linux 分为 `内核版本`和`发行版本`。
linux内核版本就是`linux的核心`。linux内核官网：www.kernel.org
内核版本说明
2.6.18 其中2代表`主版本`，6代表`次版本`，18叫做`末版本`，如果更新不重要比较少，则更新末版本，如果更新比较大，累积到一定程度，就更新它的次版本，如果更新发生了很大的质的变化，最终才更新主版本。（越稳定越好）
目前最新的内核版本
3.16

发行版本（`内核一样`，加入自己不同的东西）
redhat (`服务器`方面更加常见)（稳定性和安全性高，一般不会出现图形界面)(部分收费，一些售后)
centos 跟redhat几乎一样，不收费。用户越来越多。（已被redhat收购）
suse
fedora redhat公司开发，属于`个人版`（和windows个人版不一样，windows个人版很多软件不能安装），功能很全面，但是不太安全。
debian ubuntu（界面更加炫）

## 开源软件简介

开源软件即`开放源代码`，不是编译的二进制，而是实实在在的`源代码`，怎么写的，就怎么给你。
linux中开源软件有很多
如Apache（网站服务搭建软件），NGINX(占用服务器资源更少，支持更高的并发)，Mysql，Php，Samba，mongoDB,Python,Ruby,Sphinx等。

`开源`和`免费`是不同的。

开源软件有一些特点:
1.使用的自由（绝大多数开源软件免费）
2.研究的自由（可以获得软件源代码）
3.散布及改良的自由（可以自由传播、改良甚至销售）

## Linux应用领域

1.基于Linux的企业服务器
2.Linux在嵌入式领域

## Linux学习方法

1.应该如何提问？
先要尝试自己解决-查看帮助文档（英文）-搜索引擎搜索-示例
提问的智慧-问题详尽-问题具体点-报错贴图

## Linux与Windows的不同

1.Linux严格`区分大小写`
2.Linux中所有内容以`文件形式`保存，包括硬件，`一切内容皆文件`
3.Linux`不靠扩展名区分文件类型`(通过`权限`来区分文件类型)
下面有一些`约定俗成`的写法（为了给管理员看）
压缩包："*.gz" 、"*.bz2" "*.tar.bz2" 、 "*.tgz" 等
二进制软件包：".rpm"
网页文件："*.html" 、 "*.php"
脚步文件："*.sh"
配置文件： "*.conf"
4.Windows下的程序`不能直接在Linux中安装和运行`（好处，病毒和木马都不能执行，坏处，都需要单独开发）

## 字符界面的优势

1.字符界面占用的`系统资源更少`
2.字符界面减少了出错、被攻击的可能性

#系统分区之分区与格式化

1.磁盘分区
`磁盘分区`是使用`分区编辑器`（partion editor）在磁盘上划分几个`逻辑部分`。碟片一旦划分成数个分区，不同类的`目录与文件`可以存储进不同的分区。

2.分区类型（windows，和linux都遵守）
`主分区`：最多只能有`4个`。
`扩展分区`：
最多只能有`1`个。
主分区加扩展分区`最多有4个`。
不能写入数据，只能`包含逻辑分区`。
`逻辑分区`

3.格式化（`根本目的`是`写入文件系统`）
`格式化`（高级格式化）又称`逻辑格式化`，它是指`根据`用户选定的`文件系统`（如FAT16、FAT32、NTFS、EXT2、EXT3、EXT4等），在`磁盘`的`特定区域`写入特定数据，在`分区`中划出一片用于`存放文件分配表、目录表`等用于`文件管理`的`磁盘空间`。

#系统分区之设备文件名与挂载

为分区起`硬件设备文件名`
| 硬件             |    设备文件名 		 | 
| :--------        | --------:           | 
| IDE硬盘          | /dev/hd[a-d]        |  
|SCSI/SATA/USB硬盘 | /dev/sd[a-p]        | 
| 光驱      	   | /dev/cdrom或/dev/hdc| 
| 软盘    		   | /dev/fd[0-1]        | 
| 打印机(25针)     | /dev/lp[0-2]        | 
| 打印机(USB)      | /dev/usb/lp[0-15]   | 
| 鼠标     		   | /dev/mouse          | 

挂载

`必须分区`
`/(根分区)`
`swap分区`（交换分区，内存2倍，不超过2G,4G以上的，swap分区占和内存一样的,小于4G的，则分到大于内存的2倍)(也可以叫`虚拟内存`)
`推荐分区`
`/boot`（启动分区，200MB）

文件系统结构
![文件系统结构](/images/filetree.jpg)

`挂载`指的是`盘符`和`分区`连接到一起的`过程`。`目录`就是`挂载点`。即`盘符`。

总结：
1.`分区`：把大硬盘分为小的逻辑分区
2.`格式化`：写入文件系统
3.`分区设备文件名`：给每个分区定义设备文件名
4.`挂载`：给每个分区分配挂载点

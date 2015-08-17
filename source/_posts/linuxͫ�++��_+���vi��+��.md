title: "linux之用户管理与vi编辑器"
date: 2015-07-16 11:59:53
categories: Linux 学习笔记
tags: Linux 学习笔记
---
今天还是为大家介绍linux的相关内容，以后要是有忘记得地方，可以来这里看看。
<!--more-->
##linux的第一次接触

`关机命令`
shutdown -h now 立即进行关机
shutdown -r now 现在重新启动计算机
-t sec : -t后面加秒数,即”过几秒后关机”
-k	 : 不是要真的关机,只是发送警告信息
-r	 : 在将系统的服务停掉之后就重新启动
-h	 : 将系统服务停掉后,立即关机
-n	 : 不经过init程序,直接以shutdown关机
-f	 : 关机并启动之后,强制略过fsck的磁盘检查
-F	 : 系统重新启动之后,强制进行fsck的磁盘检查
-c	 : 取消已经在进行的shutdown命令内容

![](/images/linux/01.jpg)

`reboot` 现在重新启动计算机

进入桌面
`startx`

`用户登录`
登录时尽量少用root账户登录，因为它是系统管理员，最大的权限，难免操作失误。可以利用普通用户登录，登录后再用“su -”命令来切换成系统管理员身份

`用户注销`
在提示符下输入logout即可

##vi编辑器的使用

###什么是vi编辑器?

`vi编辑器`是linux下最有名的编辑器，也是我们学习linux必须掌握的工具，在linux下也可使用vi进行程序的开发，如java程序，c程序

###如何使用vi进行开发？

在linux下使用vi开发一个简单的java程序Hello.java，并且在linux下运行成功

`开发步骤`
-`java程序`
-vi Hello.java
-输入i，进入到插入模式
-输入Esc键，进入命令模式
-输入冒号:[wq 表示退出保存，q!表示退出不保存]
-编译javac Hello.java
-运行java Hello

`c程序`
-gcc o Hello Hello.cpp[参数o表示可自定义生成的out文件名，否则默认为a. out]
-./Hello

##用户管理与目录结构

简单介绍
`linux的文件系统`是采用`层级式的树状目录`结构，在此结构中的最上层是根目录“/”，然后在此目录下再创建其他的目录
深刻理解linux文件目录是非常重要的

![](/images/linux/02.jpg)

`usr`，安装一个软件的默认目录，相当于windows下的program files

常用命令介绍

`pwd`，显示当前在哪个路径下

linux的用户管理

`useradd` 用户名，添加用户
```
useradd xiaoming
```

`passwd` 用户名，为新用户设密码

```
passwd xiaoming，修改小明的密码
```

`userdel` 用户名，删除用户

```
userdel xiaoming，删除用户但保存用户主目录
userdel ‐r xiaoming，删除用户以及用户主目录
```

`logout`，当前用户推出
`who am i`，当前用户是谁

##linux的部分常用命令

`init` [0123456]，指定系统运行级别，类似windows的正常运行模式或安全模式
-0：关机
-1：单用户
-2：多用户状态没有网络服务
-3：多用户状态有网络服务
-4：系统未使用保留给用户
-5：图形界面
-6：系统重启

常用运行级别是`3`和`5`，要修改默认的运行级别可改文件 /etc/inittab的id:5:initdefault:这一行中的数字

FAQ：不小心设置了6，导致系统启动-重启-启动循环，怎么办？
-在进入grub引导界面时，在数秒的时候，请输入 e
-然后选中第二行，输入e
-在出现的界面里，输入1【1表示单用户级别】，1的前面需要加一个空格，单用户模式既可以修改模式，又可以修改密码，Enter
-返回后，按b

`pwd`，显示当前工作目录(print working directory)
`pwd -p` 显示出实际路径,而非使用link路径.
`cd`，改变目录
`ls`，列出文件和目录
`ls ‐a`，显示目录下的所有文件，包括隐藏文件
`ls ‐l`，显示长列表格式
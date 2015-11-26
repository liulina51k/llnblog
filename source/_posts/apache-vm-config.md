title: "Apache中虚拟主机的配置"
date: 2015-07-03 16:00:10
categories: Php 学习笔记
tags: Php 学习笔记
---
在php开发中，会`配虚拟主机`也是一个必备技能，下面就介绍一下如何配置apache中的虚拟主机。。。
<!--more-->
#基于域名的虚拟主机
##配置虚拟主机
###把虚拟主机主配置文件前的注释打开

```
# Virtual hosts
Include conf/extra/httpd-vhosts.conf
```

`DocumentRoot` 站点的根目录
`ServerName` 站点的域名

###让浏览器知道去哪访问站点

我们打开`C盘`的一个叫`HOSTS`的文件
在里面添加`域名IP`的对应。
C:\Windows\System32\drivers\etc\hosts

```
127.0.0.1    test.100.com
127.0.0.1    shop.100.com
```

![](/images/virtualhost/01.png)

###目录访问权限设置

对于test.100.com
因为它的目录在htdocs的下级，所以它的目录`访问权限继承此站点`的配置

![](/images/virtualhost/02.png)

对于shop站点，没有特别给它进行配置，因此使用主配置文件中的`默认目录权限`

![](/images/virtualhost/03.png)

我们增加对shop站点的目录权限配置

![](/images/virtualhost/04.png)

`重启APACHE`

![](/images/virtualhost/20.png)

Order参数的作用
Order deny,allow
控制顺序用的，`谁在后面，谁起作用`。

![](/images/virtualhost/05.png)

###访问站点目录的情况

![](/images/virtualhost/06.png)

我们要讲一下`Options参数`的作用：
Options Indexes FollowSymLinks
如果配置了options indexes，则会出现`目录中文件的列表`
，否则`403`！

![](/images/virtualhost/07.png)

注意：我们在测试开发时，可以设置这个参数，方便我们从列表中选择文件运行
	如果是`正式上线的站点`，`一定`要去掉这个设置！
FollowSymLinks这个参数`允许访问文件符号链接`，`建议支持`。

###默认主机的变化

如果我们启用了虚拟主机配置文件conf/extra/httpd-vhosts.conf以后
首先原来默认的主机访问不到了，或者叫失效了。
其次，`默认的站点会指向第一个虚拟主机`。

###目录索引页

就是访问目录时我们指定的页面文件，称为`目录索引页`。
当前全局认可的一个参数

![](/images/virtualhost/08.png)

![](/images/virtualhost/09.png)

![](/images/virtualhost/10.png)

访问目录时，OPTIONS INDEXES和DIRECTORYINDEX的关系和影响

![](/images/virtualhost/11.png)

#APACHE的配置文件系统

##APACHE的主配置文件系统

Httpd.conf以及其包含的一系统配置文件如httpd-vhots.conf都属于`主配置文件`。
`虚拟主机的配置`会`覆盖主配置参数`。

##分布式配置文件系统

`分布式`：分布在各站点目录中的`配置文件`。
文件名：`.htaccess`
提示：一般直接在目录建立不了这个文件，可以用`编辑器`打开新文件，另存到目录中。
    AllowOverride None
此参数：如果是`none`，`不允许`分布式配置文件生效
		如果是`all`，则`允许`分布式配置文件覆盖主配置文件。

![](/images/virtualhost/12.png)	

结论：
如果AllowOverride all，则分布式配置文件的参数将起作用！
`分布式配置文件内容更改`，`不需要重启APACHE`！

可以在`分布式配置文件`中`修改PHP的配置参数`

![](/images/virtualhost/13.png)

我们在shop站点的分布式配置文件中修改PHP的session的一个参数	

![](/images/virtualhost/14.png)	

![](/images/virtualhost/15.png)

只对`本站点`有影响！

![](/images/virtualhost/16.png)

`Php_flag`开关性质的参数 on|off|1|0
`Php_value`字符串类的参数 字符串值内容

![](/images/virtualhost/17.png)

基本就介绍这些！！！

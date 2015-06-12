title: "PHP 中的错误处理(三)"
date: 2015-06-11 13:23:54
categories: php
tags: php
---
本文中主要介绍php如何`记录错误`以及如何`发送错误`等的相关知识。
<!--more-->
#记录和报告错误
1.将错误记录到`指定的文件`中
2.将错误记录到`系统日志`中
3.将错误以`邮件`形式发送

##将错误日志保存到`指定文件`中
在`php.ini`中通过`log_errors`等来开启错误日志。示例如下：
```
log_errors = On//开启错误日志
error_log = php_errors.log//错误日志存放位置
```
示例2
```
<?php
ini_set('display_errors',0);
ini_set('error_log','D:\chinaiiss\code\exceptions\testError.log');
error_reporting(-1);
echo $test;
echo '<hr/>';
settype($var,'king');
echo '<hr/>';
test();
```

##将错误日志保存到`系统日志`中
示例一：
```
<?php
error_reporting(-1);
ini_set('display_errors',0);
ini_set('log_errors',1);
ini_set('error_log','syslog');//保存到系统日志中中
echo $test;
echo '<hr/>';
settype($var,'king');
echo '<hr/>';
test();
```
系统日志可以通过 我的电脑->右击->管理->事件查看器->应用程序->信息中即可看到不同错误级别的信息文件。

示例二：通过`syslog()`来向系统日志中发送消息。
```
<?php
error_reporting(-1);
ini_set('display_errors',0);
ini_set('log_errors',1);
ini_set('error_log','syslog');
openlog('PHP5.3',LOG_PID,LOG_SYSLOG);//打开与系统日志的连接
syslog(LOG_ERR,'this is a test of syslog'.date('Y/m/d H:i:s'));//发送内容到系统日志
closelog();//关闭系统日志
```

##将错误以`邮件`形式发送
在紧急的情况下，将遇到问题以邮件的方式发给管理人员
首先要配置好`邮件服务器`。可以使用`mail`函数，`sendmail`服务器。
可以在`php.ini`的`[mail function]`下 配置如下：
```
sendmail_from=2047333472@qq.com
sendmail_path="D:\sendmail\sendmail.ext -t"
```
之后示例代码如下：
```
<?php
error_reporting(-1);
ini_set('display_errors',0);
ini_set('log_errors',1);
ini_set('error_log','syslog');
openlog('PHP5.3',LOG_PID,LOG_SYSLOG);//打开与系统日志的连接
syslog(LOG_ERR,'this is a test of syslog'.date('Y/m/d H:i:s'));//发送内容到系统日志
closelog();//关闭系统日志
```
以后我们也可以通过`自定义处理器`根据不同情况去完成不同的处理。
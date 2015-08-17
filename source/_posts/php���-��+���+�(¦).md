title: "PHP 中的错误处理(二)"
date: 2015-06-11 10:55:03
categories: Php
tags: Php
---
本文中主要介绍如何开启错误配置选项，如何设置错误级别，以及如何通过trigger_error()来触发php错误。
<!--more-->
#如何设置错误级别
1.通过修改`PHP配置文件`中的error_reporting选项的值
2.通过`error_reporting()`函数设置
3.通过`ini_set()`函数运行时设置

##php`配置文件`中与错误相关选项

| 选项              		|描述               | 
| :--------         		| --------:         |
| error_reporting   		|设置错误报告的级别 | 
| display_errors    		|是否显示错误       | 
| log_errors        		|设置是否将产生错误信息记录到日志或者error_log中 | 
| error_log         		|设置脚步错误将记录到的文件 | 
| log_errors_max_len		|设置log_errors的最大字节数| 
| ignore_repeated_errors   	|是否忽略重复的错误信息 | 
| ignore_repeated_source   	|是否忽略重复错误消息的来源 | 
| track_errors   			|如果开启此选项，最后一个错误将永远保存在 | 

在`php.ini`中可以通过`error_reporting`来`设置错误级别`，如
```
error_reporting = E_ALL&~E_NOTICE//显示所有的错误，除了注意消息
```
可以通过`display_errors = On/Off` 来`开启或者关闭错误`(除了解析错误，都会显示。一般线上的时候不会开启此选项)。

##通过`error_reporting()`函数设置
```
echo error_reporting();
echo '<hr/>';
//显示所有的错误
error_reporting(E_ALL&~E_NOTICE);
//屏蔽错误,屏蔽不掉解析错误
error_reporting(0);
//显示错误
error_reporting(-1);
echo $test;
echo '<hr/>';
settype($var,'king');
echo '<hr/>';
imooc();
```

##通过`ini_set()`函数运行时设置
```
//int_set():运行时设置配置选项的值
ini_set('error_reporting',0);//关闭错误显示
ini_set('error_reporting',-1);//开启
ini_set('display_errors',0);//不显示错误
```

##通过`trigger_error()`触发PHP错误
触发错误的功能不只限于`PHP解释器`，还可以通过`trigger_error()`函数触发错误.
```
//@抑制错误输出
@settype($var,'king');
```
```
$num1=1;
$num2='2a';
//判断$num1和$num2是否是合法数值
if(!(is_numeric($num1) && is_numeric($num2))) {
	//trigger_error('num1和num2必须为合法数值',E_USER_NOTICE);//Notice: num1和num2必须为合法数值 in D:\chinaiiss\code\exceptions\test3.php on line 11
	//程序继续向下执行
    //trigger_error('num1和num2必须为合法数值',E_USER_WARNING);//Warning: num1和num2必须为合法数值 in D:\chinaiiss\code\exceptions\test3.php on line 12
    //程序继续向下执行
    trigger_error('num1和num2必须为合法数值',E_USER_ERROR);//Fatal error: num1和num2必须为合法数值 in D:\chinaiiss\code\exceptions\test3.php on line 13
}else {
	echo $num1+$num2;
}
echo '<br/>程序继续向下执行';
```
以上就是所要介绍的全部内容。

title: "PHP 中的错误处理与异常(四)"
date: 2015-06-11 15:28:27
categories: php
tags: php
---
本文中主要介绍自定义错误处理器等的相关知识。
<!--more-->
自定义错误处理的主要实现是通过set_error_handle()函数:设置一个用户定义的错误处理函数。使用该函数会绕过php标准错误处理程序。

##使用set_error_handle()步骤
1.创建错误处理函数
2.设置不同级别调用函数
3.set_error_handler()函数指定接管错误处理

##set_error_handle()使用示例
```
<?php
header('content-type:text/html;charset=utf8');
error_reporting(-1);
function customError($errno,$errmsg,$file,$line){
	echo "<b>错误代码: </b>[{$errno}] {$errmsg}<br/>".PHP_EOL;
	echo "<b>错误行号: </b>{$file}文件中的第 {$line}行<br/>".PHP_EOL;	
	echo "<b>PHP版本: </b>".PHP_VERSION."(".PHP_OS.")<br/>".PHP_EOL;	
	//die;
}
set_error_handler(customError);
echo $test;
echo '<hr/>';
settype($var,'king');
echo '<hr/>';
//test();(没有办法手动捕获致命错误)
trigger_error('this is a test of error',E_USER_ERROR);//此时，虽然是致命错误，但由于自定义函数中，没有终止运行，程序还是会继续运行下去。
echo '<hr/>';	
//取消接管
restore_error_handler();
echo $king;
echo '<hr/>';
set_error_handler('customError',E_ALL&~E_NOTICE);//同时设定错误级别
echo $imooc;
echo '<hr/>';
settype($var,'king');
echo 'continue...';
```
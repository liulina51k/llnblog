title: "PHP 中的错误处理(四)"
date: 2015-06-11 15:28:27
categories: php
tags: php
---
本文中主要介绍`自定义错误处理器`等的相关知识。
<!--more-->
自定义错误处理的主要实现是通过`set_error_handle()`函数:设置一个`用户自定义`的`错误处理函数`。使用该函数会绕过`php标准错误处理程序`。

##使用`set_error_handle()`步骤
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
以上介绍了set_error_handler的使用，错误处理器的实现主要是借助它，这里就不再叙述了。

下面再说下关于错误处理中的另一个知识点，`register_shutdown_function()`函数的使用。
register_shutdown_function():通过该函数，可以让我们设置一个`当执行关闭时`可以`被调用`的另一个函数。
即：当我们的`脚步执行完成或意外死掉`导致PHP执行即将关闭时，我们的这个函数将会`被调用`。
#使用场景：
1.页面强制被停止
2.程序代码意外终止或超时
示例程序如下:
```
<?php
class shutdown {
	public function endScript(){
		if(error_get_last()){
			echo '<pre>';
			print_r(error_get_last());\\获取最后的错误
			echo '</pre>';
		}
		file_put_contents('D:\chinaiiss\code\exceptions\testError.txt', 'this is a test');//此处注意路径必须为绝对路径，否则会找不到路径。
		die('end script');
	}
}
register_shutdown_function(array(new shutdown(),'endScript'));//此函数之前不能有die,或exit。否则不会被执行。
echo md6();
```
以上就是关于php中`错误相关`的一些知识点。

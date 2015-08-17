title: "PHP 中的异常处理(一)"
date: 2015-06-12 17:25:44
categories: Php
tags: Php
---
本文中主要对php中的`异常`做下基本的介绍。
<!--more-->
##php中的`异常`处理
在接下来的几篇文章中，我会介绍如下的内容：
1.什么是`异常`？异常和错误有什么`区别`？
2.异常的`基本语法结构`。
3.如何`自定义异常类`？
4.如何`自定义异常处理器`？
5.如何像`处理异常`一样`处理PHP的错误`
6.在发生错误的时候将`用户重定向`到另一个页面

##异常
`异常`：程序运行与预期不太一致，与`错误`是`两个不同`的概念。
```
try{
	需要进行异常处理的代码段;
	throw 语句抛出异常;
	//...后面代码不会执行
} catch( Exception $e ) {
	...
} catch( Exception $e ) {
	.异常处理..
} catch( Exception $e ) {
	...
}
Continue...
//未捕获到异常时，会报致命错误。
//try 里面可以嵌套抛出异常。
```

示例代码一:
```
$num=NULL;
  try {
  	$num = 3/0;
  	var_dump($num);
  }catch(Exception $e) {
  	echo $e->getMessage();
  	$num=12;
  }
  echo '<hr/>';
  echo 'continue...';
  var_dump($num);
//Warning: Division by zero in D:\chinaiiss\code\exceptions\testException.php on line 13
//bool(false) 遇到错误，会报错，不会触发异常，须手动触发。
  echo '<hr/>';

  try {
  	$num1 = 3;
  	$num2 = 0;
  	if($num2 == 0) {
  		throw new Exception('o不能当做除数');//必须通过throw手动抛出异常。java中则可以自动抛出异常。
  		echo 'this is a test';//永远不会被执行
  	}else {
  		$res = $num1/$num2;
  	}
  }catch(Exception $e) {
  	echo $e->getMessage();
  	die();
  }
  //o不能当做除数
  echo '<hr/>';
  try {
  	if($username == 'king'){
  		echo 'hello king';
  	}else{
  		throw new Exception('非法管理员');
  	}
  }catch(Exception $e){//没有catch会报错
  	echo $e->getMessage();
  	echo '<hr/>';
  	die();
  }
  echo 'continue...';
```

示例代码二:`PHP内置异常类`
```
<?php
try {
  	$pdo = new Pdo("mysql:host=localhost;dbname=test",'root1','root');
  	var_dump($pdo);
  	echo '<hr/>';
  echo 'continue...';
}catch(PDOException $e){
  	echo $e->getMessage();
}
//SQLSTATE[28000] [1045] Access denied for user 'root1'@'localhost' (using password: YES)this is a test
echo 'this is a test';
echo '<hr/>';
try {
	$splObj = new SPLFileObject('txt.txt','r');
	echo 'read File';
}catch(Exception $e){
  	echo $e->getMessage();
}
echo '<hr/>';
echo 'hello world';
//SplFileObject::__construct(txt.txt) [splfileobject.--construct]: failed to open stream: No such file or directory hello world
```
错误必须`立即处理`，而异常可以`向上传递`，异常必须被捕获。

示例代码三
```
try {
	throw new Exception('测试异常1');
}catch(Exception $e){
  	echo $e->getMessage();
  	echo '<hr/>';
  	throw new Exception('测试异常1');
}catch(Exception $e){
	echo $e->getMessage();
}
echo '<hr/>continue';
//Fatal error: Uncaught exception 'Exception' with message '测试异常1' in D:\chinaiiss\code\exceptions\pdoException.php:28 Stack trace: #0 {main} thrown in D:\chinaiiss\code\exceptions\pdoException.php on line 28
```
正确的为：
```
try {
	throw new Exception('测试异常1');
}catch(Exception $e){
  	echo $e->getMessage();
  	echo '<hr/>';
  	try {
  		throw new Exception('测试异常2');
    }catch(Exception $e){
		echo $e->getMessage();
	}
}
echo '<hr/>continue';
//测试异常1
//测试异常2
//continue
```
以上就是对`异常基本知识`的介绍。
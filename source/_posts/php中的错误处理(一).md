title: "PHP 中的错误处理(一)"
date: 2015-06-10 17:04:18
categories: Php
tags: Php
---
接下来几篇文章将会介绍下php中的错误与异常，首先我们要知道二者是完全不同的概念，不能将二者混为一谈。本文中主要介绍php中的错误类型及其级别。
<!--more-->
#php中的错误处理

##php中常见的错误类型
1.`语法错误`（如少些分号，少花括号或括号，php会停止运行）
2.`环境错误`（脚本的运行环境，或和相关服务关联的问题，打开文件失败等。）
3.`逻辑错误`（不一定是代码错，如将== 写成 =，这种错误不会直接显示，而结果能看出来）

以后可以通过单元测试（是否达到想要的结果）来改进。

##php中常见的错误级别
1.`Deprecated`最低级别的错误(不推荐,不建议,可以继续执行)
```
//Deprecated: Function ereg() is deprecated
if(ereg('imooc','this is imooc show time',$matches)) {
	print_r($matches);
}else {
	echo 'nothing found';
}
echo '<hr/>';
echo mysql_escape_string('\' or 1=1 #');//use mysql_real_escape_string() instead.
```

2.`Notice`通知级别的错误（语法存在不当的地方（如为声明变量，下标问题），可以继续执行）
```
echo $king;//Notice: Undefined variable: king in D:\chinaiiss\code\exceptions\test.php on line 14
           //king
echo '<hr>';
$userInfo = array('username'=>'king','age'=>12);
echo $userInfo['username'];
echo '<hr/>';
echo $userInfo[age];//Notice: Use of undefined constant age - assumed 'age' in D:\chinaiiss\code\exceptions\test.php on line 19
                    //12
echo '程序继续向下执行';
```

3.`Warning`警告级别的错误(语法错误，丢了参数，参数类型值不正确，需要注意)
```
settype($var,'int');
var_dump($var);//int(0)
settype($var,'king');//Warning: settype() [function.settype]: Invalid type in D:\chinaiiss\code\exceptions\test.php on line 24
echo '<hr/>';
var_dump($var);//int(0)
echo '<hr/>';
echo '程序继续向下执行';
```

4.`Fatal error`致命级别的错误（终止执行，高级别）
```
echo md6('king');//Fatal error: Call to undefined function md6() in D:\chinaiiss\code\exceptions\test.php on line 28 
//不会向下执行
echo '程序继续向下执行';
```

5.`parse error`语法解析错误（高级别，解析阶段，之前的属于是运行阶段）
```
echo 'this is a test'//Parse error: syntax error, unexpected T_ECHO, expecting ',' or ';' in D:\chinaiiss\code\exceptions\test.php on line 30 (解析报错，什么都不会运行，不执行)
```

6.`E_USER_相关`的错误（用户自定义的错误，可以在手动抛出错误情况下使用）

以上就是对php中常见错误的总结。

在`php.ini`配置文件中也有对错误级别的说明,如下
```
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Error handling and logging ;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

; Error Level Constants:
; E_ALL             - All errors and warnings (includes E_STRICT as of PHP 5.4.0)
; E_ERROR           - fatal run-time errors
; E_RECOVERABLE_ERROR  - almost fatal run-time errors
; E_WARNING         - run-time warnings (non-fatal errors)
; E_PARSE           - compile-time parse errors
; E_NOTICE          - run-time notices (these are warnings which often result
;                     from a bug in your code, but it's possible that it was
;                     intentional (e.g., using an uninitialized variable and
;                     relying on the fact it's automatically initialized to an
;                     empty string)
; E_STRICT          - run-time notices, enable to have PHP suggest changes
;                     to your code which will ensure the best interoperability
;                     and forward compatibility of your code
; E_CORE_ERROR      - fatal errors that occur during PHP's initial startup
; E_CORE_WARNING    - warnings (non-fatal errors) that occur during PHP's
;                     initial startup
; E_COMPILE_ERROR   - fatal compile-time errors
; E_COMPILE_WARNING - compile-time warnings (non-fatal errors)
; E_USER_ERROR      - user-generated error message
; E_USER_WARNING    - user-generated warning message
; E_USER_NOTICE     - user-generated notice message
; E_DEPRECATED      - warn about code that will not work in future versions
;                     of PHP
; E_USER_DEPRECATED - user-generated deprecation warnings
```
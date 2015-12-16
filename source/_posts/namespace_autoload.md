title: namespace & autoload
date: 2015-12-16 23:30:44
categories: php
tags: php
---
本文将介绍命名空间，以及命名空间的使用，以及自动加载与自动加载的使用。。。
<!--more-->
## 命名空间

### 为什么使用命名空间？
1.工程越来越大，文件越来越多，命名冲突会越来越多。
2.代码越来越复杂，类也会越来越多，如何去管理这些类，如果有个包的概念，有层次的去区分每个类，会使得代码更规范，在java里面都有命名空间的概念，在php5.3里面也增加了命名空间的支持。

### 示例
```
\\test1.php
<?php
   //namespace Test1;

   function test() {
      echo __FILE__;
   }
```
```
\\test2.php
<?php
//namespace Test2;

function test()
{
    echo __FILE__;
}

```
```
\\test.php
<?php
require 'test1.php';
require 'test2.php';
```
会报如下错误
```
Fatal error: Cannot redeclare test() (previously declared in /home/zhonglingxiao/liulina/test/mooc/design-model/test1.php:5)
```
将test1，test2中的命名空间注释拿掉就不会用这个问题。

同时对命名空间的函数调用过程如下
```
//test.php 函数调用
Test1\test();
Test2\test();
```
最后执行结果为
```
/home/zhonglingxiao/liulina/test/mooc/design-model/test1.php/home/zhonglingxiao/liulina/test/mooc/design-model/test2.php
```
这就是命名空间的相关介绍。

## 自动加载

### 为什么使用自动加载？
之前，php都是手动通过include，require来载入依赖的文件的，当php的项目变大之后，php文件越来越多，一个php文件要依赖几十个php类，那就需要在整个代码之前，写几十行require，这样的话管理起来，包括开发的时候也很不方便，而且也容易产生，当某个类删除了的时候，而require没有去掉，这时候就会产生致命错误。越来越大之后，必须采用一种自动加载类的方式。在php5.2之后，就提供了类的自动载入功能。

### 示例
1.__autoload的使用
```
\\Test1.php
<?php
class Test1 {
    public static function test() {
        echo __METHOD__;
    }
}
```
```
\\Test2.php
<?php
class Test2 {
    public static function test() {
        echo __METHOD__;
    }
}
```
```
\\test.php
<?php
Test1::test();
Test2::test();

function __autoload($class)
{
    require __DIR__.'/'.$class.'.php';
}

```
后来autoload被废弃了，原因是我们一个php的工程可能会依赖多个框架，如果说每个框架都有一个这个函数，那就会报函数重复定义的致命错误，在php5.3之后呢，官方提供了一个spl_autoload_register()来取代autoload，该函数的特点是允许存在多个autoload函数，可以执行多次，如下：

2.spl_autoload_register的使用
```
\\test.php
<?php
spl_autoload_register('autoload1');
spl_autoload_register('autoload2');
Test1::test();
Test2::test();

function autoload1($class)
{
    require __DIR__.'/'.$class.'.php';
}
function autoload2($class)
{
    require __DIR__.'/'.$class.'.php';
}

```
这样多个这个函数，也不会报错。这样就会比第一种先进一些，也是目前采用的一种主要的方法。
执行结果：
```
Test1::testTest2::test
```
关于自动载入介绍到这里！


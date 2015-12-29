title: php面向对象的三种基础设计模式
date: 2015-12-29 22:39:59
categories: Oop
tags: Oop
---
三种基础设计模式,主要包括工厂模式,单例模式,注册树模式等,这三种模式是所有面向对象设计模式中最常见的三种,下面我来介绍。。。
<!--more-->
## 3种基本设计模式
- 工厂模式,工厂方法或者类生成对象,而不是在代码中直接new
- 单例模式,使某个类的对象仅允许创建一个
- 注册模式,全局共享和交换对象

## 工厂模式示例
工厂类如下：
```
//Factory.php
namespace IMooc;

class Factory
{
     static function createDatabase()
     {
         $db = new Database();
         return $db;
     }
}
```
调用如下：
```
//index.php
$db = IMooc\Factory::createDatabase();
```

## 单例模式示例
单例类如下：
```
//Database.php
namespace IMooc;

class Database
{
     protected = $db;
     private function __construct()
     {
     }
     static function getInstance()
     {
         if (self::$db) {
             return self::$db;
         } else {
             self::$db = new self();
             return self::$db;
         }
     }
}
```
调用类如下：
```
//index.php
$db = IMooc\Database::getInstance();
$db = IMooc\Database::getInstance();//无论调用多少次,实际上只创建一次.
```
可以修改工厂类如下(使用单例)：
```
class Factory
{
     static function createDatabase()
     {
         $db = Database::getInstance();
         return $db;
     }
}
```

## 注册树模式
注册树类如下：
```
//Register.php
class Register
{
      protected static $objects;
      static function set($alias, $object)
      {
          self::$objects[$alias] = $object;
      }
      static function get($name)
      {
          return self::$objects[$name];
      }
      function _unset($alias)
      {
          unset(self::$objects[$alias]);
      }
}
```
//注册过程如下:
```
class Factory
{
     static function createDatabase()
     {
         $db = Database::getInstance();
         Register::set('db1', $db);
         return $db;
     }
}
```
调用如下：
```
//index.php
$db = \IMooc\Register::get('db1');
```
以上就是对三种基础设计模式的介绍。。。
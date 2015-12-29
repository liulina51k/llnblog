title: php面向对象之适配器设计模式
date: 2015-12-29 23:33:37
categories: Oop
tags: Oop
---
下面介绍php面向对象的设计模式中的适配器设计模式,如下。。。
<!--more-->
## 适配器模式
- 适配器模式, 可以将截然不同的函数接口封装成统一的API

- 实际应用举例, PHP的数据库操作有mysql, mysqli, pdo3种, 可以用适配器模式统一成一致。类似的场景还有cache适配器, 将memcache, redis, file, apc 等不同的缓存函数, 统一成一致。

## 适配器模式模式示例
目录结果如下
![](/images/imooc/dir1.png)

定义的接口如下
```
//Database.php 定义接口
namespace IMooc;

interface IDatabase
{
      function connect($host, $user, $passwd, $dbname);
      function query($sql);
      function close();
}
```

MySQL实现
```
//MySQL.php
namespace IMooc\Database;

use IMooc\IDatabase;

class MySQL implements IDatabase
{
      protected $conn;
      function connect($host, $user, $passwd, $dbname)
      {
          $conn = mysql_connect($host, $user, $passwd);
          mysql_select_db($dbname, $conn);
          $this->conn = $conn;
      }
      function query($sql)
      {
          $res = mysql_query($sql, $this->conn);
          return $res;
      }
      function close()
      {
          mysql_close($this->conn);
      }
}
```

MySQLi实现
```
//MySQLi.php
namespace IMooc\Database;

use IMooc\IDatabase;

class MySQLi implements IDatabase
{
      protected $conn;
      function connect($host, $user, $passwd, $dbname)
      {
          $conn = mysqli_connect($host, $user, $passwd, $dbname);
          $this->conn = $conn;
      }
      function query($sql)
      {
          return mysqli_query($this->conn, $sql);
      }
      function close()
      {
          mysqli_close($this->conn);
      }
}
```

PDO实现
```
//PDO.php
namespace IMooc\Database;

use IMooc\IDatabase;

class MySQLi implements IDatabase
{
      protected $conn;
      function connect($host, $user, $passwd, $dbname)
      {
          $conn = new \PDO("mysql:host=$host;dbname=$dbname", $user, $passwd);
          $this->conn = $conn;
      }
      function query($sql)
      {
          return $this->conn->query($sql);
      }
      function close()
      {
          unset($this->conn);
      }
}
```

适配器调用如下
```
//index.php
$db = new IMooc\Database\MySQL();//在此可以数据库操作类切换,换成MySQLi,POD等.
$db->connect('127.0.0.1', 'root', 'root', 'test');
$db->query("show database");
$db->close();
```
以上就是对适配器模式的结束。。。
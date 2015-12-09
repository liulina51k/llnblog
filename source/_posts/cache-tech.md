title: "缓存技术"
date: 2015-06-01 17:40:43
categories: 缓存
tags: 缓存
---
缓存技术主要包括：
1，静态缓存
2，Memcache redis 缓存。
<!--more-->
## 静态缓存
静态缓存：保存在磁盘上的静态文件，用php生成数据放入静态文件中

php操作缓存
1，生成缓存
2，获取缓存
3，删除缓存

示例代码
将各种操作都统一封装在一个类中。
```
<?php

class File {
	private $_dir;
	const EXT = '.txt';
	public function __construct() {
		$this->_dir = dirname(__FILE__).'/files/';
	}
	public function cacheData($key,$value = '',$path = '') {
		$filename = $this->_dir.$path.$key.self::EXT;

		if($value !== ''){//将value值写入缓存
			if(is_null($value)){
				return @unlink($filename);
			}
			$dir = dirname($filename);
			if(!is_dir($dir)) {
				mkdir($dir,0777);
			}

			return file_put_contents($filename,json_encode($value));
		}

		if(!is_file($filename)){
			return false;
		}else{
			return json_decode(file_get_contents($filename),true);
		}
	}
}
```
## Memcache, Redis特点
1, Memcache和Redis都是用来管理数据的。
2, 他们数据都是存放在内存里的。
3, Redis可以定期将数据备份到磁盘（持久化）。
4, Memcache只是简单的key/value缓存。
5, Redis不仅仅支持简单的k/v类型的数据，同时还提供list, set, hash等数据结构的存储。

## Redis数据操作
1, 开启redis客户端
2, 设置缓存值 - set index-mk-cache '数据'
3, 获取缓存数据 - get index-mk-cache
4, 设置过期时间 - setex key 10 'cache'
5, 删除缓存 - del key
## redis命令行的相关操作
1, 安装redis扩展（不介绍）
2, 开启redis服务  
```
   cd redis 
   redis-server 6379.conf//(开启服务)
   cd /wxh/redis-stable/src 
   redis-cli //回车
```
3, 设置操作
```
   set singwa 12
```
4, 读取操作
```
   get singwa //(存在返回相应的值，不存在返回(nil))
```
5, 设置过期时间
```
   sexex singwa 12 gggss
```
6, 删除缓存
```
   del singwa 
```
## php 操作redis
1, 安装phpredis扩展
2, php链接redis服务-connect(127.0.0.1,6379)
3, set 设置缓存
4, get 获取缓存
用命令行来写php程序
```
cd /data/www/app 
```
```
sudo vim setCache.php
```
```
<?php
    $redis = new Redis();
    $redis -> connect('127.0.0.1',6379);
    $redis -> set('singwa1',123);
```
在app 目录下 执行 
```
php setCache.php //（可以自己测试,相关方法与命令行中用到的方法一样）；
```
按照如上的方式与步骤 可以自己进行自己的测试，在这里不赘述。

Memcache 相关操作与 redis 类似，可以查看php手册中的Memcache类。

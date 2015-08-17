title: "crontab 定时任务"
date: 2015-06-01 22:04:19
categories: Linux
tags: Linux
---
关于定时任务，我们需要了解一下相关内容：
1, 掌握如何设置定时任务常用命令
2, 掌握如何定时运行php程序
<!--more-->
##定时任务命令
1. 定时任务服务提供crontab命令来设定服务
2. crontab -e //编辑某个用户的cron服务
3. crontab -l //列出某个用户cron服务的详细内容
4. crontab -r //删除每个用户的cron服务

##具体事例
修改定时任务
```
sudo crontab -e
```
```
*/1 * * * * /usr/bin/php /data/www/12.php
```
编辑定时任务
```
sudo crontab -l
```
删除定时任务
```
sudo crontab -r
```
##定时任务格式
| 分 (*)  |  小时 (*)  | 日 (*)  | 月(*)  	|星期(*)  |命令|
| :-------- | --------:| :--: |
|  (0-59)  |   (0-23)     |  (1-31)   | (1-12)  | (0-6) | command|  
注: "*"代表取值范围内的数字
	"/"代表每、比如每分钟等

##定时任务crontab例子
```
*/1 * * * *  php /data/www/cron.php  //意思是每分钟执行cron.php
```
```
50  7 * * * /sbin/service sshd start //意思是每天7:50开启ssh服务
```
**如何设置每分钟向数据库中插入数据**
首先是写好php程序
```
<?php
   $connect = mysql_connect('127.0.0.1','','');
   mysql_select_db('test',$connect);
   $sql  = "insert into category(`name`, `create_time`) values('sssss', ".time().")";
   mysql_query($sql, $connect);
```
写计划任务
```
sudo crontab -e
```
写完保存即可自动运行
```
*/1 * * * * /usr/bin/php /data/www/app/cron.php
```
之后自己测试即可。
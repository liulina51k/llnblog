title: "伪静态技术之url重写"
date: 2015-07-02 14:16:07
categories: Php 学习笔记
tags: Php 学习笔记
---
`伪静态技术`是很重要的一部分，编程中经常会遇到，需要掌握。下面对其简单介绍下。
<!--more-->
通过伪造资源的URL，从而使浏览器（任何请求代理用户），认为所请求的资源为`静态资源`。
但是，当请求到达服务器时，服务器`根据`响应的静态URL，`解析`成动态的URL地址，从而使动态脚本执行。

动态网址：index.php?p=back&c=admin&a=login
静态网址：index.php/back/admin/login.html

目的：
`美化URL`。
`简化URL`。
`SEO，搜索引擎优化`。

技术实现
`Path-Info`
`Rewrite`
`URL路由`（项目中自身 实现）

下面主要介绍下url重写即 `Url Rewrite`

## URL-Rewrite URL重写

将请求的URL，`依据某种规则`，`更改`成其他的请求地址！是`web服务器Apache`一门技术。（其他web服务器都支持）
例如：隐藏框架的入口文件操作，就是典型的使用了重写技术：

```
<IfModule Rewrite-Module>
RewriteModule On
RewriteCond %{REQUEST_FILENAME}	!-d
RewriteCond %{REQUEST_FILENAME}	!-f
RewriteRule (.*) index.php/$1 [QSA,L]
</IfModule>
```

### 加载重写rewrite模块

Apache支持该技术。
Apache的配置文件中。使用`loadModule`指令完成：
```
LoadModule rewrite_module modules/mod_rewrite.so
```

`相应的指令`
RewriteEngine On\Off 	重写开关。
`重写条件`
RewriteCond 测试字符串条件表达式标记
`重写规则`
RewriteRule 测试URL目标URL标记

基本流程：
当前检测到请求到达该主机时，得到所请求的URL。依据用户通过`RewriteRule指令`设定的规则，`匹配目标URL`。与此同时需要`检测相应的条件`（使用语法RewriteCond完成）。

### RewriteEngine

该指令允许出现在：
`.htaccess`,` <Directory>`段，`<VirturalHost>`段。
具体参见Apache的手册：

![手册](/images/rewrite/03.png)

但是，常规的都在`.htaccess`文件中完成。
TIP：
此时，需要保证.htaccess文件生效，需要`主配置文件`中将该目录设置为`可以被分布式重写`的。

![](/images/rewrite/04.png)

AllowOverride的值，不一定是All，取决于重写指令的`覆盖项`的值。

### RewriteCond

重写条件。
当`重写规则匹配`之后。可以利用RewriteRule指令上面的`RewriteCond条件`指令，再指定是否重写的条件。之后`条件也满足`后，才会`发生重写效果`。

![](/images/rewrite/05.png)

`一条规则Rule`，可以受到`多个条件`的控制。

### RewriteRule

`重写规则`，指明`哪种URL`应该`被重写到目标URL`上。
RewriteRule匹配URL规则重写的目标URL

![](/images/rewrite/06.png)

其中，匹配的`URL规则部分`，是一个使用`正则语法`确定的规则。
利用某套规则，匹配相应的URL规则：

![](/images/rewrite/07.png)

`提示：正则语法的是通用的`。

### IfModule

用于判断`是否载入`了某个`模块`的。
<ifModule 模块名>
	载入模块执行的配置
</ifModule>

## 详细语法RewriteCond

RewriteCond`测试字符串测试条件`的标识

`测试字符串`
是一个字符串。可以使用`一些特定的变量`
例如：%{REQUEST_FILENAME}

常用的：
HTTP_USER_AGENT	请求代理信息
HTTP_REFERER		请求的来源
REQUEST_FILENAME	请求的脚本名

`测试条件`
可以是`正则表达式`，或者其他的`特殊指令`，例如：
正则表达式

`特殊指令`
`-f`	是否是文件
`-d`	是否是目录

### 示例一：浏览器相关主页

利用`当前浏览器`的不同，展示`不同的主页`。
```
RewriteCond %{HTTP_USER_AGENT} Firefox
```
`条件标志`
[条件标志列表]
`[NC]`	大小写不敏感
```
RewriteCond %{HTTP_USER_AGENT} Firefox [NC]
```

`[OR]` `默认`多个条件间为`逻辑与`的关系。增加`OR标志`后，就是`逻辑或`关系
```
RewriteCond %{HTTP_USER_AGENT} Firefox [NC,OR]
RewriteCond %{HTTP_USER_AGENT} Chrome [NC,OR]
RewriteRulr ^$ index_firefox.php
```

最终结果
```
RewriteCond %{HTTP_USER_AGENT} firefox [NC,OR]
RewriteRulr ^$ index_firefox.php

RewriteCond %{HTTP_USER_AGENT} MSIE [NC,OR]
RewriteRulr ^$ index_ie.php

RewriteRulr ^$ index.php
```

### 示例二：防止盗链

HTTP_REFERER
`请求来源`。
`功能`，用来：操作后，返回原始页面。（登录后）
`防止盗链`：`防止`其他网站（不允许的站点）`来访问`，`当前站点上`的资源（图片）
```
RewriteCond %{HTTP_REFERER} !localhost [NC]

```
以上条件，就可以匹配上`不属于localhost域`请求来源。

满足以上条件后，所有的`对图片`的请求，全都禁止！
```
RewriteRuleRule \.(jpg|jpeg|gif|png)$ - [F]

```
其中：
\.(jpg|jpeg|gif|png)$规则 指的是凡事以jpg,png等图片后缀结尾的，都匹配。

`-重写的URL`，表示`不予重写`的含义。
`[F]`规则标识F，表示Forbidden，`阻止该请求`的含义。

## RewriteRule的详细语法

RewriteRule `匹配规则` `重写目标规则`标志
`匹配规则`：正则表达式
`重写目标`：确定的URL地址，可以使用`反向引用`。

规则标志：
`F`	阻止
`L`	最后的规则。
`PT`	传递到下一个处理器（就是Apache执行的下一个步骤）
`QSA连接查询字符串`，query string append 是否将请求URL中的查询字符串部分，添加到目标URL中。
`差异`：在目标URL存在参数的情况下：

没有QSA：

![noQSA](/images/rewrite/a.png)

存在QSA：

![QSA](/images/rewrite/b.png)

可见，`追加的参数`，`覆盖``目标URL上`的`原有参数`。
`注意`：如果匹配URL是一个通用规则，例如TP中的隐藏入口文件脚本

![](/images/rewrite/c.png)

`注意`
重写规则是会`持续匹配`的。

![](/images/rewrite/d.png)

`建议`，定义规则时，`注意顺序`，`尽量少的定义重复规则`（循环规则），最好`匹配规则`配合上`重写条件``一起使用`！

#总结– `静态相关`的概念

`静态化`：直接生成静态页面HTML，浏览器访问静态页面。OB
`伪静态`：通过URL的形式，伪造静态地址错觉。（优化效果最弱，仅仅优化URL格式），Rewrite
`静态缓存`：将HTML代码临时保存起来，浏览器用户请求PHP脚本，php脚本判断是否使用，静态缓存。模板替换，写入文件
`数据缓存`：将中间数据存储在临时位置（文件中，特殊的小的表，内存中）。

以上技术是可以`结合`使用。

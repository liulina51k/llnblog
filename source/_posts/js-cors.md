title: js-cors
date: 2015-12-08 22:45:17
categories: Js 相关笔记
tags: Js 相关笔记
---
由于工作工作中,要用ajax进行跨域请求，所以把相关的知识点做了下总结，如下：
<!--more-->
## 目前有两种方式实现跨域,

#### 方式一：普通的jsonp方式进行跨域
```
//php：
$data = ['key1'=>'val1', 'key2'=>'val2'];
$callback = $_GET['callback'];
echo $callback . '(' . json_encode($data) . ')';
```
```
//html：
$.ajax({
    url: "http://www.test.com/php/cors.php",
    type: "get",
    dataType: "jsonp",
    success: function(data) {
        console.log(data);
    }
});
```

#### 方式二：可以向服务器传递cookie信息,以及文件等。客户端与服务器端对应的header信息要一致.
```
//php：
header("Access-Control-Allow-Origin: {$_SERVER['HTTP_ORIGIN']}");
header("Access-Control-Allow-Credentials: true");
header("Access-Control-Allow-Headers: withcredentials");
$data1 = ['key1'=>'val1', 'key2'=>'val2'];
echo json_encode($data1);
```
```
//html：
$.ajax({
    url: "http://www.test.com/php/cors.php",
    type: "get",
    headers: {
        withCredentials: true,
    }
    success: function(data) {
        console.log(data);
    }
});
```



title: PHP面向对象高级特性(一)
date: 2015-12-27 22:27:40
categories: Oop
tags: Oop
---
本文介绍下面向对象高级特性的一些使用。。。，如SPL库等的使用。。。
<!--more-->
## SPL库的使用(PHP标准库)
- SplStack, SplQueue, SplHeap, SplEixedArray等数据结构类
- ArrayIterator, AppendIterator, Countable, ArrayObject.
- SPL提供的函数

1.SplStack 的基本使用
```
$stack = new SplStack();
$stack->push("data1\n");
$stack->push("data2\n");

echo $stack->pop();
echo $stack->pop();
//data2 data1 先进先出
```

2.SplQueue 的基本使用
```
$queue = new SplQueue();
$queue->enqueue("data1\n");
$queue->enqueue("data2\n");

echo $queue->dequeue();
echo $queue->dequeue();
//data1 data2 先进后出
```

3.SplMinHeap 的基本使用
```
$heap = new SplMinHeap();
$heap->insert("data1\n");
$heap->insert("data2\n");

echo $heap->extract();
echo $heap->extract();
//data1 data2 先进后出
```

4.SplFixedArray 的基本使用
```
$array = new SplFixedArray(10);
$array[0] = 123;
$array[9] = 1234;

var_dump($array);
//object(SplFixedArray)#1 (10) { [0]=> int(123) [1]=> NULL [2]=> NULL [3]=> NULL [4]=> NULL [5]=> NULL [6]=> NULL [7]=> NULL [8]=> NULL [9]=> int(1234) }
```

## PHP链式操作的实现
1.传统的实现方式
```
$db = new IMooc\Database();
$db->where("id=1");
$db->where("name=2");
$db->order("id desc");
$db->limit(10);
```
2.链式方式
```
//Database.php中实现如下
class Database
{
    function where($where)
    {
        return $this;
    }
    function order($order)
    {
        return $this;
    }
    function limit($limit)
    {
        return $this;
    }
}
//调用如下
$db = new IMooc\Database();
$db->where("id=1")->where("name=2")->order("id desc")->limit(10);
// $db->where("id=1");
// $db->where("name=2");
// $db->order("id desc");
// $db->limit(10);
```

## PHP魔术方法的使用
- __get/__set
- __call/__callStatic
- __toString
- __invoke

1.__get/__set 的使用
```
//Object 类示例
class Object
{
     protected $array = array();

     function __set($key, $value)
     {
         echo __METHOD__;
         $this->array[$key] = $value;
     }
     function __get($key)
     {
         echo __METHOD__;
         return $this->array[$key];
     }
}
//调用使用
$obj = new IMooc\Object();
$obj->title = 'hello';
echo $obj->title;
//IMooc\Object::__setIMooc\Object::__gethello
```

2.__call/__callStatic 的使用
```
//Object 示例
function __call($func, $param)
{
  return "magic function\n";
}
static function __callStatic($func, $param)
{
  return "magic sttic function\n";
}
//调用使用
echo $obj->test("hello", 123);
//magic function
echo IMooc\Object::test("hello1", 1234);
//magic sttic function
```

3.__toString 的使用
```
//Object 示例
function __toString()
{
    return __CLASS__;
}
//调用使用
echo $obj;
//IMooc\Object
```

4.__invoke__ 的使用
```
//Object 示例
function __invoke($param)
{
  var_dump($param);
  return "invoke";
}
//调用使用
echo $obj("test1");
//string(5) "test1" invoke
```
基本介绍就这些!
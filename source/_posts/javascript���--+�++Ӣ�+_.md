title: "javascript中的内部类的介绍"
date: 2015-06-26 10:53:40
categories: Js 相关笔记
tags: Js 相关笔记
---
Javascript中本身有提供一些,可以直接使用的类, 这种类就是内部类, 主要有:
Object/Array/Math/Boolean/String/RegExp/Date/Number
<!--more-->
#内部类的分类
从`使用的方式`看，分为`静态类`和`动态类`
`静态类` 使用 类名. 属性/方法
```
Math.abs(-11)
```
`动态类` 使用 var 对象=new 动态类() 对象. 属性/方法
```
   //显示当前的日期
   var nowDate=new Date();
   window.alert(nowDate.toLocaleDateString());
```

下面介绍一些常用的`内部类`

##Math 类
Math类是`静态类`，提供了常用的`数学函数`和`常数`，下面介绍一些常用的函数，其余见手册。
```
console.log(Math.abs(-1));//1 (返回数的绝对值)
console.log(Math.ceil(4.5));//5 （对一个数进行上舍入）
console.log(Math.floor(4.5));//4（对一个数进行下舍入）
console.log(Math.max(4,5));//5 （求最大值）
console.log(Math.min(4,5));//4（求最小值）
console.log(Math.round(4.5));//5（对一个数进行四舍五入）
console.log(Math.random());//0.5753722707740963（一个大于0小于1的16位小数位的数字）
```
```
//返回1到100之间的随机数
console.log(Math.round(Math.random()*100));
```

##Date 类
Date类提供了`日期和时间`的操作，下面介绍一些常用的函数，其余见手册。
```
//日期Date类的使用，该类为动态类，该类需要通过对象来调用相应的方法。
console.log(Date()); //返回当前日期和时间
var date = new Date();
console.log(date.getDate()); //从Date对象返回一个月中的某一天
console.log(date.getDay()); //从Date对象返回一周中的某一天
console.log(date.getMonth()); //从Date对象返回月份
console.log(date.getYear()); //从Date对象返回年
console.log(date.getHours()); //从Date对象返回小时数
console.log(date.getMinutes()); //从Date对象返回分钟
console.log(date.getSeconds()); //从Date对象返回秒数
```

##String 类
String类是`动态类`，提供了对`字符串`的各种操作，下面介绍一些常用的函数，其余见手册。
1.indexOf() 返回某个字符串值在该字符串中`首次出现`的位置
```
//strObj.indexOf(subString[, startIndex])
//返回 String 对象内第一次出现子字符串的字符位置。
function IndexDemo(str2){
   var str1 = "BABEBIBOBUBABEBIBOBU"
   var s = str1.indexOf(str2);
   return(s);
}
console.log(IndexDemo('BI'));//4
```
2.lastIndexOf() 返回某个字符串值在该字符串中`最后出现`的位置
```
//strObj.lastIndexOf(substring[, startindex])
//返回 String 对象中子字符串最后出现的位置。
function lastIndexDemo(str2)
{
   var str1 = "BABEBIBOBUBABEBIBOBU"
   var s = str1.lastIndexOf(str2);
   return(s);
}
console.log(lastIndexDemo('BI'));//14
```
3.split() 把字符串`分割`为字符串数组
```
//stringObj.split([separator[, limit]])
//将一个字符串分割为子字符串，然后将结果作为字符串数组返回。
function SplitDemo(){
   var s, ss;
   var s = "The rain in Spain falls mainly in the plain.";
   // 在每个空格字符处进行分解。
   ss = s.split(" ");
   return(ss);
}
console.log(SplitDemo());//['The','rain','in','Spain',...,'plain.']
```
4.substr() 提取从start下标开始的`指定数目`的字符 
```
//stringvar.substr(start [, length ])
//返回一个从指定位置开始的指定长度的子字符串。
function SubstrDemo(){
   var s, ss;                // 声明变量。
   var s = "The rain in Spain falls mainly in the plain.";
   ss = s.substr(12, 5);  // 获取子字符串。
   return(ss);               // 返回 "Spain"。
}
console.log(SubstrDemo());//Spain
```
5.substring() 提取字符串中`介于两个指定下标之间`的子串
```
//strVariable.substring(start, end)或者"String Literal".substring(start, end)
//返回位于 String 对象中指定位置的子字符串。 
function SubstringDemo(){
   var ss;                         // 声明变量。
   var s = "The rain in Spain falls mainly in the plain..";
   ss = s.substring(12, 17);   // 取子字符串。
   return(ss);                     // 返回子字符串。
}
console.log(SubstringDemo());//Spain
```
6.charAt() 返回`指定位置`的`字符`
```
//strObj.charAt(index)
//返回指定索引位置处的字符。
function charAtTest(n){
   var str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"; // 初始化变量。
   var s;                                  // 声名变量。
   s = str.charAt(n - 1);                  // 从索引为n – 1的位置处
                                           // 获取正确的字符。
   return(s);                              //返回字符。
}
console.log(charAtTest(5));//E
```
7.length() 属性，可以得到字符串的`长度`
```
//strVariable.length"或者String Literal".length 
//返回 String 对象的长度。
```
8.toString() js中`所有内部对象`的成员方法，作用是将`对象中的数据`转换成某个格式的`字符串`。
```
//objectname.toString([radix]) radix 代表进制数
//返回对象的字符串表示。toString 方法是所有内建的 JScript 对象的成员
```
9.match() 
```
//stringObj.match(rgExp) 
//使用正则表达式模式对字符串执行查找，并将包含查找的结果作为数组返回。
function MatchDemo(){
   var r, re;         // 声明变量。
   var s = "The rain in Spain falls mainly in the plain";
   re = /ain/i;    // 创建正则表达式模式。
   r = s.match(re);   // 尝试匹配搜索字符串。
   return(r);         // 返回第一次出现 "ain" 的地方。
}
console.log(MatchDemo());//['ain',index:5,input:'The rain in Spain falls mainly in the plain']
function MatchDemo2(){
   var r, re;         // 声明变量。
   var s = "The rain in Spain falls mainly in the plain";
   re = /ain/ig;      // 创建正则表达式模式。
   r = s.match(re);   // 尝试去匹配搜索字符串。
   return(r);         // 返回的数组包含了所有 "ain" 
                      // 出现的四个匹配。
}
console.log(MatchDemo2());//['ain','ain','ain','ain']
```
10.replace()
```
//stringObj.replace(rgExp, replaceText)
//返回根据正则表达式进行文字替换后的字符串的复制。
function ReplaceDemo(){
   var r, re;                    // 声明变量。
   var ss = "The man hit the ball with the bat.\n";
   ss += "while the fielder caught the ball with the glove.";
   re = /The/g;             // 创建正则表达式模式。
   r = ss.replace(re, "A");    // 用 "A" 替换 "The"。
   return(r);                   // 返回替换后的字符串。
}
console.log(ReplaceDemo());//A man hit the ball with the bat.
//while the fielder caught the ball with the glove.
```
11.search() 
```
//stringObj.search(rgExp)
//返回与正则表达式查找内容匹配的第一个子字符串的位置。
//search 方法指明是否存在相应的匹配。如果找到一个匹配，search 方法将返回一个整数值，指明这个匹配距离字符串开始的偏移位置。如果没有找到匹配，则返回 -1。
function SearchDemo(){
   var r, re;                   // 声明变量。
   var s = "The rain in Spain falls mainly in the plain.";
   re = /falls/i;            // 创建正则表达式模式。
   r = s.search(re);            // 查找字符串。
   return(r);                   // 返回 Boolean 结果。
}
console.log(SearchDemo());//18
```

##Array 类
Array类提供了对`数组`的操作，使用Array类可以轻松的`创建数组`，并对数组进行`删除`，`排序`和`合并`等操作。
```
//Array类的使用，该类为动态类，该类需要通过对象来调用相应的方法。
//方式一
var myArr1 = new Array();
//可以动态的添加元素:myArr1[0] = 3;myArr1[1] = 'hello'.
//方式二
var myArr2 = new Array(12,34,3.56,"白骨精");
//myArr2[0] = '牛魔王';myArr2[1] = '红孩儿';myArr2[1] = '铁扇公主'.
//常用方法
myArr1.pop();//出栈
myArr1.push();//入栈
//Array类没有下标越界问题
```

##Boolean 类
```
//Boolean类的使用，该类是一个把布尔值打包的布尔对象，这个对象在实际编程中用的不是很多，了解即可。
//toString() 把逻辑值转换为字符串，并返回结果
//valueOf() 返回布尔对象的原始值
```

##Number 类
```
//Number类的使用，该对象是原始数值的包装类。常用的函数有:
//toString() 把一个Number对象转换为字符串，并返回结果
//toFixed() 把数字转换为字符串，结果的小数点后有指定位数的数字
//请输出23的二进制字符串和16进制的字符串
var b = 23;
console.log(b.toString(2));
console.log(b.toString(16));
```

#系统函数
js中的函数分为`三大类`，`自定义函数`，`js内部类的成员函数（方法）`，`系统函数`（全局函数）。
系统函数也叫全局函数，`可以直接使用`，是js设计者们为了编程方便提供的。
常见的一些`系统函数`如下：
1.eval() 
```
//eval() 可以把一个字符串当成一个脚步来运行，用处很大
//eval(codeString)
//检查 JScript 代码并执行. 必选项 codestring 参数是包含有效 JScript 代码的字符串值。这个字符串将由 JScript 分析器进行分析和执行。
eval("var mydate = new Date();");
//传递给 eval 方法的代码执行时的上下文和调用 eval 方法的一样. 
console.log(mydate);
```
2.parseInt() 
```
//parseInt() 把字符串转成正数
//parseInt(numString, [radix])
//返回由字符串转换得到的整数。
//parseInt 方法返回与保存在 numString 中的数字值相等的整数。如果 numString 的前缀不能解释为整数，则返回 NaN（而不是数字）。 
console.log(parseInt("abc"));    // 返回 NaN。
console.log(parseInt("12abc"));  // 返回 12。
```
3.parseFloat()
```
//parseFloat() 把字符串转成小数
//parseFloat(numString)
//返回由字符串转换得到的浮点数。
//parseFloat 方法返回与 numString 中保存的数相等的数字表示。如果 numString 的前缀不能解释为浮点数，则返回 NaN （而不是数字）。
console.log(parseFloat("abc"))      // 返回 NaN。
console.log(parseFloat("1.2abc"))  // 返回 1.2。
```
4.parse()
```
//Date.parse(dateVal)
//解析一个包含日期的字符串，并返回该日期与 1970 年 1 月 1 日午夜之间所间隔的毫秒数。
//parse 方法返回一个整数值，这个整数表示 dateVal 中所包含的日期与 1970 年 1 月 1 日午夜之间相间隔的毫秒数。 
//parse 方法是 Date 对象的一个静态方法。正因为它是一个静态方法，它是通过下面例子中所示的方法被调用的，而不是作为一个已创建 Date 对象的一个方法被调用。 
var datestring = "November 1, 1997 10:15 AM";
console.log(Date.parse(datestring));
```
5.isNaN()
```
//isNaN() //判断某个值是不是数（该函数不是特别完美）
//isNaN(numValue)
//如果值是 NaN， 那么 isNaN 函数返回 true ，否则返回 false 。 使用这个函数的典型情况是检查 parseInt 和 parseFloat 方法的返回值。 
//还有一种办法，变量可以与它自身进行比较。 如果比较的结果不等，那么它就是 NaN 。 这是因为 NaN 是唯一与自身不等的值。 
```
6.isFinite()
```
//isFinite(number)
//返回一个 Boolean 值,指明所提供的数字是否是有限的。
//如果 number 不是 NaN 、负无穷或正无穷，那么 isFinite 方法将返回 true 。 如果是这三种情况，函数返回 false 。 
```

最后总结：`内部类`和`系统函数`多查查`javascript参考手册`。
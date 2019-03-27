---
layout: ew
title: javascript内置对象Math、Date……
date: 2019-03-26 19:26:45
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- javascript # 可配置多个标签，注意格式
---
JavaScript提供了一些内置的对象和函数，内置对象提供编程的几种最常用的功能，JavaScript内置对象有以下几种。
Math对象：处理所有的数学运算
Date对象：处理日期和时间的存储、转化和表达
String对象：处理所有的字符串操作
Array对象：提供一个数组的模型、存储大量有序的数据
Boolean对象：布尔对象，一个布尔变量就是一个布尔对象(没有可用的属性和方法)
Number对象：数值对象,一个数值变量就是一个数值对象
RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具
Event对象：提供JavaScript事件的各种处理信息
 <!-- more -->
### 一、Math
与其它全局对象不同的是, Math 不是一个构造器.  Math 的所有属性和方法都是静态的. 
#### 1. 属性
下面列出来的属性，好像我用到过的就`Math.PI`.
```javascript
Math.E       // 2.718281828459045
Math.PI      // 圆周率，一个圆的周长和直径之比 3.141592653589793
Math.LN2     // 2的自然对数, 约等于0.693.
Math.LN10    // 10的自然对数, 约等于 2.303.
Math.LOG2E   // 以2为底E的对数, 约等于 1.443.
Math.LOG10E  // 以10为底E的对数, 约等于 0.434.
Math.SQRT1_2 // 1/2的平方根, 约等于 0.707.
Math.SQRT2   // 2的平方根,约等于 1.414.
```
#### 2.方法
一大堆方法里面，反正我用到的不是很多，相对较为常用的放在的了最下方，注意`ceil`，和`floor`值为负数的时候取整，不能被负数给带到坑里面了 
```javascript
Math.abs(x)    // 返回x的绝对值.
Math.acos(x)   // 返回x的反余弦值.
Math.acosh(x)  // 返回x的反双曲余弦值.
Math.asin(x)   // 返回x的反正弦值.
Math.asinh(x)  // 返回x的反双曲正弦值.
Math.atan(x)   // 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值.
Math.atanh(x)  // 返回 x 的反双曲正切值.
Math.atan2(y, x) // 返回 y/x 的反正切值.
Math.cbrt(x)   // 返回x的立方根.
Math.clz32(x)  // 返回一个32位整数的前导零的数量。
Math.cos(x)    // 返回x的余弦值.
Math.cosh(x)   // 返回x的双曲余弦值.
Math.exp(x)    // 返回 Ex, 当x为参数,  E 是欧拉常数 (2.718...), 自然对数的底.
Math.expm1(x)  // 返回 exp(x)-1 的值.
Math.fround(x) // 返回数字的最接近的单精度浮点型表示.
Math.hypot([x[,y[,…]]])  // 返回其参数平方和的平方根。
Math.imul(x)   // 返回32位整数乘法的结果。
Math.log(x)    // 返回一个数的自然对数（loge， 即ln）。
Math.log1p(x)  // 返回 1 加上一个数字的的自然对数（loge， 即ln）。
Math.log10(x)  // 返回以10为底数的x的对数。
Math.log2(x)   // 返回以2为底数的x的对数。
Math.max([x[,y[,…]]]) // 返回0个到多个数值中最大值.
Math.min([x[,y[,…]]]) // 返回0个到多个数值中最小值.
Math.sign(x)   // 返回x的符号函数, 判定x是正数,负数还是0.
Math.sin(x)    // 返回正弦值.
Math.sinh(x)   // 返回x的双曲正弦值.
Math.tan(x)    // 返回x的正切值.
Math.tanh(x)   // 返回x的双曲正切值.
Math.toSource()// 返回字符串 "Math".
Math.trunc(x)  // 返回x的整数部分,去除小数.

Math.round(x)  // 返回四舍五入后的整数.
Math.random()  // 返回0到1之间的伪随机数([0 1)包括0，不包括1）
Math.pow(x,y)  // 返回x的y次方.
Math.sqrt(x)   // 返回x的平方根.
Math.ceil(x)   // 返回x向上取整后的值（向上取整）.
Math.floor(x)  // 返回小于x的最大整数（向下取整）.
```
### 二、Date
Date对象基于1970年1月1日（世界标准时间）起的毫秒,`new Date()`根据本地时间返回，里面也有很多方法可以获取到指定的年月日时分秒毫秒等，也可以设置时间，值得注意的是，获取月份的时候是个坑，因为月份是从0开始的，获取月份（0-11）,也就是1月份是0，所以一般将获取到的月份`+1`，达到我们正常的（1-12）月
#### 1. 属性
Date.prototype 属性表示Date构造函数的原型
```javascript
Date.prototype 
```
#### 2. 方法
```javascript
var myDate = new Date()           // 创建一个日期对象
myDate.getFullYear()              // 返回年份 
myDate.getMonth()                 // 返回月份数（0-11） 
myDate.getDay()                   // 返回星期中第几天(0-6),想要得到星期几，需要+1
myDate.getDate()                  // 返回日
myDate.getHours()                 // 返回时
myDate.getMinutes()               // 返回分
myDate.getSeconds()               // 返回秒
myDate.getTime()                  // 返回从1970年1月1日00:00到现在的毫秒数(时间戳)
myDate.setFullYear()              // 设置年份(4位数)
myDate.setMonth()                 // 设置月份(0-11)
myDate.setDate()                  // 设置日(1-31)
myDate.setHours()                 // 设置小时数(0-23)
myDate.setMinutes()               // 设置分钟数(0-59)
myDate.setSeconds()               // 设置秒数(0-59)
myDate.setMilliseconds()          // 设置毫秒(0-999)
```

### 三、String
#### 1. 属性
```javascript
constructor    // 对创建该对象的函数的引用
length         // 字符串的长度
prototype      // 允许您向对象添加属性和方法
```
#### 2. 方法
```javascript
anchor()       // 创建 HTML 锚。
big()	       // 用大号字体显示字符串。	
blink()	       // 显示闪动字符串。	
bold()	       // 使用粗体显示字符串。
charAt()	   // 返回在指定位置的字符。
charCodeAt()   // 返回在指定的位置的字符的 Unicode 编码。	
concat()	   // 连接字符串。	
fixed()	       // 以打字机文本显示字符串。	
fontcolor()	   // 使用指定的颜色来显示字符串。
fontsize()	   // 使用指定的尺寸来显示字符串。
fromCharCode() // 从字符编码创建一个字符串。
indexOf()	   // 检索字符串。
italics()	   // 使用斜体显示字符串。
lastIndexOf()  // 从后向前搜索字符串。
link()	       // 将字符串显示为链接。
localeCompare()// 用本地特定的顺序来比较两个字符串。
match()	       // 找到一个或多个正则表达式的匹配。
replace()	   // 替换与正则表达式匹配的子串。
search()	   // 检索与正则表达式相匹配的值。
slice()	       // 提取字符串的片断，并在新的字符串中返回被提取的部分。
small()	       // 使用小字号来显示字符串。
split()	       // 把字符串分割为字符串数组。
strike()	   // 使用删除线来显示字符串。
sub()	       // 把字符串显示为下标。	
substr()	   // 从起始索引号提取字符串中指定数目的字符。
substring()	   // 提取字符串中两个指定的索引号之间的字符。
sup()	       // 把字符串显示为上标。
toLocaleLowerCase()	// 把字符串转换为小写。
toLocaleUpperCase() // 把字符串转换为大写。
toLowerCase()	    // 把字符串转换为小写。
toUpperCase()	    // 把字符串转换为大写。
toSource()	        // 代表对象的源代码。
toString()	        // 返回字符串。
valueOf()	        // 返回某个字符串对象的原始值。
```

>参考：[W3school](https://www.jb51.net/w3school/js/jsref_obj_regexp.htm)

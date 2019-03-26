---
layout: ew
title: js内置对象Math、Date……
date: 2019-03-26 19:26:45
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- javascript # 可配置多个标签，注意格式
---
生活中如果你没有对象，那么在js中就有啦，因为人们常说“万物皆对象”。
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
var mydate = new Date()           // 创建一个日期对象
mydate.getFullYear()              // 返回年份 
mydate.getMonth()                 // 返回月份数（0-11） 
mydate.getDay()                   // 返回星期中第几天(0-6),想要得到星期几，需要+1
mydate.getDate()                  // 返回日
mydate.getHours()                 // 返回时
mydate.getMinutes()               // 返回分
mydate.getSeconds()               // 返回秒
mydate.getTime()                  // 返回从1970年1月1日00:00到现在的毫秒数(时间戳)
mydate.setFullYear(yearInt)       // 设置年份(4位数)
mydate.setMonth(monthInt)         // 设置月份(0-11)
mydate.setDate(dateInt)           // 设置日(1-31)
mydate.setHours(hourInt)          // 设置小时数(0-23)
mydate.setMinutes(minInt)         // 设置分钟数(0-59)
mydate.setSeconds(secInt)         // 设置秒数(0-59)
mydate.setMilliseconds(milliInt)  // 设置毫秒(0-999)
```
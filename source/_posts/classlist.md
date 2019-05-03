---
title: 原生js中的classList
date: 2019-05-03 21:27:31
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- javascript # 可配置多个标签，注意格式
---

`element.classList` 操作元素的class属性，`obj.className`操作class, 但是二者区别还是很大的。
 <!-- more -->
 #### className
这里通过点击事件，直接就是将`class='box'`替换成了`class='active'`，元素上原来设置的`.box`样式也完全被`.active`替换掉了。
 ```javascript
    <div id="box" class="box"></div>

    var box = document.querySelector('#box');

    box.onclick = function(){
        box.className = "active"
    }

 ```
 #### classList
如果换成`classList`来设置，那么可以支持两个设置的属性同事存在，之前设置的那个的属性不会被覆盖
```javascript
    var box = document.querySelector('#box');

    box.onclick = function(){
    
        box.classList.add("active")
    
    }

```
`classlist`几种用法
```javascript
    add(String [, String])  //添加指定的类值。如果这些类已经存在于元素的属性中，那么它们将被忽略。
    remove(String [,String]) //删除指定的类值。
    item (Number) //按集合中的索引返回类值。
    toggle (tring [, force]) //当只有一个参数时：切换 class value; 即如果类存在，则删除它并返回false，如果不存在，则添加它并返回true。当存在第二个参数时：如果第二个参数的计算结果为true，则添加指定的类值，如果计算结果为false，则删除它
    contains(String) //检查元素的类属性中是否存在指定的类值。
    replace(oldClass, newClass) //用一个新类替换已有类。

```
示例
```javascript
const div = document.createElement('div');
div.className = 'foo';

// our starting state: <div class="foo"></div>
console.log(div.outerHTML);

// use the classList API to remove and add classes
div.classList.remove("foo");
div.classList.add("anotherclass");

// <div class="anotherclass"></div>
console.log(div.outerHTML);

// if visible is set remove it, otherwise add it
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10 );

console.log(div.classList.contains("foo"));

// add or remove multiple classes
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// add or remove multiple classes using spread syntax
const cls = ["foo", "bar"];
div.classList.add(...cls); 
div.classList.remove(...cls);

// replace class "foo" with class "bar"
div.classList.replace("foo", "bar");
```


---
title: jQuery事件绑定方式有哪些
date: 2019-03-25 22:53:08
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- jQuery # 可配置多个标签，注意格式
---

jQuery中提供了四种事件监听方式`bing、live、delegate、on`，对应的解除监听的函数分别是`unbind、lie、undelegate、off`
 <!-- more -->
1. bind()
直接绑定在元素上bind(type,[data],function(){})
type:事件类型，如click、change、mouseover等;
data:传入监听函数的参数，通过event.data取到。可选;
function:监听函数，可传入event对象，这里的event是jQuery封装的event对象，与原生的event对象有区别
```javascript
源码：
  bind: function( types, data, fn ) {

  return this.on( types, null, data, fn );

  }

$('#btn li').bind('click',function(){})
```
2. live()
通过冒泡的方式绑定到元素上的，更适合列表类型的，绑定到document DOM节点上，和bind()不一样，live支持动态数据
```javascript
live: function( types, data, fn ) {
 
jQuery( this.context ).on( types, this.selector, data, fn );
 
return this;
 
}
```
可以看到live方法并没有将监听器绑定到自己(this)身上，而是绑定到了this.context上了,正常来说就是document了，live没有将事件绑定在自己的身上而是事件委托绑在了document上

3. delegate()
参数多了一个selector，用来指定触发事件的目标元素，监听器将被绑定在调用此方法的元素上，小范围的使用事件代理，性能要优于live()
```javascript
delegate: function( selector, types, data, fn ) {
 
return this.on( types, selector, data, fn );
 
}
```
4. on
$(selector).on(event,childSelector,data,function)
1.7版本新添加的，也是推荐使用的事件绑定方法。其实bind、live、delegate都是通过该方法实现的：
```javascript   
bind: function( types, data, fn ) {
 return this.on( types, null, data, fn );
},
unbind: function( types, fn ) {
 return this.off( types, null, fn );
},

live: function( types, data, fn ) {
 jQuery( this.context ).on( types, this.selector, data, fn );
 return this;
},
die: function( types, fn ) {
 jQuery( this.context ).off( types, this.selector || "**", fn );
 return this;
},

delegate: function( selector, types, data, fn ) {
 return this.on( types, selector, data, fn );
},
undelegate: function( selector, types, fn ) {
 return arguments.length == 1 ? 
  this.off( selector, "**" ) : 
  this.off( types, selector, fn );
```
使用on方法和上面方法一样
```javascript
// Bind
$( "#members li a" ).on( "click", function( e ) {} ); 
$( "#members li a" ).bind( "click", function( e ) {} );

// Live
$( document ).on( "click", "#members li a", function( e ) {} ); 
$( "#members li a" ).live( "click", function( e ) {} );

// Delegate
$( "#members" ).on( "click", "li a", function( e ) {} ); 
$( "#members" ).delegate( "li a", "click", function( e ) {} );
```
> 参考：https://blog.csdn.net/liwenfei123/article/details/80408537
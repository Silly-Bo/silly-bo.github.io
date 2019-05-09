---
title: vue中v-model实现原理
date: 2019-05-09 21:40:56
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- VUE # 可配置多个标签，注意格式
---
vue中有很多指令，今天记录一下`v-model`指令的实现原理
 <!-- more -->
#### 一、先了解下input输入框中的 input事件
`oninput`事件在用户在输入元素值发生变化时立即触发；该事件在 `<input>` 或 `<textarea>` 元素的值发生改变时触发。

缺点： 
1. 从脚本中修改值不会触发事件。
2. 从浏览器下拉提示框里选取值时不会触发。
3. IE9 以下不支持，所以IE9以下可用onpropertychange事件（只在IE下支持，其他浏览器不支持  ）代替。
```html
<!-- js下面的方法使用 -->
 <input type="text" oninput="fn()">
```
#### 二、现在贴出在vue中的实现原理
```javascript
    <div id="app">
        <input type="text" v-bind:value="msg" v-on:input="change">
        <p>{{msg}}</p>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                msg: '我是内容'
            },
            methods: {
                change(e){
                    console.log(e.target.value)
                    this.msg = e.target.value
                }
            },
        })
    </script>
```
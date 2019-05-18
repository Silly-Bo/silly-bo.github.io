---
title: webpack4.x的使用
date: 2019-05-18 17:54:41
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- VUE # 可配置多个标签，注意格式
---
本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。
 <!-- more -->
### 一、安装
 在文件夹中先初始化项目生成`package.json`文件，便于更好的管理
```hash
    npm init --yes
```
通过`npm`下载`webpack`，这里下载的@4.27.1版本,注意`--save-dev`是开发环境下依赖
```hash
    npm install webpack --save-dev
```

### 二、简单打包小测试
 在创建的文件中分别创建`main.js`，`App.js`，`index.html`,然后再引入`vue.js`文件
 1. 文件目录
|--node_modules
|--App.js
|--main.js
|--index.html
|--vue.js
|--package.json

 1.1. main.js文件里:
```javascript
import Vue from './vue.js';
import App from './App.js';

new Vue({
    el:'#app',
    components:{
        App
    },
    template:`
        <App/>
    `
})
```
 1.2. App.js文件夹里:
```javascript
var app = {
    template:`
        <div>我是App文件</div>
    `
}
export default app
```
 1.3. index.html文件夹里:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="app"></div>
    <script src="./build.js"></script>
</body>
</html>
```
2. 打包
通过命令`webpack ./main.js -o ./build.js --mode 'development'`将文件目录中的文件打包
```hash
webpack ./main.js -o ./build.js --mode 'development'
``` 

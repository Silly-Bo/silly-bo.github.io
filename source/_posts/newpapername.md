---
title: Nginx
date: 2019-03-24 11:11:18
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- Nginx # 可配置多个标签，注意格式
---

### 一、安装
windows电脑可以通过点击[Nginx](http://nginx.org/en/download.html "nginx官方下载地址")到官方网址进行下载，Mac电脑可以通过brew(又叫homebrew，Mac中的一款软件包管理工具）通过命令进行下载，下面是通过Mac电脑演示
1. 安装
```hash
sudo brew install nginx
```
2. 启动Nginx服务
```hash
sudo brew services start nginx   
```
3. 关闭Nginx服务
```hash
sudo brew services stop nginx
```
4. 在浏览器地址栏输入`localhost:8080`,页面就会显示下图
![nginx](http://pord6y7be.bkt.clouddn.com/nginx.png)
5. 查看nginx安装目录
```hash
open /usr/local/etc/nginx/
```
6. 在打开的文件夹中找到`nginx.conf`文件并打开找到下面的这个代码，将前面的`#`去掉
```javascript
# include servers/*;
```
这里将前面的`#`去掉





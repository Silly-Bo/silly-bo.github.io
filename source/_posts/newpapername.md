---
title: Nginx安装和基础代理配置
date: 2019-03-24 11:11:18
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- Nginx # 可配置多个标签，注意格式
---
![nginx](http://pord6y7be.bkt.clouddn.com/nginx.jpg)
 <!-- more -->
### 一、安装
windows电脑可以通过点击[Nginx](http://nginx.org/en/download.html "nginx官方下载地址")到官方网址进行下载，Mac电脑可以通过brew(又叫homebrew，Mac中的一款软件包管理工具）通过命令进行下载，下面是通过windows电脑演示
1. 安装
点击[Nginx](http://nginx.org/en/download.html "nginx官方下载地址")到官方网址下载
2. 将下载的文件解压，放在的C盘下面，打开文件夹，找到`nginx.exe`直接点击启动，也可以通过CMD终端，cd到文件夹下输入strat nginx启动
```javascript
网上找的一些nginx常用命令
start nginx            开启nginx
nginx -s stop         快速关闭Nginx，可能不保存相关信息，并迅速终止web服务。
nginx -s quit         平稳关闭Nginx，保存相关信息，有安排的结束web服务。
nginx -s reload      因改变了Nginx相关配置，需要重新加载配置而重载。
nginx -s reopen      重新打开日志文件。
nginx -c filename    为 Nginx 指定一个配置文件，来代替缺省的。。
nginx -v             显示 nginx 的版本。
```
3. 启动后在浏览器地址栏输入`localhost:8080`,就会显示下图页面了
![nginx](http://pord6y7be.bkt.clouddn.com/nginx.png)

### 二、配置
1. 找到nginx解压后的文件夹，我的文件夹在c盘根目录
```hash
C:\nginx-1.14.2
```
2. 打开的文件夹中找到`nginx.conf`文件并打开，找到下面的这个代码，在下面加一段代码`include servers/*`,如果有这段代码，直接将前面的`#`去掉，然后在跟`nginx.conf`同级目录下，创建一个servers文件夹，文件夹下面创建一个`.conf`的文件，
```javascript
|--conf
   |--servers
      |--test.conf
   |--fastcgi.conf
   |--fastcgi_params
   |--koi-utf
   |--koi-win
   |--mime.types
   |--nginx.conf
   |--scgi_params
   |--uwsgi_params
   |--win-utf
|--contrib
|--docs
|--html
|--logs
|--temp
|--nginx.exe
```
```javascript
#gzip  on;   /*我这里是33行*/
include servers/*;  /*include在这里是导入servers下面所有的.conf文件*/
```
3. servers文件夹下`test.conf`文件配置
```javascript
server {
    #监听的端口号
    listen       80;

    #用来指定ip地址或者域名，多个配置之间用空格分隔,假如在本地运行，配置www.xx.com就需要去更改电脑的host文件
    #如何更改host：在C:\Windows\System32\drivers\etc目录下的host文件中添加一条DNS记录：127.0.0.1  www.test.com

    server_name  test.com;

    #反向代理代理服务器访问模式
    location / {
        proxy_pass   http://127.0.0.1:8888;  //代理的地址
    }
}
```
4. 通过node先启动一个服务
```javascript
const http = require('http');
http.createServer((req,res)=>{
    console.log('请求的地址',req.headers.host)
    res.end('请求了')
}).listen(8888)
```
5. 在浏览器地址栏输入`www.test.com`启动的server.js后台就会打印出来代理请求的地址
```hash
请求的地址 127.0.0.1:8888
```
6. 设置host
nginx为了实现反向代理的需求而增加了一个`ngx_http_proxy_module`模块。其中`proxy_set_header`指令就是该模块需要读取的配置文件。在这里，所有设置的值的含义和http请求头中的含义完全相同，除了Host外还有`X-Forward-For`。
Host的含义是表明请求的主机名，因为nginx作为反向代理使用，而如果后端的服务器设置有类似防盗链或者根据http请求头中的host字段来进行路由或判断功能的话，如果反向代理层的nginx不重写请求头中的host字段，将会导致请求失败【默认反向代理服务器会向后端真实服务器发送请求，并且请求头中的`host`字段应为`proxy_pass`指令设置的服务器】。
  同理，`X_Forward_For`字段表示该条http请求是有谁发起的？如果反向代理服务器不重写该请求头的话，那么后端真实服务器在处理时会认为所有的请求都来在反向代理服务器，如果后端有防攻击策略的话，那么机器就被封掉了。因此，在配置用作反向代理的nginx中一般会增加两条配置，修改http的请求头：
```
proxy_set_header Host $http_host;
proxy_set_header X-Forward-For $remote_addr;
```
这里的`$http_host`和`$remote_addr`都是nginx的导出变量，可以再配置文件中直接使用。如果Host请求头部没有出现在请求头中，则$http_host值为空，但是$host值为主域名。因此，一般而言，会用`$host`代替`$http_host`变量，从而避免http请求中丢失Host头部的情况下Host不被重写的失误。
```javascript
location / {
        proxy_pass   http://127.0.0.1:8888;  //代理的地址
        proxy_set_header Host $host;
        proxy_set_header X-Forward-For $remote_addr;
    }
```
这个时候server.js下面打印的地址就是指定的host了
```hash
请求的地址 www.test.com
```



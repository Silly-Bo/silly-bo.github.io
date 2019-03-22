---
title: hexo写博客与发布
date: 2019-03-22 14:11:32
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
# - 实用技术 # 一级分类
- 个人博客 # 二级分类 
tags:   # 这里写的标签会自动汇集到 tags 页面上
- 实用 # 可配置多个标签，注意格式
- 个人博客
# photos:  #在首页摘要中显示文章图片
#     - "http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322162122.png" 
---

### 一、写博客
刚开始时候不知道怎么设置标签和分类，然后网上找了一些资料搞定了，记录一下，先创建一个.md的文件放到 `/source/_posts `文件夹中，在刚建的.md文件中进行一系列的操作。
 <!-- more -->
#### 操作
先在git bash中命令新建.md的文件
```hash
 hexo new newpapername
```
然后`source/_posts`文件夹下面新创建个newpapername.md文件，打开newpapername.md文件就可以写自己的东西了，原来自动生成的是下面的样子

```javascript
---
title: newpapername
date: 2019-03-22 15:38:48
---
```
这个时候根据自己文章的内容进行分类和添加标签，下面是这篇文件设定的标签和文件夹
```javascript
---
title: hexo写博客与发布
date: 2019-03-22 14:11:32
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
# - 实用技术 # 一级分类
- 个人博客 # 二级分类 
tags:   # 这里写的标签会自动汇集到 tags 页面上
- 实用 # 可配置多个标签，注意格式
- 个人博客
---

```
这里我只设置了一个分类，默认是一级分类，生成后的图片如下
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322154430.png)

这里点击分类的时候显示就能显示自己设定的个人博客分类了
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322161547.png)

上面设定了两个标签，一个是实用，一个是个人博客，现在也一样可以显示了
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322162122.png)

补充一下：将本地图片截取的图片生成在线地址，我这里用的是[七牛云](https://portal.qiniu.com/signup?code=3lpiscgrmeb82)地址已经贴上。

### 二、发布到github

#### 操作
1. 生成SSH添加到GitHub
在git bash 中输入命令，设置用户名和邮箱
```bash
git config --global user.name "yourname"
git config --global user.email "youremail"
```
2. 然后创建SSH,一路回车
```bash
ssh-keygen -t rsa -C "youremail"
```
这个时候电脑C盘里面就生成了.ssh的文件夹
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322173438.png)

简单的说`ssh`就是一个密钥，`id_rsa`是私人秘钥，不能给别人看的，`id_rsa.pub`是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。然后在GitHub的settings中找到SSH and GPG keys 选项
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322174135.png)

3. 查看是否成功
```bash
ssh -T git@github.com
```

4. 将hexo部署到GitHub
我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 _config.yml，翻到最后，修改
YourgithubName 就是你创建的gitHub名字。
```javascript   
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```
5. 安装`deploy-git`,也就是部署的命令,这样你才能用命令部署到GitHub。
```bash
npm install hexo-deployer-git --save
```
6. 然后执行
```bash
hexo clean      
hexo generate  # 可以缩写 hexo g
hexo deploy    # 可以缩写 hexo d      
```
注意deploy时可能要你输入username和password。
7. 部署到GitHub出现404页面
出现这个问题的主要原因是因为起名字的时候没有和前面博客名字保持一致，只需要在settings中将名字改成一致，保存后，刷新页面即可
![示例](http://pord6y7be.bkt.clouddn.com/QQ%E6%88%AA%E5%9B%BE20190322182508.png)

### 三、 在其他电脑上操作
1. 跟上面一样需要安装`安装git，安装node，安装hexo，安装配置name，配置邮箱名，配置ssh key密钥……等`
```javascript
git，
配置name，
配置邮箱名，
生成ssh key  与github配置授权

```
2. 将github上面的代码克隆下来
```hash
git clone git@github.com:Silly-Bo/Silly-Bo.github.io.git
```
3. 进入到克隆的文件仓库中
```hash
cd xxx.github.io
npm install 
npm install hexo-deployer-git --save
```
4. 生成、部署
```hash
hexo g 
hexo d
```
5. 可以写新博客了
```hash
hexo new newpage
```
6. 别忘记提交
```hash
git add . 
git connit -m 'XXXX'
git push
```
7. 如果已经在克隆过的电脑上要实用的话，需要先拉新项目
```hash
git pull
```




> 参考：[zjufangzh](https://blog.csdn.net/sinat_37781304/article/details/82729029)
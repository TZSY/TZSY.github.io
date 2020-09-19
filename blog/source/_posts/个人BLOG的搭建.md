---
title: 个人BLOG的搭建
date: 2020-09-19 15:23:46
tags: 教程

---

#  搭建blog的流程

##  前言

​	近来学习git的用法，尝试使用github来管理自己的文件，干脆就继续搭一个git的blog，以后估计也会一直维护，不断改进。正好完成该blog的第一个post。

​	搭建环境是ubuntu，这篇仅仅只是搭建。

​	在搭建时建议进入root模式，避免权限问题，如下进入

```
$sudo su
```



##  安装nodejs和npm

​	在网上了解了一下，选择了hexo框架来搭建blog，前置当然是要下载的。

```
$ apt install node//安装nodejs
$ apt install npm//安装npm
$ npm install -g cnpm --registry=http://registry.npm.taobao.org
//换taobao的源用npm下载cnpm
//安装完成可以使用--version查看版本
```

##  全局安装hexo

```
$ cnpm install -g hexo-cli
$ hexo --version//查看版本，检查是否成功
```

接下来决定安装目录

```
$ pwd
username//个人文件夹，各自选择
$ mkdir blog //在当前目录下创建blog文件夹，后续操作全部在此文件夹下，名字各自取
$ cd blog//进入blog
```

接下来开始用hexo搭建blog

```
$ hexo init
INFO Clioning hexo-starter to /User/username/blog
...
Clioning into "/User/username/blog/themes/landscape"...
//初始给你了个landscape的主题
...
INFO Start blogging with Hexo!
```

hexo目前已经安装完整。

##  启动blog

```
$ hexo s//启动hexo博客
INFO Start processing
INFO Hexo is running at http://localhost:4000. Press Ctrl+C to stop.
```

​	在浏览器输入localhost:4000，就能看到目前生成在本地的blog了。

​	Hexo给你新建了一个HelloWorld文章，里面有hexo的一些操作，可以关注一下。

##  写post

​	现在写一篇自己的post。

```
hexo n "我的第一篇博客文章"//new了一个名字为“我的第一篇博客文章”的markdown文件。
```

​	该post在blog的下属文件夹

```
$ cd source/_posts/
```

​	用vim或者别的什么markdown工具编辑文件

```
---
title: 我的第一篇博客文章
date: 2020-0x-0x 12:20:20
tags: 标签
---
注意在上面：的后面一定要接一个空格
```

​	保存退出，接下来退回blog文件夹下

```
$ cd ../..
$ pwd
/Users/username/blog
```

​	然后进行下面的操作

```
$ hexo clean
$ hexo g//生成hexoblog
$ hexo s//再次启动hexo
```

​	之后刷新一下localhost:4000，就可以发现已经提交了新的post。

##  部署到github上

​	第一步，当然是登录github

​	第二步，新建一个库，库名为 xxxx.github.io(注意xxxx是你的名字，比如我是TZSY，就是TZSY.github.io),必须符合要求。随意写下description然后create repository就完事了。

​	然后回到shell，安装一个工具

```
$ cnpm install --save hexo-deployer-git
```

​	安装完成，我们就需要配置这个工具了。打开_config.yml，我照样使用vim打开。

```
$ vim _config.yml
```

​	到最底部

```
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type:
```

​	改成

```
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/xxxx/xxxx.github.io.git
  branch:master
```

​	xxxx是各自的昵称，当然可以去github那边直接复制这个https://.....;branch不写就是默认master，要改分支就改成自己想要的分支。

​	_config.yml目前就修改完成了，下一步就是部署到远端。

```
$ hexo d
Username for "https://github.com":
Password for "https://xxxx@github.com":
输入就完事了
```

​	可能还会有报错，我遇到的是没有global设置

```
$ git config --global user.email "xxxx@xx.com"
$ git config --global user.name "xxxx"
```

​	设置完成后再

```
$ hexo d
```

​	就部署成功了，可以使用xxxx.github.io访问了。
##  主题的更换

​	还是在blog目录下操作

```
$ git clone http://github.com/litten/hexo-theme-yilia.git themes/yilia
```

​	这是一个叫yilia的hexo主题，大家可以自行寻找其他的主题，还是一样的操作。

​	修改_config.yml中的theme行

```
$ theme: landscape  
改成
$ theme: yilia
```

​	保存退出。

```
$ hexo clean
$ hexo g
$ hexo s
$ hexo d
```

​	然后进去之后再按照各自主题的说明进行对_config.yml的修改。

##  参考资料

​	搭建blog的大部分内容都参考于B站CodeSheep的讲解视频。非常感谢他的视频对我的指导。以下贴出视频链接：https://www.bilibili.com/video/BV1Yb411a7ty/



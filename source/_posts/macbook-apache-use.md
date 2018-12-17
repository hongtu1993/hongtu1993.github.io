---
title: macbook apache use
author: 毛宇鹏
date: 2018-12-13 14:02:08
subtitle:
showTitle: macbook自带apache使用
description: Apache是世界使用排名第一的Web服务器软件。平时我们可以将html文件放到apache的root目录的话，就可以通过ip地址去访问。。。当然，apache支持运行php环境，而mac下，apache和php都已经默认安装好的了，关键是我们怎么去使用...
tags:
    - macbook
    - apache
categories:
    - macbook
---

笔者机器：mac pro ox10.10
## macbook自带apache简单介绍
### apache
Apache是世界使用排名第一的Web服务器软件。平时我们可以将html文件放到apache的root目录的话，就可以通过ip地址去访问。。。当然，apache支持运行php环境，而mac下，apache和php都已经默认安装好的了，关键是我们怎么去使用...

### mac下apache的目录

在终端输入命令,打开`/etc`文件夹(如下图)，看以看到`apache2`文件夹，这个文件夹就是apache的安装目录。

    open /etc

![查看mac下apache的安装目录](http://upload-images.jianshu.io/upload_images/1687958-3e26ee72d5063e47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### apache的httpd.conf扼要解读

![httpd配置文件](http://upload-images.jianshu.io/upload_images/1687958-6afb8fb01f8ac83f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

        #端口监听，下面配置的意思是apache启动后会监听80端口
        Listen 80

        #apache的root目录，这里可以根据个人需求去修改
        #例如：把`index.html`放到`/Library/WebServer/Documents`下，就可以使用 127.0.0.1/index.html 去访问
        DocumentRoot "/Library/WebServer/Documents"

### 启动apache
        sudo apachectl start/restart

### 测试
打开浏览器，输入localhost

![测试页面](http://upload-images.jianshu.io/upload_images/1687958-7b0a377013cf6d50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



---
title: macos-built-in-use-of-apache
author: 毛宇鹏
date: 2020-03-05 14:27:19
subtitle:
showTitle: MacOs自带的apache使用
description: 配置Macbook Macos系统内置的apache, 使用与开机启动
tags:
    - mac
    - apache
categories:
    - computer
---

笔者机器：mac pro ox10.10

## macbook自带apache简单介绍

### apache

Apache是世界使用排名第一的Web服务器软件。平时我们可以将html文件放到apache的root目录的话，就可以通过ip地址去访问。。。当然，apache支持运行php环境，而mac下，apache和php都已经默认安装好的了，关键是我们怎么去使用...

### mac下apache的目录

在终端输入命令,打开`/etc`文件夹(如下图)，看以看到`apache2`文件夹，这个文件夹就是apache的安装目录。
        
    open /etc

![查看mac下apache的安装目录](http://qiniu.maoyupeng.club/mweb/15833897996731.png)

#### apache的httpd.conf扼要解读

![httpd配置文件](http://qiniu.maoyupeng.club/mweb/15833898610752.png)

        #端口监听，下面配置的意思是apache启动后会监听80端口
        Listen 80

        #apache的root目录，这里可以根据个人需求去修改
        #例如：把`index.html`放到`/Library/WebServer/Documents`下，就可以使用 127.0.0.1/index.html 去访问
        DocumentRoot "/Library/WebServer/Documents"

### 启动apache

        sudo apachectl start/restart

### 测试

打开浏览器，输入localhost

![测试页面](http://qiniu.maoyupeng.club/mweb/15833898867186.png)




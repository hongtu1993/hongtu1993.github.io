---
title: install-centos-6-6-on-virtual-box
author: 毛宇鹏
date: 2019-03-25 20:06:03
subtitle: VirtualBox上安装Centos6.6系统
showTitle: 在VirtualBox上安装Centos6.6系统
description: 记录下在VirtualBox上安装系统, 把遇到的坑重新复习一遍. 不单单包含安装内容, 还包括Centos6.6配置静态ip,Centos6.6安装配置jdk等知识点
tags:
    - centos6.6
categories:
    - linux
---

## 安装系统

### 创建实例
首先电脑先安装VirtualBox软件, 这里就不记录那么详细...

打开软件, 如图,并点击`new`按钮新建一个实例 (下面都是一些截图, 可能加载比较慢, 耐心等待)

![](http://qiniu.maoyupeng.club/15535158498924.jpg)

依次填好 `name`,`type(系统类型)` 和 `version(对应的版本)`, 因为是演示安装 Centos6.6, 所以选择如下图:

![](http://qiniu.maoyupeng.club/15535162452911.jpg)

选择内存和空间(基本一路next...直到创建成功)

![](http://qiniu.maoyupeng.club/15535162452911.jpg)
![](http://qiniu.maoyupeng.club/15535165415134.jpg)
![](http://qiniu.maoyupeng.club/15535165621763.jpg)
![](http://qiniu.maoyupeng.club/15535165759996.jpg)
![](http://qiniu.maoyupeng.club/15535165931790.jpg)
![](http://qiniu.maoyupeng.club/15535166127193.jpg)
![](http://qiniu.maoyupeng.club/15535166559413.jpg)

### 安装镜像(iso)

`Start`实例, 会弹出一个询问窗口, 然后选择对应的镜像文件, 前提是镜像文件需要提前下载到电脑硬盘中

![](http://qiniu.maoyupeng.club/15535170264417.jpg)

选择第二项, 会有一个警告, 使用tab切换到 `Skip` 跳过选项, 回车往下执行
![](http://qiniu.maoyupeng.club/15535172811722.jpg)

![](http://qiniu.maoyupeng.club/15535173676951.jpg)

![](http://qiniu.maoyupeng.club/ScreenFlow.2019-03-25%2021_36_16.gif)

## 配置静态Ip

启动虚拟机, 并登陆系统后, 输入命令 `ifconfig`查看ip信息, 如下图:

![](http://qiniu.maoyupeng.club/15535212588330.jpg)

上图标识, 并没有自动分配静态ip, 所以需要如下配置, 才能获取到静态Ip

```bash
# 输入以下命令, 并编辑文件
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
![](http://qiniu.maoyupeng.club/15535214706837.jpg)

修改成yes, 并重启network, 再次查看`ifconfig`, 就可以看到静态ip了

```bash
# 重启network
service network restart
```

## 安装JDK8

---
title: MacOS M1 快速搭建Java开发环境
tags:
  - MacOS
  - Java
categories:
  - macbook
abbrlink: b5436530
date: 2022-06-16 11:10:04
---

> 前言：本人从事后端Java开发，和偶尔前端开发工作。

![](macbook.png)

最近入手了2021款的Macbook M1 Max型号的笔记本电脑，由于M1芯片是基于ARM架构研发的，所以平时都是使用x86架构的芯片，上手会有那么一点不适应。`（怎么JDK没有ARM版本？怎么Docker启动的容器会有警告或直接启动失败？）`
    
因此通过此文章，记录下我的环境搭建过程。    

<!-- more -->

## JDK安装

通过 [Zulu官方网站](https://www.azul.com/downloads/?version=java-8-lts&os=macos&architecture=arm-64-bit&package=jdk) 生成您需要的JDK版本，并且下载`.dmg`安装文件，直接双击安装即可。Zulu是基于OpenJDK构建的，请放心使用，不会有版权问题。

![](zulu-jdk.png)

安装成功后，可以通过命令`java -version`检查是否安装成功，如输出类似下图信息，即表示安装成功。

![](check-jdk-version.png)

## Docker Compose 搭建开发环境

我比较常用的开发环境分别有`Mysql`、`Redis`和`Nacos`。所以我整理了一个Docker Compose文件，通过docker帮我完成并就绪开发环境。

持续更新 todo...

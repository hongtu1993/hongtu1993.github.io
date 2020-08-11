---
title: gitHub bind domain name
author: 毛宇鹏
date: 2020-08-11 14:12:32
subtitle:
showTitle: Github绑定自己的域名
description: 如何在github中绑定自己的域名
tags:
    - domain
categories:
---

需要在github中绑定自定义域名主要有三个步骤，创建名为`xxx.github.io`的资源库，在工程目录配置CNAME文件，以及域名解析

## 创建资源库

怎么创建资源库这里就不详细说了，说白了也就是创建一个名为 `xxx.github.io`的仓库

## 配置CNAME文件

在工程根目录下，创建名为 `CNAME`的文件,并添加上你的域名，示例如下：

```text
www.maoyupeng.club
```

## 域名解析

| 记录类型 | 主机记录 | 记录值 |
|-------|------|------|
| CNAME | @ | 192.30.252.153 或 192.30.252.154 |
| www | CNAME | xxx.github.io |

请注意替换您的仓库前缀名称，示例 `hongtu1993.github.io`



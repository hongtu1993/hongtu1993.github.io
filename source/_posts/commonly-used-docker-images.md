---
title: commonly used docker images
author: 毛宇鹏
date: 2020-08-12 12:12:40
subtitle:
showTitle: 常用Docker镜像
description: 列举出作者常用的docker镜像，以及镜像安装配置和使用方法
tags:
    - docker
    - dockerfile
categories:
    - docker
---

## mysql5.7

### docker-compose方式

文件夹目录

```
根目录
    |__ msyql-compose.yml   docker-compose 文件
    |__ conf                mysql的配置文件
    |__ data                mysql的数据目录
    |__ logs                mysql的日志文件
```

#### mysql-compose.yml
```bash
version: '3.4'
services:
  db:
    image: mysql:5.7
    container_name: mysql
    ports:
      # 访问宿主机的33060端口，即可访问到容器的3306端口
      - "33060:3306"
    restart: always
    environment:
      # root用户默认密码，请自行修改  
      - MYSQL_ROOT_PASSWORD=mao
    volumes:
      - ./conf/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf
      - ./data:/usr/local/mysql/data
      - ./logs/:/usr/local/mysql/logs
```

#### mysqld.cnf配置文件

在conf目录下添加文件名为 `mysqld.cnf` 的配置文件，内容参考以下：
 
```bash
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
#log-error      = /var/log/mysql/error.log
# By default we only accept connections from localhost
#bind-address   = 127.0.0.1
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

max_allowed_packet=40M
innodb_log_file_size=256M
```

#### 参考命令

* 启动：`docker-compose -f mysql-compose.yml up -d`
* 停止：`docker-compose -f mysql-compose.yml stop`



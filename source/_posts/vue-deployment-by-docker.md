---
title: Vue deployment by docker
author: 毛宇鹏
date: 2020-02-26 23:50:23
subtitle:
showTitle: Docker部署vue项目
description: 通过Dockerfile构建Vue项目的Docker镜像并发布到docker
tags:
    - docker
    - vue
    - dockerfile
categories:
    - docker
---


### 编写Dockerfile
在项目根目录新建名为`Dockerfile`的文件, 并添加以下代码:
```bash
# build stage
# 拉取最小体积的node环境容器, 并安装cnpm (加快容器构建速度,npm比较慢)
FROM node:lts-alpine as build-stage
RUN npm install -g cnpm --registry=https://registry.npm.taobao.org

# 进入容器的app目录, 然后拷贝当前目录(根目录)的所有文件到容器的当前目录中(/app)
WORKDIR /app
COPY . .

# 删除vue环境配置文件(主要想通过容器的环境变量来达到不同的环境切换,以及为了部署到阿里云的容器服务或华为云的容器服务时, 通过配置项来配置相关的环境变量, 如果不需要可自行删除以下这句代码)
RUN rm -f .env.*

ENV VUE_APP_TEST_VALUE="My test Value"

#在容器内build
RUN cnpm run build


# production stage
# 最后通过nginx部署build出来的文件(/dist)
FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

```

### 创建镜像

编写好`Dockerfile`后, 则可通过docker命令创建一个docker镜像, 以下为参考指令:

```bash
docker build --no-cache -t vue-docker:1.0 .
```

**启动容器**

```bash
docker run -p 80:80 --name vue-docker1.0 vue-docker:1.0 
```

附上demo地址:
[https://gitee.com/mao-share/vue-docker.git](https://gitee.com/mao-share/vue-docker.git)



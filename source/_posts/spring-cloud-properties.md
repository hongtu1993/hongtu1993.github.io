---
title: spring cloud properties
subtitle:
showTitle: SpringCloud生产配置
description: SpringCloud生产配置调优
author: 毛宇鹏
date: 2018-12-10 12:11:47
tags:
    - spring cloud
    - properties
    - yml
categories:
    - spring
---

## Eureka Server通用配置项

```yml
#eureka server刷新readCacheMap的时间，注意，client读取的是readCacheMap，这个时间决定了多久会把readWriteCacheMap的缓存更新到readCacheMap上
#默认30s
eureka.server.responseCacheUpdateIntervalMs=3000

#eureka server缓存readWriteCacheMap失效时间，这个只有在这个时间过去后缓存才会失效，失效前不会更新，过期后从registry重新读取注册服务信息，registry是一个ConcurrentHashMap。
#由于启用了evict其实就用不太上改这个配置了
#默认180s
eureka.server.responseCacheAutoExpirationInSeconds=180

#启用主动失效，并且每次主动失效检测间隔为3s
#默认60s
eureka.server.eviction-interval-timer-in-ms=3000

#服务过期时间配置,超过这个时间没有接收到心跳EurekaServer就会将这个实例剔除
#注意，EurekaServer一定要设置eureka.server.eviction-interval-timer-in-ms否则这个配置无效，这个配置一般为服务刷新时间配置的三倍
#默认90s
eureka.instance.lease-expiration-duration-in-seconds=15
#服务刷新时间配置，每隔这个时间会主动心跳一次
#默认30s
eureka.instance.lease-renewal-interval-in-seconds=5
#eureka client刷新本地缓存时间
#默认30s
eureka.client.registryFetchIntervalSeconds=5
#eureka客户端ribbon刷新时间
#默认30s
ribbon.ServerListRefreshInterval=1000
eureka.instance.preferIpAddress=true
#关闭自我保护
eureka.server.enable-self-preservation=false
eureka.client.serviceUrl.defaultZone=http://192.168.1.10:8100/eureka/

# 参考原文: https://blog.csdn.net/zhxdick/article/details/79153711

```

## Eureka Client通用配置项

```yml
#服务过期时间配置,超过这个时间没有接收到心跳EurekaServer就会将这个实例剔除
#注意，EurekaServer一定要设置eureka.server.eviction-interval-timer-in-ms否则这个配置无效，这个配置一般为服务刷新时间配置的三倍
#默认90s
eureka.instance.lease-expiration-duration-in-seconds=15
#服务刷新时间配置，每隔这个时间会主动心跳一次
#默认30s
eureka.instance.lease-renewal-interval-in-seconds=5
#eureka client刷新本地缓存时间
#默认30s
eureka.client.registryFetchIntervalSeconds=5
#eureka客户端ribbon刷新时间
#默认30s
ribbon.ServerListRefreshInterval=1000
eureka.instance.preferIpAddress=true
#关闭自我保护
eureka.server.enable-self-preservation=false
#最好每个实例不同顺序，按照离自己最近的Eureka地址放到最前面
eureka.client.serviceUrl.defaultZone=http://192.168.1.10:8100/eureka/
```

## 解决Spring Cloud第一次调用失败

> 原因: Hystrix默认的超时时间是1秒, 如果1秒未响应, 将会执行fallback代码. 并且首次加载都是比较慢的, 初始化完成时间远大于1秒

**解决方法**

在zuul配置文件里禁用超时时间,或把超时时间设长一点;

```yml
hystrix:
  command:
    default:
      execution:
        timeout:
          enabled: false #禁用超时
```

```yml
hystrix:
  command:
    default:
      execution:
        isolation:
            thread:
                # 设置超时时间为8秒后
                timeoutInMilliseconds: 8000
        timeout:
          enabled: true
```


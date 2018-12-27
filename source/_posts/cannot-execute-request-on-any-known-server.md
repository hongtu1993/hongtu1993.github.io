---
title: cannot execute request on any known server
author: 毛宇鹏
date: 2018-12-27 09:34:40
subtitle:
showTitle: Eureka2.x配置连接密码报错
description: 使用了新版的Eureka之后, 发现配置服务密码的方式有所改变了, 而且Security默认开启了csrf拦截,导致服务注册不上来. 遇到这些问题该怎么办呢?
tags:
    - spring cloud
    - yml
categories:
    - spring
---


# 添加依赖包

```
<!--加入服务认证(密码),需要引入security-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

# 配置文件 `application.yml`
## 2.0版本配置方法(注意:与旧版配置不同)
```yml
server:
  port: 8100
eureka:
  instance:
    hostname: localhost
  client:
    # 由于该应用为注册中心,所以设置为false,代表不向注册中心注册自己
    register-with-eureka: false
    # 由于注册中心的职责就是维护服务示例,它并不需要去检索服务,所以也设置为false
    fetch-registry: false
    serviceUrl:
      defaultZone: http://name:pwd@${eureka.instance.hostname}:${server.port}/eureka/
spring:
  security:
    user:
      name: name
      password: pwd
```


## 测试

启动并访问http://localhost:8100 ,可以看到登录界面, 说明用户密码已经生效了

![image.png](http://qiniu.maoyupeng.club/15458735160123.jpg)


`接着启动服务注册到注册中心,此时发现启动时抛出异常:Cannot execute request on any known server`

![image.png](http://qiniu.maoyupeng.club/15458736992721.jpg)

原因是因为新版本的security默认开启了csrf拦截, 所以需要禁用csrf功能. 在启动类中加入以下代码:

```java
package cn.com.szzt.cloud.register;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;
import org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

/**
 * @author 毛宇鹏
 */
@EnableEurekaServer
@SpringBootApplication(exclude={
        DataSourceAutoConfiguration.class,
        HibernateJpaAutoConfiguration.class
})
public class RegisterApplication {

    public static void main(String[] args) {
        SpringApplication.run(RegisterApplication.class, args);
    }

    /**
     * 2.1版本的security默认加上了 csrf 拦截, 所以需要通过重写方法, 把csrf拦截禁用
     * 参考: https://github.com/yinjihuan/spring-cloud/issues/1
     * <pre>
     *     This is because @EnableWebSecurity is now added by default when Spring Security is on the classpath.
     *     This enable CSRF protection by default. You will have the same problem in 1.5.10 if you add @EnableWebSecurity.
     *     One work around, which is not the most secure workaround if you have browsers using the Eureka dashboard, is to disable CSRF protection.
     *     This can be done by adding the following configurations to your app.
     * </pre>
     */
    @EnableWebSecurity
    static class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http.csrf().disable();
            super.configure(http);
        }
    }
}
```
问题解决!!

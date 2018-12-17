---
title: Spring boot reference guide
author: 毛宇鹏
date: 2018-12-13 14:09:54
subtitle:
showTitle: Springboot1.3.0参考指南
description: 本节提供一个Spring Boot参考文档的简明概述。你可以把它作为文档其余部分的导航。你可以从头到尾依次阅读该参考指南，或跳过你不感兴趣的章节。
tags:
categories:
---

## 介绍

转载自:[https://www.gitbook.com/book/qbgbook/spring-boot-reference-guide-zh/details](https://www.gitbook.com/book/qbgbook/spring-boot-reference-guide-zh/details)

### 1.Spring Boot文档
本节提供一个Spring Boot参考文档的简明概述。你可以把它作为文档其余部分的导航。你可以从头到尾依次阅读该参考指南，或跳过你不感兴趣的章节。

#### 1.1关于本文档

Spring Boot参考指南有[html](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/reference/html)，[pdf](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/reference/pdf/spring-boot-reference.pdf)和[epub](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/reference/epub/spring-boot-reference.epub)形式的文档。在[docs.spring.io/spring-boot/docs/current/reference](http://docs.spring.io/spring-boot/docs/current/reference)可获取到最新的副本。

在对副本不收取任何费用，并且不管是打印还是电子版每个副本都包含版权声明的情况下，你可以自己使用本文档副本，也可以分发给其他人。

### 开始
如果你想从总体上对Spring Boot或Spring入门，本章节就是为你准备的！在这里，我们将回答基本的"what?"，"how?"和"why?"问题。你会发现一个温雅的Spring Boot介绍及安装指南。然后我们构建第一个Spring Boot应用，并讨论一些我们需要遵循的核心原则。

#### 2.1 Spring Boot介绍
Spring Boot使开发独立的，产品级别的基于Spring的应用变得非常简单，你只需"just run"。 我们为Spring平台及第三方库提供开箱即用的设置，这样你就可以有条不紊地开始。多数Spring Boot应用需要很少的Spring配置。

你可以使用Spring Boot创建Java应用，并使用java -jar启动它或采用传统的war部署方式。我们也提供了一个运行"spring脚本"的命令行工具。

我们主要的目标是：

* 为所有的Spring开发提供一个从根本上更快的和广泛使用的入门经验。
* 开箱即用，但你可以通过不采用默认设置来摆脱这种方式。
* 提供一系列大型项目常用的非功能性特征（比如，内嵌服务器，安全，指标，健康检测，外部化配置）。
* 绝对不需要代码生成及XML配置。

#### 2.2 系统要求
默认情况下，Spring Boot 1.3.0.BUILD-SNAPSHOT 需要Java7和Spring框架4.1.3或以上。你可以在Java6下使用Spring Boot，不过需要添加额外配置。具体参考[Section 73.9, “How to use Java 6”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/73.9.%20How%20to%20use%20Java%206.md) 。构建环境明确支持的有Maven（3.2+）和Gradle（1.12+）。

注：尽管你可以在Java6或Java7环境下使用Spring Boot，通常我们建议你如果可能的话就使用Java8。

##### 2.2.1 Servlet容器

下列内嵌容器支持开箱即用（out of the box）：

|名称|Servlet版本|Java版本|
| ------------- |:-------------:| -----:|
|Tomcat 8|	3.1	|Java 7+|
|Tomcat 7	|3.0|	Java 6+|
|Jetty 9	|3.1	|Java 7+|
|Jetty 8	|3.0	|Java 6+|
|Undertow 1.1	|3.1	|Java 7+|

你也可以将Spring Boot应用部署到任何兼容Servlet 3.0+的容器。

#### 2.3 Spring Boot安装
Spring Boot可以跟典型的Java开发工具一块使用或安装为一个命令行工具。不管怎样，你将需要安装[Java SDK v1.6](http://www.java.com/) 或更高版本。在开始之前，你需要检查下当前安装的Java版本：

	$ java -version

如果你是一个Java新手，或你只是想体验一下Spring Boot，你可能想先尝试[Spring Boot CLI](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/II.%20Getting%20started/10.2.%20Installing%20the%20Spring%20Boot%20CLI.md)，否则继续阅读经典地安装指南。

注：尽管Spring Boot兼容Java 1.6，如果可能的话，你应该考虑使用Java最新版本。

##### 2.3.1 为Java开发者准备的安装指南
你可以像使用其他任何标准Java库那样使用Spring Boot，只需简单地在你的classpath下包含正确的spring-boot-*.jar文件。Spring Boot不需要集成任何特殊的工具，所以你可以使用任何IDE或文本编辑器；Spring Boot应用也没有什么特殊之处，所以你可以像任何其他Java程序那样运行和调试。

尽管你可以拷贝Spring Boot jars，不过，我们通常推荐你使用一个支持依赖管理的构建工具（比如Maven或Gradle）。

###### 2.3.1.1 Maven安装
Spring Boot兼容Apache Maven 3.2或更高版本。如果没有安装Maven，你可以参考[maven.apache.org](http://maven.apache.org/)指南。

注：在很多操作系统上，你可以通过一个包管理器安装Maven。如果你是一个OSX Homebrew用户，可以尝试brew install maven。Ubuntu用户可以运行sudo apt-get install maven。

Spring Boot依赖的groupId为org.springframework.boot。通常你的Maven POM文件需要继承spring-boot-starter-parent，然后声明一个或多个[“Starter POMs”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/III.%20Using%20Spring%20Boot/13.4.%20Starter%20POMs.md)依赖。Spring Boot也提供了一个用于创建可执行jars的[Maven](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/VIII.%20Build%20tool%20plugins/58.%20Spring%20Boot%20Maven%20plugin.md)插件。

下面是一个典型的pom.xml文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!-- Inherit defaults from Spring Boot -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.3.0.BUILD-SNAPSHOT</version>
    </parent>

    <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <!-- Package as an executable jar -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <!-- Add Spring repositories -->
    <!-- (you don't need this if you are using a .RELEASE version) -->
    <repositories>
        <repository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots><enabled>true</enabled></snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
        </pluginRepository>
        <pluginRepository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </pluginRepository>
    </pluginRepositories>
</project>
```

注：`spring-boot-starter-parent`是使用Spring Boot的一个不错的方式，但它不总是合适的。有时你需要继承一个不同的parent POM，或者你可能只是不喜欢我们的默认配置。查看[Section 13.1.2, “Using Spring Boot without the parent POM”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/III.%20Using%20Spring%20Boot/13.1.2.%20Using%20Spring%20Boot%20without%20the%20parent%20POM.md)获取使用import的替代解决方案。

###### 2.3.1.2 Gradle安装
Spring Boot兼容Gradle 1.12或更高版本。如果没有安装Gradle，你可以参考[www.gradle.org](http://www.gradle.org/)上的指南。

Spring Boot依赖可以使用org.springframework.boot group来声明。通常，你的项目将声明一个或多个[“Starter POMs”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/III.%20Using%20Spring%20Boot/13.4.%20Starter%20POMs.md)依赖。Spring Boot提供一个用于简化依赖声明和创建可执行jars的有用的[Gradle](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/VIII.%20Build%20tool%20plugins/59.%20Spring%20Boot%20Gradle%20plugin.md)插件。

注：当你需要构建一个项目时，Gradle Wrapper提供一个获取Gradle的漂亮方式。它是一个伴随你的代码一块提交的小脚本和库，用于启动构建进程。具体参考[Gradle Wrapper](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/II.%20Getting%20started/www.gradle.org/docs/current/userguide/gradle_wrapper.html)。

下面是一个典型的build.gradle文件：

	buildscript {
    repositories {
        jcenter()
        maven { url "http://repo.spring.io/snapshot" }
        maven { url "http://repo.spring.io/milestone" }
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.0.BUILD-SNAPSHOT")
    }
	}

	apply plugin: 'java'
	apply plugin: 'spring-boot'

	jar {
	    baseName = 'myproject'
	    version =  '0.0.1-SNAPSHOT'
	}

	repositories {
	    jcenter()
	    maven { url "http://repo.spring.io/snapshot" }
	    maven { url "http://repo.spring.io/milestone" }
	}

	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web")
	    testCompile("org.springframework.boot:spring-boot-starter-test")
	}

##### 2.3.2 Spring Boot CLI安装
Spring Boot是一个命令行工具，用于使用Spring进行快速原型搭建。它允许你运行[Groovy](http://groovy.codehaus.org/)脚本，这意味着你可以使用类Java的语法，并且没有那么多的模板代码。

你没有必要为了使用Spring Boot而去用CLI，但它绝对是助力Spring应用的最快方式。

###### 2.3.2.1 手动安装
你可以从Spring软件仓库下载Spring CLI分发包：

[spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.zip](http://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/1.3.0.BUILD-SNAPSHOT/spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.zip)
[spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.tar.gz](http://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/1.3.0.BUILD-SNAPSHOT/spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.tar.gz)
不稳定的[snapshot](http://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/)分发包也能获取到。

下载完成后，遵循解压后的存档里的[INSTALL.txt](http://raw.github.com/spring-projects/spring-boot/master/spring-boot-cli/src/main/content/INSTALL.txt)操作指南进行安装。一般而言，在.zip文件的bin/目录下存在一个spring脚本（Windows下是spring.bat），或者使用java -jar来运行一个.jar文件（该脚本会帮你确定classpath被正确设置）。

###### 2.3.2.2 使用GVM安装
GVM（Groovy环境管理器）可以用来管理多种不同版本的Groovy和Java二进制包，包括Groovy自身和Spring Boot CLI。可以从gvmtool.net获取gvm，并使用以下命令安装Spring Boot：

	$ gvm install springboot
	$ spring --version
	Spring Boot v1.3.0.BUILD-SNAPSHOT

如果你正在为CLI开发新的特性，并想轻松获取你刚构建的版本，可以使用以下命令：

	$ gvm install springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin/spring-1.3.0.BUILD-SNAPSHOT/
	$ gvm use springboot dev
	$ spring --version
	Spring CLI v1.3.0.BUILD-SNAPSHOT

这将会在你的gvm仓库中安装一个名叫dev的本地spring实例。它指向你的目标构建位置，所以每次你重新构建Spring Boot，spring将会是最新的。

你可以通过以下命令来验证：

	$ gvm ls springboot

	================================================================================
	Available Springboot Versions
	================================================================================
	> + dev
	* 1.3.0.BUILD-SNAPSHOT

	================================================================================
	+ - local version
	* - installed
	> - currently in use
	================================================================================

###### 2.3.2.3 使用OSX Homebrew进行安装
如果你的环境是Mac，并使用[Homebrew](http://brew.sh/)，想要安装Spring Boot CLI只需如下操作：

	$ brew tap pivotal/tap
	$ brew install springboot

Homebrew将把spring安装到/usr/local/bin下。

注：如果该方案不可用，可能是因为你的brew版本太老了。你只需执行brew update并重试即可。

###### 2.3.2.4 使用MacPorts进行安装
如果你的环境是Mac，并使用[MacPorts](http://www.macports.org/)，想要安装Spring Boot CLI只需如下操作：

	$ sudo port install spring-boot-cli

###### 2.3.2.5 命令行实现
Spring Boot CLI启动脚本为[BASH](http://en.wikipedia.org/wiki/Bash_%28Unix_shell%29)和[zsh](http://en.wikipedia.org/wiki/Zsh) shells提供完整的命令行实现。你可以在任何shell中source脚本（名称也是spring），或将它放到你个人或系统范围的bash实现初始化中。在一个Debian系统里，系统范围的脚本位于/shell-completion/bash下，当一个新的shell启动时该目录下的所有脚本都被执行。想要手动运行该脚本，例如，你已经使用GVM进行安装了：

	$ . ~/.gvm/springboot/current/shell-completion/bash/spring
	$ spring
	  grab  help  jar  run  test  version

注：如果你使用Homebrew或MacPorts安装Spring Boot CLI，命令行实现脚本会自动注册到你的shell。

###### 2.3.2.6 Spring CLI示例快速入门
下面是一个相当简单的web应用，你可以用它测试你的安装是否成功。创建一个名叫app.groovy的文件：

```java
@RestController
class ThisWillActuallyRun {

    @RequestMapping("/")
    String home() {
        "Hello World!"
    }

}
```
然后简单地从一个shell中运行它：

	$ spring run app.groovy

注：当你首次运行该应用时将会花费一点时间，因为需要下载依赖。后续运行将会快很多。

在你最喜欢的浏览器中打开localhost:8080，然后你应该看到以下输出：

	Hello World!


##### 2.3.3 从Spring Boot早期版本升级
如果你正在升级一个Spring Boot早期版本，查看下放在[project wiki](http://github.com/spring-projects/spring-boot/wiki)上的"release notes"。你会发现每次发布的更新指南和一个"new and noteworthy"特性列表。

想要升级一个已安装的CLI，你需要使用合适的包管理命令（例如，brew upgrade），或如果你是手动安装CLI，按照[standard instructions](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/II.%20Getting%20started/10.2.1.%20Manual%20installation.md)操作并记得更新你的PATH环境变量以移除任何老的引用。

##### 2.3.4 开发你的第一个Spring Boot应用
让我们使用Java开发一个简单的"Hello World!" web应用，来强调下Spring Boot的一些关键特性。我们将使用Maven构建该项目，因为大多数IDEs都支持它。

注：[spring.io](http://spring.io/)网站包含很多使用Spring Boot的"入门"指南。如果你正在找特定问题的解决方案，可以先去那瞅瞅。

在开始前，你需要打开一个终端，检查是否安装可用的Java版本和Maven：

	$ java -version
	java version "1.7.0_51"
	Java(TM) SE Runtime Environment (build 1.7.0_51-b13)
	Java HotSpot(TM) 64-Bit Server VM (build 24.51-b03, mixed mode)


	$ mvn -v
	Apache Maven 3.2.3 (33f8c3e1027c3ddde99d3cdebad2656a31e8fdf4; 2014-08-11T13:58:10-07:00)
	Maven home: /Users/user/tools/apache-maven-3.1.1
	Java version: 1.7.0_51, vendor: Oracle Corporation

注：该示例需要创建自己的文件夹。后续的操作假设你已创建一个合适的文件夹，并且它是你的“当前目录”。

##### 2.3.5 创建POM
我们需要以创建一个Maven pom.xml文件作为开始。该pom.xml是用来构建项目的处方。打开你最喜欢的文本编辑器，然后添加以下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.3.0.BUILD-SNAPSHOT</version>
    </parent>

    <!-- Additional lines to be added here... -->

    <!-- (you don't need this if you are using a .RELEASE version) -->
    <repositories>
        <repository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots><enabled>true</enabled></snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
        </pluginRepository>
        <pluginRepository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </pluginRepository>
    </pluginRepositories>
</project>
```

这会给你一个可运转的构建，你可以通过运行mvn package测试它（现在你可以忽略"jar将是空的-没有包含任何内容！"的警告）。

注：目前你可以将该项目导入一个IDE（大多数现代的Java IDE都包含对Maven的内建支持）。简单起见，我们将继续使用普通的文本编辑器完成该示例。

##### 2.3.6 添加classpath依赖
Spring Boot提供很多"Starter POMs"，这能够让你轻松的将jars添加到你的classpath下。我们的示例程序已经在POM的partent节点使用了spring-boot-starter-parent。spring-boot-starter-parent是一个特殊的starter，它提供了有用的Maven默认设置。同时，它也提供了一个dependency-management节点，这样对于”blessed“依赖你可以省略version标记。

其他的”Starter POMs“简单的提供依赖，这些依赖可能是你开发特定类型的应用时需要的。由于正在开发一个web应用，我们将添加一个spring-boot-starter-web依赖-但在此之前，让我们看下目前所拥有的：

	$ mvn dependency:tree
	[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT

`mvn dependency:tree`命令以树形表示来打印你的项目依赖。你可以看到`spring-boot-starter-parent`本身并没有提供依赖。编辑我们的pom.xml，并在parent节点下添加`spring-boot-starter-web`依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

如果再次运行`mvn dependency:tree`，你将看到现在有了一些其他依赖，包括Tomcat web服务器和Spring Boot自身。

##### 2.3.7 编写代码
为了完成应用程序，我们需要创建一个单独的Java文件。Maven默认会编译`src/main/java`下的源码，所以你需要创建那样的文件结构，然后添加一个名为`src/main/java/Example.java`的文件：

```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.stereotype.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(Example.class, args);
    }

}
```

尽管这里没有太多代码，但很多事情正在发生。让我们分步探讨重要的部分。

###### 2.3.7.1 @RestController和@RequestMapping注解
我们的Example类上使用的第一个注解是@RestController。这被称为一个构造型（stereotype）注解。它为阅读代码的人们提供建议。对于Spring，该类扮演了一个特殊角色。在本示例中，我们的类是一个web @Controller，所以当处理进来的web请求时，Spring会询问它。

@RequestMapping注解提供路由信息。它告诉Spring任何来自"/"路径的HTTP请求都应该被映射到home方法。@RestController注解告诉Spring以字符串的形式渲染结果，并直接返回给调用者。

注：@RestController和@RequestMapping注解是Spring MVC注解（它们不是Spring Boot的特定部分）。具体查看Spring参考文档的[MVC](http://docs.spring.io/spring/docs/4.1.5.RELEASE/spring-framework-reference/htmlsingle#mvc)章节。

###### 2.3.7.2 @EnableAutoConfiguration注解
第二个类级别的注解是@EnableAutoConfiguration。这个注解告诉Spring Boot根据添加的jar依赖猜测你想如何配置Spring。由于spring-boot-starter-web添加了Tomcat和Spring MVC，所以auto-configuration将假定你正在开发一个web应用并相应地对Spring进行设置。

**Starter POMs和Auto-Configuration**：设计auto-configuration的目的是更好的使用"Starter POMs"，但这两个概念没有直接的联系。你可以自由地挑选starter POMs以外的jar依赖，并且Spring Boot将仍旧尽最大努力去自动配置你的应用。

###### 2.3.7.3 main方法
我们的应用程序最后部分是main方法。这只是一个标准的方法，它遵循Java对于一个应用程序入口点的约定。我们的main方法通过调用run，将业务委托给了Spring Boot的SpringApplication类。SpringApplication将引导我们的应用，启动Spring，相应地启动被自动配置的Tomcat web服务器。我们需要将`Example.class`作为参数传递给run方法来告诉SpringApplication谁是主要的Spring组件。为了暴露任何的命令行参数，args数组也会被传递过去。

##### 2.3.8 运行示例
到此我们的应用应该可以工作了。由于使用了`spring-boot-starter-parent` POM，这样我们就有了一个非常有用的run目标，我们可以用它启动程序。在项目根目录下输入`mvn spring-boot:run`来启动应用：

	$ mvn spring-boot:run

	  .   ____          _            __ _ _
	 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
	( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
	 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
	  '  |____| .__|_| |_|_| |_\__, | / / / /
	 =========|_|==============|___/=/_/_/_/
	 :: Spring Boot ::  (v1.3.0.BUILD-SNAPSHOT)
	....... . . .
	....... . . . (log output here)
	....... . . .
	........ Started Example in 2.222 seconds (JVM running for 6.514)

如果使用一个浏览器打开`localhost:8080`，你应该可以看到以下输出：

	Hello World!

点击`ctrl-c`温雅地关闭应用程序。

##### 2.3.9 创建一个可执行jar
让我们通过创建一个完全自包含的可执行jar文件来结束我们的示例，该jar文件可以在生产环境运行。可执行jars（有时候被成为胖jars "fat jars"）是包含你的编译后的类和你的代码运行所需的依赖jar的存档。

**可执行jars和Java**：Java没有提供任何标准的加载内嵌jar文件（即jar文件中还包含jar文件）的方法。如果你想发布一个自包含的应用这就是一个问题。为了解决该问题，很多开发者采用"共享的"jars。一个共享的jar简单地将来自所有jars的类打包进一个单独的“超级jar”。采用共享jar方式的问题是很难区分在你的应用程序中可以使用哪些库。在多个jars中如果存在相同的文件名（但内容不一样）也会是一个问题。Spring Boot采取一个不同的途径，并允许你真正的内嵌jars。

为了创建可执行的jar，需要将spring-boot-maven-plugin添加到我们的pom.xml中。在dependencies节点下插入以下内容：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

注：`spring-boot-starter-paren `POM包含用于绑定repackage目标的<executions>配置。如果你不使用parent POM，你将需要自己声明该配置。具体参考插件文档。

保存你的pom.xml，然后从命令行运行`mvn package`：

	$ mvn package

	[INFO] Scanning for projects...
	[INFO]
	[INFO] ------------------------------------------------------------------------
	[INFO] Building myproject 0.0.1-SNAPSHOT
	[INFO] ------------------------------------------------------------------------
	[INFO] .... ..
	[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
	[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
	[INFO]
	[INFO] --- spring-boot-maven-plugin:1.3.0.BUILD-SNAPSHOT:repackage (default) @ myproject ---
	[INFO] ------------------------------------------------------------------------
	[INFO] BUILD SUCCESS
	[INFO] ------------------------------------------------------------------------

如果查看target目录，你应该看到myproject-0.0.1-SNAPSHOT.jar。该文件应该有10Mb左右的大小。如果想偷看内部结构，你可以运行`jar tvf`：

	$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar

在target目录下，你应该也能看到一个很小的名为myproject-0.0.1-SNAPSHOT.jar.original的文件。这是在Spring Boot重新打包前Maven创建的原始jar文件。

为了运行该应用程序，你可以使用`java -jar`命令：

	$ java -jar target/myproject-0.0.1-SNAPSHOT.jar
	 .   ____          _            __ _ _
	 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
	( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
	 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
	  '  |____| .__|_| |_|_| |_\__, | / / / /
	 =========|_|==============|___/=/_/_/_/
	 :: Spring Boot ::  (v1.3.0.BUILD-SNAPSHOT)
	....... . . .
	....... . . . (log output here)
	....... . . .
	........ Started Example in 2.536 seconds (JVM running for 2.864)

和以前一样，点击ctrl-c来温柔地退出程序。

### 使用Spring Boot
本章节将会详细介绍如何使用Spring Boot。它覆盖了构建系统，自动配置和运行/部署选项等主题。我们也覆盖了一些Spring Boot最佳实践。尽管Spring Boot没有什么特别的（只是一个你能消费的库），但仍有一些建议，如果你遵循的话将会让你的开发进程更容易。

如果你刚接触Spring Boot，那最好先读下上一章节的[Getting Started](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/II.%20Getting%20started/README.md)指南。

#### 3.1 构建系统
强烈建议你选择一个支持依赖管理，能消费发布到Maven中央仓库的artifacts的构建系统。我们推荐你选择Maven或Gradle。选择其他构建系统来使用Spring Boot也是可能的（比如Ant），但它们不会被很好的支持。

##### 3.1.1 Maven
Maven用户可以继承spring-boot-starter-parent项目来获取合适的默认设置。该父项目提供以下特性：

* 默认编译级别为Java 1.6
* 源码编码为UTF-8
* 一个依赖管理节点，允许你省略普通依赖的<version>标签，继承自spring-boot-dependencies POM。
* 合适的[资源过滤](https://maven.apache.org/plugins/maven-resources-plugin/examples/filter.html)
* 合适的插件配置（[exec插件](http://mojo.codehaus.org/exec-maven-plugin/)，[surefire](http://maven.apache.org/surefire/maven-surefire-plugin/)，[Git commit ID](https://github.com/ktoso/maven-git-commit-id-plugin)，[shade](http://maven.apache.org/plugins/maven-shade-plugin/)）
* 针对application.properties和application.yml的资源过滤

最后一点：由于默认配置文件接收Spring风格的占位符（`${...}`），Maven filtering改用`@..@`占位符（你可以使用Maven属性`resource.delimiter`来覆盖它）。

###### 3.1.1.1 继承starter parent
想配置你的项目继承`spring-boot-starter-parent`只需要简单地设置`parent`为：

```xml
<!-- Inherit defaults from Spring Boot -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.3.0.BUILD-SNAPSHOT</version>
</parent>
```
注：你应该只需要在该依赖上指定Spring Boot版本。如果导入其他的starters，你可以放心的省略版本号。

###### 3.1.1.2 使用没有父POM的Spring Boot

不是每个人都喜欢继承`spring-boot-starter-parent` POM。你可能需要使用公司标准parent，或你可能倾向于显式声明所有Maven配置。

如果你不使用`spring-boot-starter-parent`，通过使用一个`scope=import`的依赖，你仍能获取到依赖管理的好处：

```xml
<dependencyManagement>
     <dependencies>
        <dependency>
            <!-- Import dependency management from Spring Boot -->
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>1.3.0.BUILD-SNAPSHOT</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

###### 3.1.1.3 改变java版本
`spring-boot-starter-parent`选择相当保守的Java兼容策略。如果你遵循我们的建议，使用最新的Java版本，你可以添加一个`java.version`属性：

```xml
<properties>
    <java.version>1.8</java.version>
</properties>
```

###### 3.1.1.4 使用Spring Boot Maven插件
Spring Boot包含一个[Maven插件](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/VIII.%20Build%20tool%20plugins/58.%20Spring%20Boot%20Maven%20plugin.md)，它可以将项目打包成一个可执行jar。如果想使用它，你可以将该插件添加到<plugins>节点处：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```
注：如果使用Spring Boot starter parent pom，你只需要添加该插件而无需配置它，除非你想改变定义在partent中的设置。

##### 3.1.2 Gradle
Gradle用户可以直接在它们的dependencies节点处导入”starter POMs“。跟Maven不同的是，这里没有用于导入共享配置的"超父"（super parent）。

	apply plugin: 'java'

	repositories { jcenter() }
	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web:1.3.0.BUILD-SNAPSHOT")
	}

[spring-boot-gradle-plugin](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/VIII.%20Build%20tool%20plugins/59.%20Spring%20Boot%20Gradle%20plugin.md)插件也是可以使用的，它提供创建可执行jar和从source运行项目的任务。它也添加了一个ResolutionStrategy用于让你省略常用依赖的版本号：

	buildscript {
    repositories { jcenter() }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.0.BUILD-SNAPSHOT")
    }
	}

	apply plugin: 'java'
	apply plugin: 'spring-boot'

	repositories { jcenter() }
	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web")
	    testCompile("org.springframework.boot:spring-boot-starter-test")
	}

##### 3.1.3 Ant
使用Apache Ant构建一个Spring Boot项目是完全可能的，然而，Spring Boot没有为它提供特殊的支持或插件。Ant脚本可以使用Ivy依赖管理系统来导入starter POMs。

查看[Section 73.8, “Build an executable archive with Ant”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/73.8.%20Build%20an%20executable%20archive%20with%20Ant.md)获取更多指导。

##### 3.1.4 Starter POMs
Starter POMs是可以包含到应用中的一个方便的依赖关系描述符集合。你可以获取所有Spring及相关技术的一站式服务，而不需要翻阅示例代码，拷贝粘贴大量的依赖描述符。例如，如果你想使用Spring和JPA进行数据库访问，只需要在你的项目中包含`spring-boot-starter-data-jpa`依赖，然后你就可以开始了。

该starters包含很多你搭建项目，快速运行所需的依赖，并提供一致的，管理的传递依赖集。

名字有什么含义：所有的starters遵循一个相似的命名模式：`spring-boot-starter-*`，在这里*是一种特殊类型的应用程序。该命名结构旨在帮你找到需要的starter。很多IDEs集成的Maven允许你通过名称搜索依赖。例如，使用相应的Eclipse或STS插件，你可以简单地在POM编辑器中点击ctrl-space，然后输入"`spring-boot-starter`"可以获取一个完整列表。

下面的应用程序starters是Spring Boot在`org.springframework.boot`组下提供的：

**Spring Boot application starters**



|名称									|	描述 |
|:--------------------------------------|:-----------------------------------------------------|
|spring-boot-starter						|核心Spring Boot starter，包括自动配置支持，日志和YAML |
|spring-boot-starter-actuator			|生产准备的特性，用于帮你监控和管理应用 |
|spring-boot-starter-amqp				|对"高级消息队列协议"的支持，通过spring-rabbit实现 |
|spring-boot-starter-aop					|对面向切面编程的支持，包括spring-aop和AspectJ |
|spring-boot-starter-batch				|对Spring Batch的支持，包括HSQLDB数据库 |
|spring-boot-starter-cloud-connectors	|对Spring Cloud Connectors的支持，简化在云平台下（例如，Cloud Foundry 和Heroku）服务的连接 |
|spring-boot-starter-data-elasticsearch	|对Elasticsearch搜索和分析引擎的支持，包括spring-data-elasticsearch |
|spring-boot-starter-data-gemfire		|对GemFire分布式数据存储的支持，包括spring-data-gemfire |
|spring-boot-starter-data-jpa			|对"Java持久化API"的支持，包括spring-data-jpa，spring-orm和Hibernate |
|spring-boot-starter-data-mongodb		|对MongoDB NOSQL数据库的支持，包括spring-data-mongodb |
|spring-boot-starter-data-rest			|对通过REST暴露Spring Data仓库的支持，通过spring-data-rest-webmvc实现 |
|spring-boot-starter-data-solr			|对Apache Solr搜索平台的支持，包括spring-data-solr |
|spring-boot-starter-freemarker			|对FreeMarker模板引擎的支持 |
|spring-boot-starter-groovy-templates	|对Groovy模板引擎的支持 |
|spring-boot-starter-hateoas				|对基于HATEOAS的RESTful服务的支持，通过spring-hateoas实现 |
|spring-boot-starter-hornetq				|对"Java消息服务API"的支持，通过HornetQ实现 |
|spring-boot-starter-integration			|对普通spring-integration模块的支持 |
|spring-boot-starter-jdbc				|对JDBC数据库的支持 |
|spring-boot-starter-jersey				|对Jersey RESTful Web服务框架的支持 |
|spring-boot-starter-jta-atomikos		|对JTA分布式事务的支持，通过Atomikos实现 |
|spring-boot-starter-jta-bitronix		|对JTA分布式事务的支持，通过Bitronix实现 |
|spring-boot-starter-mail				|对javax.mail的支持 |
|spring-boot-starter-mobile				|对spring-mobile的支持 |
|spring-boot-starter-mustache			|对Mustache模板引擎的支持 |
|spring-boot-starter-redis				|对REDIS键值数据存储的支持，包括spring-redis |
|spring-boot-starter-security			|对spring-security的支持 |
|spring-boot-starter-social-facebook	|	对spring-social-facebook的支持 |
|spring-boot-starter-social-linkedin	|	对spring-social-linkedin的支持 |
|spring-boot-starter-social-twitter		|对spring-social-twitter的支持 |
|spring-boot-starter-test				|对常用测试依赖的支持，包括JUnit, Hamcrest和Mockito，还有spring-test模块 |
|spring-boot-starter-thymeleaf			|对Thymeleaf模板引擎的支持，包括和Spring的集成 |
|spring-boot-starter-velocity			|对Velocity模板引擎的支持 |
|spring-boot-starter-web				|	对全栈web开发的支持，包括Tomcat和spring-webmvc |
|spring-boot-starter-websocket			|对WebSocket开发的支持 |
|spring-boot-starter-ws	对Spring 		|Web服务的支持 |

除了应用程序的starters，下面的starters可以用于添加[生产准备](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/V.%20Spring%20Boot%20Actuator/README.md)的特性。

**Spring Boot生产准备的starters**


|名称|	描述|
|:---|:--|
|spring-boot-starter-actuator|	添加生产准备特性，比如指标和监控|
|spring-boot-starter-remote-shell|	添加远程ssh shell支持|

最后，Spring Boot包含一些可用于排除或交换具体技术方面的starters。

**Spring Boot technical starters**

|名称|描述|
|:---|:--|
|spring-boot-starter-jetty		|导入Jetty HTTP引擎（作为Tomcat的替代）|
|spring-boot-starter-log4j		|对Log4J日志系统的支持|
|spring-boot-starter-logging		|导入Spring Boot的默认日志系统（Logback）|
|spring-boot-starter-tomcat		|导入Spring Boot的默认HTTP引擎（Tomcat）|
|spring-boot-starter-undertow	|导入Undertow HTTP引擎（作为Tomcat的替代）|

注：查看GitHub上位于`spring-boot-starters`模块内的[README](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-starters/README.adoc)文件，可以获取到一个社区贡献的其他starter POMs列表。


#### 3.2 组织你的代码
Spring Boot不需要使用任何特殊的代码结构，然而，这里有一些有用的最佳实践。

##### 3.2.1 使用"default"包
当类没有包含`package`声明时，它被认为处于`default package`下。通常不推荐使用`default package`，并应该避免使用它。因为对于使用`@ComponentScan`，`@EntityScan`或`@SpringBootApplication`注解的Spring Boot应用来说，来自每个jar的类都会被读取，这会造成一定的问题。

注：我们建议你遵循Java推荐的包命名规范，使用一个反转的域名（例如`com.example.project`）。

##### 3.2.2 定位main应用类
我们通常建议你将main应用类放在位于其他类上面的根包（root package）中。通常使用`@EnableAutoConfiguration`注解你的main类，并且暗地里为某些项定义了一个基础“`search package`”。例如，如果你正在编写一个JPA应用，被`EnableAutoConfiguration`注解的类所在包将被用来搜索`@Entity`项。

使用根包允许你使用`@ComponentScan`注解而不需要定义一个basePackage属性。如果main类位于根包中，你也可以使用`@SpringBootApplication`注解。

下面是一个典型的结构：

	com
	 +- example
	     +- myproject
	         +- Application.java
	         |
	         +- domain
	         |   +- Customer.java
	         |   +- CustomerRepository.java
	         |
	         +- service
	         |   +- CustomerService.java
	         |
	         +- web
	             +- CustomerController.java

`Application.java`文件将声明main方法，还有基本的`@Configuration`。

```java
package com.example.myproject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableAutoConfiguration
@ComponentScan
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

#### 3.3 配置类
Spring Boot提倡基于Java的配置。尽管你可以使用一个XML源来调用`SpringApplication.run()`，我们通常建议你使用`@Configuration`类作为主要源。一般定义main方法的类也是主要`@Configuration`的一个很好候选。

注：很多使用XML配置的Spring配置示例已经被发布到网络上。你应该总是尽可能的使用基于Java的配置。搜索查看`enable*`注解就是一个好的开端。

##### 3.3.1 导入其他配置类
你不需要将所有的`@Configuration`放进一个单独的类。`@Import`注解可以用来导入其他配置类。另外，你也可以使用`@ComponentScan`注解自动收集所有的Spring组件，包括`@Configuration`类。

##### 3.3.2 导入XML配置
如果你绝对需要使用基于XML的配置，我们建议你仍旧从一个`@Configuration`类开始。你可以使用附加的`@ImportResource`注解加载XML配置文件。

#### 3.4 自动配置
Spring Boot自动配置（`auto-configuration`）尝试根据你添加的jar依赖自动配置你的Spring应用。例如，如果你的classpath下存在`HSQLDB`，并且你没有手动配置任何数据库连接beans，那么我们将自动配置一个内存型（in-memory）数据库。

你可以通过将`@EnableAutoConfiguration`或`@SpringBootApplication`注解添加到一个`@Configuration`类上来选择自动配置。

注：你只需要添加一个`@EnableAutoConfiguration`注解。我们建议你将它添加到主`@Configuration`类上。

##### 3.4.1 逐步替换自动配置
自动配置是非侵占性的，任何时候你都可以定义自己的配置类来替换自动配置的特定部分。例如，如果你添加自己的`DataSource` bean，默认的内嵌数据库支持将不被考虑。

如果需要找出当前应用了哪些自动配置及应用的原因，你可以使用`--debug`开关启动应用。这将会记录一个自动配置的报告并输出到控制台。

##### 3.4.2 禁用特定的自动配置
如果发现应用了你不想要的特定自动配置类，你可以使用`@EnableAutoConfiguration`注解的排除属性来禁用它们。

	import org.springframework.boot.autoconfigure.*;
	import org.springframework.boot.autoconfigure.jdbc.*;
	import org.springframework.context.annotation.*;

	@Configuration
	@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
	public class MyConfiguration {
	}

#### 3.5 Spring Beans和依赖注入
你可以自由地使用任何标准的Spring框架技术去定义beans和它们注入的依赖。简单起见，我们经常使用`@ComponentScan`注解搜索beans，并结合`@Autowired`构造器注入。

如果使用上面建议的结构组织代码（将应用类放到根包下），你可以添加`@ComponentScan`注解而不需要任何参数。你的所有应用程序组件（`@Component`, `@Service`, `@Repository`, `@Controller`等）将被自动注册为Spring Beans。

下面是一个`@Service Bean`的示例，它使用构建器注入获取一个需要的RiskAssessor bean。

	package com.example.service;

	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Service;

	@Service
	public class DatabaseAccountService implements AccountService {

	    private final RiskAssessor riskAssessor;

	    @Autowired
	    public DatabaseAccountService(RiskAssessor riskAssessor) {
	        this.riskAssessor = riskAssessor;
	    }

	    // ...
	}

注：注意如何使用构建器注入来允许`riskAssessor`字段被标记为`final`，这意味着`riskAssessor`后续是不能改变的。

#### 3.6 使用@SpringBootApplication注解
很多Spring Boot开发者总是使用`@Configuration`，`@EnableAutoConfiguration`和`@ComponentScan`注解他们的main类。由于这些注解被如此频繁地一块使用（特别是你遵循以上最佳实践时），Spring Boot提供一个方便的`@SpringBootApplication`选择。

该@SpringBootApplication注解等价于以默认属性使用`@Configuration`，`@EnableAutoConfiguration`和`@ComponentScan`。

	package com.example.myproject;

	import org.springframework.boot.SpringApplication;
	import org.springframework.boot.autoconfigure.SpringBootApplication;

	@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
	public class Application {

	    public static void main(String[] args) {
	        SpringApplication.run(Application.class, args);
	    }

	}

#### 3.7 运行应用程序
将应用打包成jar并使用一个内嵌HTTP服务器的一个最大好处是，你可以像其他方式那样运行你的应用程序。调试Spring Boot应用也很简单；你不需要任何特殊IDE或扩展。

注：本章节只覆盖基于jar的打包，如果选择将应用打包成war文件，你最好参考一下服务器和IDE文档。

##### 3.7.1 从IDE中运行
你可以从IDE中运行Spring Boot应用，就像一个简单的Java应用，但是，你首先需要导入项目。导入步骤跟你的IDE和构建系统有关。大多数IDEs能够直接导入Maven项目，例如Eclipse用户可以选择File菜单的`Import…​ --> Existing Maven Projects`。

如果不能直接将项目导入IDE，你可以需要使用构建系统生成IDE元数据。Maven有针对Eclipse和IDEA的插件；Gradle为各种IDEs提供插件。

注：如果意外地运行一个web应用两次，你将看到一个"端口已在使用中"错误。为了确保任何存在的实例是关闭的，STS用户可以使用Relaunch按钮而不是Run按钮。

##### 3.7.2 作为一个打包后的应用运行
如果使用Spring Boot Maven或Gradle插件创建一个可执行jar，你可以使用java -jar运行你的应用。例如：

	$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

运行一个打包的程序并开启远程调试支持是可能的，这允许你将调试器附加到打包的应用程序上：

	$ java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n \
	       -jar target/myproject-0.0.1-SNAPSHOT.jar


##### 3.7.3 使用Maven插件运行
Spring Boot Maven插件包含一个run目标，它可以用来快速编译和运行应用程序。应用程序以一种暴露的方式运行，由于即时"热"加载，你可以编辑资源。

	$ mvn spring-boot:run

你可能想使用有用的操作系统环境变量：

	$ export MAVEN_OPTS=-Xmx1024m -XX:MaxPermSize=128M -Djava.security.egd=file:/dev/./urandom

("egd"设置是通过为Tomcat提供一个更快的会话keys熵源来加速Tomcat的。)

##### 3.7.4 使用Gradle插件运行
Spring Boot Gradle插件也包含一个run目标，它可以用来以暴露的方式运行你的应用程序。不管你什么时候导入`spring-boot-plugin`，bootRun任务总是被添加进去。

	$ gradle bootRun

你可能想使用那些有用的操作系统环境变量：

	$ export JAVA_OPTS=-Xmx1024m -XX:MaxPermSize=128M -Djava.security.egd=file:/dev/./urandom

##### 3.7.5 热交换
由于Spring Boot应用程序只是普通的Java应用，那JVM热交换（hot-swapping）应该能出色的工作。JVM热交换在它能替换的字节码上有些限制，更全面的解决方案可以使用[Spring Loaded](https://github.com/spring-projects/spring-loaded)项目或[JRebel](http://zeroturnaround.com/software/jrebel/)。

关于热交换可以参考“How-to”相应章节。


#### 3.8 打包用于生产的应用程序
可执行jars可用于生产部署。由于它们是自包含的，非常适合基于云的部署。关于其他“生产准备”的特性，比如健康监控，审计和指标REST，或JMX端点，可以考虑添加spring-boot-actuator。具体参考Part V, [“Spring Boot Actuator: Production-ready features”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/V.%20Spring%20Boot%20Actuator/README.md)。

### Spring Boot特性
#### 4.1 SpringApplication
SpringApplication类提供了一种从main()方法启动Spring应用的便捷方式。在很多情况下，你只需委托给SpringApplication.run这个静态方法：

```java
public static void main(String[] args){
    SpringApplication.run(MySpringConfiguration.class, args);
}
```
当应用启动时，你应该会看到类似下面的东西（这是何方神兽？？）：

	.   ____          _            __ _ _
	 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
	( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
	 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
	  '  |____| .__|_| |_|_| |_\__, | / / / /
	 =========|_|==============|___/=/_/_/_/
	 :: Spring Boot ::   v1.2.2.BUILD-SNAPSHOT

	2013-07-31 00:08:16.117  INFO 56603 --- [           main] o.s.b.s.app.SampleApplication            : Starting SampleApplication v0.1.0 on mycomputer with PID 56603 (/apps/myapp.jar started by pwebb)
	2013-07-31 00:08:16.166  INFO 56603 --- [           main] ationConfigEmbeddedWebApplicationContext : Refreshing org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@6e5a8246: startup date [Wed Jul 31 00:08:16 PDT 2013]; root of context hierarchy
	2014-03-04 13:09:54.912  INFO 41370 --- [           main] .t.TomcatEmbeddedServletContainerFactory : Server initialized with port: 8080
	2014-03-04 13:09:56.501  INFO 41370 --- [           main] o.s.b.s.app.SampleApplication

默认情况下会显示INFO级别的日志信息，包括一些相关的启动详情，比如启动应用的用户等。

##### 4.1.1 自定义Banner
通过在classpath下添加一个banner.txt或设置banner.location来指定相应的文件可以改变启动过程中打印的banner。如果这个文件有特殊的编码，你可以使用banner.encoding设置它（默认为UTF-8）。

在banner.txt中可以使用如下的变量：

|变量	|描述|
|:---|:--|
|${application.version}	|MANIFEST.MF中声明的应用版本号，例如1.0|
|${application.formatted-version}|	MANIFEST.MF中声明的被格式化后的应用版本号（被括号包裹且以v作为前缀），用于显示，例如(v1.0)|
|${spring-boot.version}	|正在使用的Spring Boot版本号，例如1.2.2.BUILD-SNAPSHOT|
|${spring-boot.formatted-version}|	正在使用的Spring Boot被格式化后的版本号（被括号包裹且以v作为前缀）, 用于显示，例如(v1.2.2.BUILD-SNAPSHOT)|

注：如果想以编程的方式产生一个banner，可以使用SpringBootApplication.setBanner(…)方法。使用org.springframework.boot.Banner接口，实现你自己的printBanner()方法。

##### 4.1.2 自定义SpringApplication
如果默认的SpringApplication不符合你的口味，你可以创建一个本地的实例并自定义它。例如，关闭banner你可以这样写：

```java
public static void main(String[] args){
    SpringApplication app = new SpringApplication(MySpringConfiguration.class);
    app.setShowBanner(false);
    app.run(args);
}
```

注：传递给SpringApplication的构造器参数是spring beans的配置源。在大多数情况下，这些将是@Configuration类的引用，但它们也可能是XML配置或要扫描包的引用。

你也可以使用application.properties文件来配置SpringApplication。具体参考[Externalized](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IV.%20Spring%20Boot%20features/23.%20Externalized%20Configuration.md) 配置。查看配置选项的完整列表，可参考[SpringApplication Javadoc](http://docs.spring.io/spring-boot/docs/1.2.2.BUILD-SNAPSHOT/api/org/springframework/boot/SpringApplication.html).

##### 4.1.3 流畅的构建API
如果你需要创建一个分层的ApplicationContext（多个具有父子关系的上下文），或你只是喜欢使用流畅的构建API，你可以使用SpringApplicationBuilder。SpringApplicationBuilder允许你以链式方式调用多个方法，包括可以创建层次结构的parent和child方法。

```java
new SpringApplicationBuilder()
    .showBanner(false)
    .sources(Parent.class)
    .child(Application.class)
    .run(args);
```
注：创建ApplicationContext层次时有些限制，比如，Web组件(components)必须包含在子上下文(child context)中，且相同的Environment即用于父上下文也用于子上下文中。具体参考[SpringApplicationBuilder javadoc](http://docs.spring.io/spring-boot/docs/1.2.2.BUILD-SNAPSHOT/api/org/springframework/boot/builder/SpringApplicationBuilder.html)

##### 4.1.4 Application事件和监听器
除了常见的Spring框架事件，比如[ContextRefreshedEvent](http://docs.spring.io/spring/docs/4.1.4.RELEASE/javadoc-api/org/springframework/context/event/ContextRefreshedEvent.html)，一个SpringApplication也发送一些额外的应用事件。一些事件实际上是在ApplicationContext被创建前触发的。

你可以使用多种方式注册事件监听器，最普通的是使用SpringApplication.addListeners(…)方法。在你的应用运行时，应用事件会以下面的次序发送：

1. 在运行开始，但除了监听器注册和初始化以外的任何处理之前，会发送一个ApplicationStartedEvent。
2. 在Environment将被用于已知的上下文，但在上下文被创建前，会发送一个ApplicationEnvironmentPreparedEvent。
3. 在refresh开始前，但在bean定义已被加载后，会发送一个ApplicationPreparedEvent。
4. 启动过程中如果出现异常，会发送一个ApplicationFailedEvent。

注：你通常不需要使用应用程序事件，但知道它们的存在会很方便（在某些场合可能会使用到）。在Spring内部，Spring Boot使用事件处理各种各样的任务。

##### 4.1.5 Web环境
一个SpringApplication将尝试为你创建正确类型的ApplicationContext。在默认情况下，使用AnnotationConfigApplicationContext或AnnotationConfigEmbeddedWebApplicationContext取决于你正在开发的是否是web应用。

用于确定一个web环境的算法相当简单（基于是否存在某些类）。如果需要覆盖默认行为，你可以使用setWebEnvironment(boolean webEnvironment)。通过调用setApplicationContextClass(…)，你可以完全控制ApplicationContext的类型。

注：当JUnit测试里使用SpringApplication时，调用setWebEnvironment(false)是可取的。

##### 4.1.6 命令行启动器
如果你想获取原始的命令行参数，或一旦SpringApplication启动，你需要运行一些特定的代码，你可以实现CommandLineRunner接口。在所有实现该接口的Spring beans上将调用run(String… args)方法。

```java
import org.springframework.boot.*
import org.springframework.stereotype.*

@Component
public class MyBean implements CommandLineRunner {
    public void run(String... args) {
        // Do something...
    }
}
```

如果一些CommandLineRunner beans被定义必须以特定的次序调用，你可以额外实现org.springframework.core.Ordered接口或使用org.springframework.core.annotation.Order注解。

##### 4.1.7 Application退出
每个SpringApplication在退出时为了确保ApplicationContext被优雅的关闭，将会注册一个JVM的shutdown钩子。所有标准的Spring生命周期回调（比如，DisposableBean接口或@PreDestroy注解）都能使用。

此外，如果beans想在应用结束时返回一个特定的退出码（exit code），可以实现org.springframework.boot.ExitCodeGenerator接口。

#### 4.2 外化配置
Spring Boot允许外化（externalize）你的配置，这样你能够在不同的环境下使用相同的代码。你可以使用properties文件，YAML文件，环境变量和命令行参数来外化配置。使用@Value注解，可以直接将属性值注入到你的beans中，并通过Spring的Environment抽象或绑定到结构化对象来访问。

Spring Boot使用一个非常特别的PropertySource次序来允许对值进行合理的覆盖，需要以下面的次序考虑属性：

1. 命令行参数
2. 来自于java:comp/env的JNDI属性
3. Java系统属性（System.getProperties()）
4. 操作系统环境变量
5. 只有在random.*里包含的属性会产生一个RandomValuePropertySource
6. 在打包的jar外的应用程序配置文件（application.properties，包含YAML和profile变量）
7. 在打包的jar内的应用程序配置文件（application.properties，包含YAML和profile变量）
8. 在@Configuration类上的@PropertySource注解
9. 默认属性（使用SpringApplication.setDefaultProperties指定）

下面是一个具体的示例（假设你开发一个使用name属性的@Component）：

```java
import org.springframework.stereotype.*
import org.springframework.beans.factory.annotation.*

@Component
public class MyBean {
    @Value("${name}")
    private String name;
    // ...
}
```

你可以将一个application.properties文件捆绑到jar内，用来提供一个合理的默认name属性值。当运行在生产环境时，可以在jar外提供一个application.properties文件来覆盖name属性。对于一次性的测试，你可以使用特定的命令行开关启动（比如，java -jar app.jar --name="Spring"）。


##### 4.2.1 配置随机值
RandomValuePropertySource在注入随机值（比如，密钥或测试用例）时很有用。它能产生整数，longs或字符串，比如：

```java
my.secret=${random.value}
my.number=${random.int}
my.bignumber=${random.long}
my.number.less.than.ten=${random.int(10)}
my.number.in.range=${random.int[1024,65536]}
```

random.int*语法是OPEN value (,max) CLOSE，此处OPEN，CLOSE可以是任何字符，并且value，max是整数。如果提供max，那么value是最小的值，max是最大的值（不包含在内）。

##### 4.2.2 访问命令行属性
默认情况下，SpringApplication将任何可选的命令行参数（以'--'开头，比如，--server.port=9000）转化为property，并将其添加到Spring Environment中。如上所述，命令行属性总是优先于其他属性源。

如果你不想将命令行属性添加到Environment里，你可以使用SpringApplication.setAddCommandLineProperties(false)来禁止它们。

##### 4.2.3 Application属性文件
SpringApplication将从以下位置加载application.properties文件，并把它们添加到Spring Environment中：

1. 当前目录下的一个/config子目录
2. 当前目录
3. 一个classpath下的/config包
4. classpath根路径（root）

这个列表是按优先级排序的（列表中位置高的将覆盖位置低的）。

注：你可以使用YAML（'.yml'）文件替代'.properties'。

如果不喜欢将application.properties作为配置文件名，你可以通过指定spring.config.name环境属性来切换其他的名称。你也可以使用spring.config.location环境属性来引用一个明确的路径（目录位置或文件路径列表以逗号分割）。

	$ java -jar myproject.jar --spring.config.name=myproject
	//or
	$ java -jar myproject.jar --spring.config.location=classpath:/default.properties,classpath:/override.properties

如果spring.config.location包含目录（相对于文件），那它们应该以/结尾（在加载前，spring.config.name产生的名称将被追加到后面）。不管spring.config.location是什么值，默认的搜索路径classpath:,classpath:/config,file:,file:config/总会被使用。以这种方式，你可以在application.properties中为应用设置默认值，然后在运行的时候使用不同的文件覆盖它，同时保留默认配置。

注：如果你使用环境变量而不是系统配置，大多数操作系统不允许以句号分割（period-separated）的key名称，但你可以使用下划线（underscores）代替（比如，使用SPRING_CONFIG_NAME代替spring.config.name）。如果你的应用运行在一个容器中，那么JNDI属性（java:comp/env）或servlet上下文初始化参数可以用来取代环境变量或系统属性，当然也可以使用环境变量或系统属性。

##### 4.2.4 特定的Profile属性
除了application.properties文件，特定配置属性也能通过命令惯例application-{profile}.properties来定义。特定Profile属性从跟标准application.properties相同的路径加载，并且特定profile文件会覆盖默认的配置。

##### 4.2.5 属性占位符
当application.properties里的值被使用时，它们会被存在的Environment过滤，所以你能够引用先前定义的值（比如，系统属性）。

	app.name=MyApp
	app.description=${app.name} is a Spring Boot application

注：你也能使用相应的技巧为存在的Spring Boot属性创建'短'变量，具体参考[Section 63.3, “Use ‘short’ command line arguments”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/63.3.%20Use%20‘short’%20command%20line%20arguments.md)。

##### 4.2.6 使用YAML代替Properties
[YAML](http://yaml.org/)是JSON的一个超集，也是一种方便的定义层次配置数据的格式。无论你何时将[SnakeYAML](http://code.google.com/p/snakeyaml/) 库放到classpath下，SpringApplication类都会自动支持YAML作为properties的替换。

注：如果你使用'starter POMs'，spring-boot-starter会自动提供SnakeYAML。

###### 4.2.6.1 加载YAML
Spring框架提供两个便利的类用于加载YAML文档，YamlPropertiesFactoryBean会将YAML作为Properties来加载，YamlMapFactoryBean会将YAML作为Map来加载。

示例：

	environments:
	    dev:
	        url: http://dev.bar.com
	        name: Developer Setup
	    prod:
	        url: http://foo.bar.com
	        name: My Cool App

上面的YAML文档会被转化到下面的属性中：

	environments.dev.url=http://dev.bar.com
	environments.dev.name=Developer Setup
	environments.prod.url=http://foo.bar.com
	environments.prod.name=My Cool App

YAML列表被表示成使用[index]间接引用作为属性keys的形式，例如下面的YAML：

	my:
	   servers:
	       - dev.bar.com
	       - foo.bar.com

将会转化到下面的属性中:

	my.servers[0]=dev.bar.com
	my.servers[1]=foo.bar.com

使用Spring DataBinder工具绑定那样的属性（这是@ConfigurationProperties做的事），你需要确定目标bean中有个java.util.List或Set类型的属性，并且需要提供一个setter或使用可变的值初始化它，比如，下面的代码将绑定上面的属性：

	@ConfigurationProperties(prefix="my")
	public class Config {
	    private List<String> servers = new ArrayList<String>();
	    public List<String> getServers() {
	        return this.servers;
	    }
	}

###### 4.2.6.2 在Spring环境中使用YAML暴露属性
YamlPropertySourceLoader类能够用于将YAML作为一个PropertySource导出到Sprig Environment。这允许你使用熟悉的@Value注解和占位符语法访问YAML属性。

###### 4.2.6.3 Multi-profile YAML文档
你可以在单个文件中定义多个特定配置（profile-specific）的YAML文档，并通过一个spring.profiles key标示应用的文档。例如：

	server:
	    address: 192.168.1.100
	---
	spring:
	    profiles: development
	server:
	    address: 127.0.0.1
	---
	spring:
	    profiles: production
	server:
	    address: 192.168.1.120

在上面的例子中，如果development配置被激活，那server.address属性将是127.0.0.1。如果development和production配置（profiles）没有启用，则该属性的值将是192.168.1.100。

###### 4.2.6.4 YAML缺点
YAML文件不能通过@PropertySource注解加载。所以，在这种情况下，如果需要使用@PropertySource注解的方式加载值，那就要使用properties文件。

##### 4.2.7 类型安全的配置属性
使用@Value("${property}")注解注入配置属性有时可能比较笨重，特别是需要使用多个properties或你的数据本身有层次结构。为了控制和校验你的应用配置，Spring Boot提供一个允许强类型beans的替代方法来使用properties。

示例：

	@Component
	@ConfigurationProperties(prefix="connection")
	public class ConnectionSettings {
	    private String username;
	    private InetAddress remoteAddress;
	    // ... getters and setters
	}

当@EnableConfigurationProperties注解应用到你的@Configuration时，任何被@ConfigurationProperties注解的beans将自动被Environment属性配置。这种风格的配置特别适合与SpringApplication的外部YAML配置进行配合使用。

	# application.yml
	connection:
	    username: admin
	    remoteAddress: 192.168.1.1
	# additional configuration as required

为了使用@ConfigurationProperties beans，你可以使用与其他任何bean相同的方式注入它们。

	@Service
	public class MyService {
	    @Autowired
	    private ConnectionSettings connection;
	     //...
	    @PostConstruct
	    public void openConnection() {
	        Server server = new Server();
	        this.connection.configure(server);
	    }
	}

你可以通过在@EnableConfigurationProperties注解中直接简单的列出属性类来快捷的注册@ConfigurationProperties bean的定义。

	@Configuration
	@EnableConfigurationProperties(ConnectionSettings.class)
	public class MyConfiguration {
	}

注：使用@ConfigurationProperties能够产生可被IDEs使用的元数据文件。具体参考[Appendix B, Configuration meta-data](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/X.%20Appendices/B.%20Configuration%20meta-data.md)。

###### 4.2.7.1 第三方配置
正如使用@ConfigurationProperties注解一个类，你也可以在@Bean方法上使用它。当你需要绑定属性到不受你控制的第三方组件时，这种方式非常有用。

为了从Environment属性配置一个bean，将@ConfigurationProperties添加到它的bean注册过程：

	@ConfigurationProperties(prefix = "foo")
	@Bean
	public FooComponent fooComponent() {
	    ...
	}

和上面ConnectionSettings的示例方式相同，任何以foo为前缀的属性定义都会被映射到FooComponent上。

###### 4.2.7.2 松散的绑定（Relaxed binding）
Spring Boot使用一些宽松的规则用于绑定Environment属性到@ConfigurationProperties beans，所以Environment属性名和bean属性名不需要精确匹配。常见的示例中有用的包括虚线分割（比如，context--path绑定到contextPath）和将环境属性转为大写字母（比如，PORT绑定port）。

示例：

	@Component
	@ConfigurationProperties(prefix="person")
	public class ConnectionSettings {
	    private String firstName;
	}

下面的属性名都能用于上面的@ConfigurationProperties类：


|属性|	说明|
|:--|:--|
|person.firstName	|标准驼峰规则|
|person.first-name	|虚线表示，推荐用于.properties和.yml文件中|
|PERSON_FIRST_NAME	|大写形式，使用系统环境变量时推荐|

Spring会尝试强制外部的应用属性在绑定到@ConfigurationProperties beans时类型是正确的。如果需要自定义类型转换，你可以提供一个ConversionService bean（bean id为conversionService）或自定义属性编辑器（通过一个CustomEditorConfigurer bean）。

###### 4.2.7.3 @ConfigurationProperties校验
Spring Boot将尝试校验外部的配置，默认使用JSR-303（如果在classpath路径中）。你可以轻松的为你的@ConfigurationProperties类添加JSR-303 javax.validation约束注解：

	@Component
	@ConfigurationProperties(prefix="connection")
	public class ConnectionSettings {
	    @NotNull
	    private InetAddress remoteAddress;
	    // ... getters and setters
	}

你也可以通过创建一个叫做configurationPropertiesValidator的bean来添加自定义的Spring Validator。

注：spring-boot-actuator模块包含一个暴露所有@ConfigurationProperties beans的端点。简单地将你的web浏览器指向/configprops或使用等效的JMX端点。具体参考[Production ready features](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/V.%20Spring%20Boot%20Actuator/40.%20Endpoints.md)。

#### 4.3 Profiles
Spring Profiles提供了一种隔离应用程序配置的方式，并让这些配置只能在特定的环境下生效。任何@Component或@Configuration都能被@Profile标记，从而限制加载它的时机。

	@Configuration
	@Profile("production")
	public class ProductionConfiguration {
	    // ...
	}

以正常的Spring方式，你可以使用一个spring.profiles.active的Environment属性来指定哪个配置生效。你可以使用平常的任何方式来指定该属性，例如，可以将它包含到你的application.properties中：

	spring.profiles.active=dev,hsqldb

或使用命令行开关：

	--spring.profiles.active=dev,hsqldb

##### 4.3.1 添加激活的配置(profiles)
spring.profiles.active属性和其他属性一样都遵循相同的排列规则，最高的PropertySource获胜。也就是说，你可以在application.properties中指定生效的配置，然后使用命令行开关替换它们。

有时，将特定的配置属性添加到生效的配置中而不是替换它们是有用的。spring.profiles.include属性可以用来无条件的添加生效的配置。SpringApplication的入口点也提供了一个用于设置额外配置的Java API（比如，在那些通过spring.profiles.active属性生效的配置之上）：参考setAdditionalProfiles()方法。

示例：当一个应用使用下面的属性，并用--spring.profiles.active=prod开关运行，那proddb和prodmq配置也会生效：

	---
	my.property: fromyamlfile
	---
	spring.profiles: prod
	spring.profiles.include: proddb,prodmq

注：spring.profiles属性可以定义到一个YAML文档中，用于决定什么时候该文档被包含进配置中。具体参考Section 63.6, [“Change configuration depending on the environment”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/63.6.%20Change%20configuration%20depending%20on%20the%20environment.md)


##### 4.3.2 以编程方式设置profiles
在应用运行前，你可以通过调用SpringApplication.setAdditionalProfiles(…)方法，以编程的方式设置生效的配置。使用Spring的ConfigurableEnvironment接口激动配置也是可行的。

##### 4.3.3 Profile特定配置文件
application.properties（或application.yml）和通过@ConfigurationProperties引用的文件这两种配置特定变种都被当作文件来加载的，具体参考Section 23.3, [“Profile specific properties”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IV.%20Spring%20Boot%20features/23.4.%20Profile-specific%20properties.md)。

#### 4.5 日志
Spring Boot内部日志系统使用的是[Commons Logging](http://commons.apache.org/logging)，但开放底层的日志实现。默认为会[Java Util Logging](http://docs.oracle.com/javase/7/docs/api/java/util/logging/package-summary.html), [Log4J](http://logging.apache.org/log4j/), [Log4J2](http://logging.apache.org/log4j/2.x/)和[Logback](http://logback.qos.ch/)提供配置。每种情况下都会预先配置使用控制台输出，也可以使用可选的文件输出。

默认情况下，如果你使用'Starter POMs'，那么就会使用Logback记录日志。为了确保那些使用Java Util Logging, Commons Logging, Log4J或SLF4J的依赖库能够正常工作，正确的Logback路由也被包含进来。

注：如果上面的列表看起来令人困惑，不要担心，Java有很多可用的日志框架。通常，你不需要改变日志依赖，Spring Boot默认的就能很好的工作。

##### 4.4.1 日志格式
Spring Boot默认的日志输出格式如下：

	2014-03-05 10:57:51.112  INFO 45469 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/7.0.52
	2014-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
	2014-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1358 ms
	2014-03-05 10:57:51.698  INFO 45469 --- [ost-startStop-1] o.s.b.c.e.ServletRegistrationBean        : Mapping servlet: 'dispatcherServlet' to [/]
	2014-03-05 10:57:51.702  INFO 45469 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]

输出的节点（items）如下：

1. 日期和时间 - 精确到毫秒，且易于排序。
2. 日志级别 - ERROR, WARN, INFO, DEBUG 或 TRACE。
3. Process ID。
4. 一个用于区分实际日志信息开头的---分隔符。
5. 线程名 - 包括在方括号中（控制台输出可能会被截断）。
6. 日志名 - 通常是源class的类名（缩写）。
7. 日志信息。


##### 4.4.2 控制台输出
默认的日志配置会在写日志消息时将它们回显到控制台。默认，ERROR, WARN和INFO级别的消息会被记录。可以在启动应用时，通过--debug标识开启控制台的DEBUG级别日志记录。

	$ java -jar myapp.jar --debug

如果你的终端支持ANSI，为了增加可读性将会使用彩色的日志输出。你可以设置spring.output.ansi.enabled为一个[支持的值](http://docs.spring.io/spring-boot/docs/1.2.2.BUILD-SNAPSHOT/api/org/springframework/boot/ansi/AnsiOutput.Enabled.html)来覆盖自动检测。

##### 4.4.3 文件输出
默认情况下，Spring Boot只会将日志记录到控制台而不会写进日志文件。如果除了输出到控制台你还想写入到日志文件，那你需要设置logging.file或logging.path属性（例如在你的application.properties中）。

下表显示如何组合使用`logging.*`：


|logging.file|	logging.path	|示例|	描述|
|:--|:--|:--|:--|
|(none)	|(none)		||只记录到控制台|
|Specific file	|(none)	|my.log	|写到特定的日志文件里，名称可以是一个精确的位置或相对于当前目录|
|(none)	|Specific folder|	/var/log|	写到特定文件夹下的spring.log里，名称可以是一个精确的位置或相对于当前目录|

日志文件每达到10M就会被轮换（分割），和控制台一样，默认记录ERROR, WARN和INFO级别的信息。

##### 4.4.4 日志级别
所有支持的日志系统在Spring的Environment（例如在application.properties里）都有通过'logging.level.*=LEVEL'（'LEVEL'是TRACE, DEBUG, INFO, WARN, ERROR, FATAL, OFF中的一个）设置的日志级别。

示例：application.properties

	logging.level.org.springframework.web: DEBUG
	logging.level.org.hibernate: ERROR

##### 4.4.5 自定义日志配置
通过将适当的库添加到classpath，可以激活各种日志系统。然后在classpath的根目录(root)或通过Spring Environment的logging.config属性指定的位置提供一个合适的配置文件来达到进一步的定制（注意由于日志是在ApplicationContext被创建之前初始化的，所以不可能在Spring的@Configuration文件中，通过@PropertySources控制日志。系统属性和平常的Spring Boot外部配置文件能正常工作）。

根据你的日志系统，下面的文件会被加载：

|日志系统	|定制|
|:--|:--|
|Logback|	logback.xml|
|Log4j	|log4j.properties或log4j.xml|
|Log4j2	|log4j2.xml|
|JDK (Java Util Logging)	|logging.properties|
为了帮助定制一些其他的属性，从Spring的Envrionment转换到系统属性：

|Spring Environment	|	System Property		|评价|
|:--|:--|:--|
|logging.file	|LOG_FILE|	如果定义，在默认的日志配置中使用|
|logging.path	|LOG_PATH|	如果定义，在默认的日志配置中使用|
|PID		|PID	|	当前的处理进程(process)ID（如果能够被发现且还没有作为操作系统环境变量被定义）|

所有支持的日志系统在解析它们的配置文件时都能查询系统属性。具体可以参考spring-boot.jar中的默认配置。

注：在运行可执行的jar时，Java Util Logging有类加载问题，我们建议你尽可能避免使用它。

#### 4.5 开发web应用
Spring Boot非常适合开发web应用程序。你可以使用内嵌的Tomcat，Jetty或Undertow轻轻松松地创建一个HTTP服务器。大多数的web应用都使用spring-boot-starter-web模块进行快速搭建和运行。

##### 4.5.1 Spring Web MVC 框架
Spring Web MVC框架（通常简称为"Spring MVC"）是一个富"模型，视图，控制器"的web框架。 Spring MVC允许你创建特定的@Controller或@RestController beans来处理传入的HTTP请求。 使用@RequestMapping注解可以将控制器中的方法映射到相应的HTTP请求。

示例：

```java
@RestController
@RequestMapping(value="/users")
public class MyRestController {

    @RequestMapping(value="/{user}", method=RequestMethod.GET)
    public User getUser(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}/customers", method=RequestMethod.GET)
    List<Customer> getUserCustomers(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}", method=RequestMethod.DELETE)
    public User deleteUser(@PathVariable Long user) {
        // ...
    }
}
```

###### 4.5.1.1 Spring MVC自动配置
Spring Boot为Spring MVC提供适用于多数应用的自动配置功能。在Spring默认基础上，自动配置添加了以下特性：

1. 引入ContentNegotiatingViewResolver和BeanNameViewResolver beans。
2. 对静态资源的支持，包括对WebJars的支持。
3. 自动注册Converter，GenericConverter，Formatter beans。
4. 对HttpMessageConverters的支持。
5. 自动注册MessageCodeResolver。
6. 对静态index.html的支持。
7. 对自定义Favicon的支持。

如果想全面控制Spring MVC，你可以添加自己的@Configuration，并使用@EnableWebMvc对其注解。如果想保留Spring Boot MVC的特性，并只是添加其他的MVC配置(拦截器，formatters，视图控制器等)，你可以添加自己的WebMvcConfigurerAdapter类型的@Bean（不使用@EnableWebMvc注解）。

###### 4.5.1.2 HttpMessageConverters
Spring MVC使用HttpMessageConverter接口转换HTTP请求和响应。合理的缺省值被包含的恰到好处（out of the box），例如对象可以自动转换为JSON（使用Jackson库）或XML（如果Jackson XML扩展可用则使用它，否则使用JAXB）。字符串默认使用UTF-8编码。

如果需要添加或自定义转换器，你可以使用Spring Boot的HttpMessageConverters类：

```java
import org.springframework.boot.autoconfigure.web.HttpMessageConverters;
import org.springframework.context.annotation.*;
import org.springframework.http.converter.*;

@Configuration
public class MyConfiguration {

    @Bean
    public HttpMessageConverters customConverters() {
        HttpMessageConverter<?> additional = ...
        HttpMessageConverter<?> another = ...
        return new HttpMessageConverters(additional, another);
    }
}
```
任何在上下文中出现的HttpMessageConverter bean将会添加到converters列表，你可以通过这种方式覆盖默认的转换器（converters）。

###### 4.5.1.3 MessageCodesResolver
Spring MVC有一个策略，用于从绑定的errors产生用来渲染错误信息的错误码：MessageCodesResolver。如果设置`spring.mvc.message-codes-resolver.format`属性为`PREFIX_ERROR_CODE`或`POSTFIX_ERROR_CODE`（具体查看`DefaultMessageCodesResolver.Format`枚举值），Spring Boot会为你创建一个MessageCodesResolver。

###### 4.5.1.4 静态内容
默认情况下，Spring Boot从classpath下一个叫/static（/public，/resources或/META-INF/resources）的文件夹或从ServletContext根目录提供静态内容。这使用了Spring MVC的ResourceHttpRequestHandler，所以你可以通过添加自己的WebMvcConfigurerAdapter并覆写addResourceHandlers方法来改变这个行为（加载静态文件）。

在一个单独的web应用中，容器默认的servlet是开启的，如果Spring决定不处理某些请求，默认的servlet作为一个回退（降级）将从ServletContext根目录加载内容。大多数时候，这不会发生（除非你修改默认的MVC配置），因为Spring总能够通过DispatcherServlet处理请求。

此外，上述标准的静态资源位置有个例外情况是[Webjars](http://www.webjars.org/)内容。任何在/webjars/**路径下的资源都将从jar文件中提供，只要它们以Webjars的格式打包。

注：如果你的应用将被打包成jar，那就不要使用src/main/webapp文件夹。尽管该文件夹是一个共同的标准，但它仅在打包成war的情况下起作用，并且如果产生一个jar，多数构建工具都会静悄悄的忽略它。

###### 4.5.1.5 模板引擎
正如REST web服务，你也可以使用Spring MVC提供动态HTML内容。Spring MVC支持各种各样的模板技术，包括Velocity, FreeMarker和JSPs。很多其他的模板引擎也提供它们自己的Spring MVC集成。

Spring Boot为以下的模板引擎提供自动配置支持：

1. [FreeMarker](http://freemarker.org/docs/)
2. [Groovy](http://beta.groovy-lang.org/docs/groovy-2.3.0/html/documentation/markup-template-engine.html)
3. [Thymeleaf](http://www.thymeleaf.org/)
4. [Velocity](http://velocity.apache.org/)

注：如果可能的话，应该忽略JSPs，因为在内嵌的servlet容器使用它们时存在一些[已知的限制](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IV.%20Spring%20Boot%20features/26.3.4.%20JSP%20limitations.md)。

当你使用这些引擎的任何一种，并采用默认的配置，你的模板将会从src/main/resources/templates目录下自动加载。

注：IntelliJ IDEA根据你运行应用的方式会对classpath进行不同的整理。在IDE里通过main方法运行你的应用跟从Maven或Gradle或打包好的jar中运行相比会导致不同的顺序。这可能导致Spring Boot不能从classpath下成功地找到模板。如果遇到这个问题，你可以在IDE里重新对classpath进行排序，将模块的类和资源放到第一位。或者，你可以配置模块的前缀为classpath*:/templates/，这样会查找classpath下的所有模板目录。

###### 4.5.1.6 错误处理
Spring Boot默认提供一个/error映射用来以合适的方式处理所有的错误，并且它在servlet容器中注册了一个全局的 错误页面。对于机器客户端（相对于浏览器而言，浏览器偏重于人的行为），它会产生一个具有详细错误，HTTP状态，异常信息的JSON响应。对于浏览器客户端，它会产生一个白色标签样式（whitelabel）的错误视图，该视图将以HTML格式显示同样的数据（可以添加一个解析为erro的View来自定义它）。为了完全替换默认的行为，你可以实现ErrorController，并注册一个该类型的bean定义，或简单地添加一个ErrorAttributes类型的bean以使用现存的机制，只是替换显示的内容。

如果在某些条件下需要比较多的错误页面，内嵌的servlet容器提供了一个统一的Java DSL（领域特定语言）来自定义错误处理。 示例：

```java
@Bean
public EmbeddedServletContainerCustomizer containerCustomizer(){
    return new MyCustomizer();
}

// ...
private static class MyCustomizer implements EmbeddedServletContainerCustomizer {
    @Override
    public void customize(ConfigurableEmbeddedServletContainer container) {
        container.addErrorPages(new ErrorPage(HttpStatus.BAD_REQUEST, "/400"));
    }
}
```

你也可以使用常规的Spring MVC特性来处理错误，比如[@ExceptionHandler](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#mvc-exceptionhandlers)方法和[@ControllerAdvice](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#mvc-ann-controller-advice)。ErrorController将会捡起任何没有处理的异常。

N.B. 如果你为一个路径注册一个ErrorPage，最终被一个过滤器（Filter）处理（对于一些非Spring web框架，像Jersey和Wicket这很常见），然后过滤器需要显式注册为一个ERROR分发器（dispatcher）。

```java
@Bean
public FilterRegistrationBean myFilter() {
    FilterRegistrationBean registration = new FilterRegistrationBean();
    registration.setFilter(new MyFilter());
    ...
    registration.setDispatcherTypes(EnumSet.allOf(DispatcherType.class));
    return registration;
}
```
注：默认的FilterRegistrationBean没有包含ERROR分发器类型。

###### 4.5.1.7 Spring HATEOAS
如果你正在开发一个使用超媒体的RESTful API，Spring Boot将为Spring HATEOAS提供自动配置，这在多数应用中都工作良好。自动配置替换了对使用@EnableHypermediaSupport的需求，并注册一定数量的beans来简化构建基于超媒体的应用，这些beans包括一个LinkDiscoverer和配置好的用于将响应正确编排为想要的表示的ObjectMapper。ObjectMapper可以根据spring.jackson.*属性或一个存在的Jackson2ObjectMapperBuilder bean进行自定义。

通过使用@EnableHypermediaSupport，你可以控制Spring HATEOAS的配置。注意这会禁用上述的对ObjectMapper的自定义。

##### 4.5.2 JAX-RS和Jersey
如果喜欢JAX-RS为REST端点提供的编程模型，你可以使用可用的实现替代Spring MVC。如果在你的应用上下文中将Jersey 1.x和Apache Celtix的Servlet或Filter注册为一个@Bean，那它们工作的相当好。Jersey 2.x有一些原生的Spring支持，所以我们会在Spring Boot为它提供自动配置支持，连同一个启动器（starter）。

想要开始使用Jersey 2.x只需要加入spring-boot-starter-jersey依赖，然后你需要一个ResourceConfig类型的@Bean，用于注册所有的端点（endpoints）。

	@Component
	public class JerseyConfig extends ResourceConfig {
	    public JerseyConfig() {
	        register(Endpoint.class);
	    }
	}
所有注册的端点都应该被@Components和HTTP资源annotations（比如@GET）注解。

	@Component
	@Path("/hello")
	public class Endpoint {
	    @GET
	    public String message() {
	        return "Hello";
	    }
	}
由于Endpoint是一个Spring组件（@Component），所以它的生命周期受Spring管理，并且你可以使用@Autowired添加依赖及使用@Value注入外部配置。Jersey servlet将被注册，并默认映射到/*。你可以将@ApplicationPath添加到ResourceConfig来改变该映射。

默认情况下，Jersey将在一个ServletRegistrationBean类型的@Bean中被设置成名称为jerseyServletRegistration的Servlet。通过创建自己的相同名称的bean，你可以禁止或覆盖这个bean。你也可以通过设置spring.jersey.type=filter来使用一个Filter代替Servlet（在这种情况下，被覆盖或替换的@Bean是jerseyFilterRegistration）。该servlet有@Order属性，你可以通过spring.jersey.filter.order进行设置。不管是Servlet还是Filter注册都可以使用spring.jersey.init.*定义一个属性集合作为初始化参数传递过去。

这里有一个[Jersey](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-jersey)示例，你可以查看如何设置相关事项。

##### 4.5.3 内嵌servlet容器支持
Spring Boot支持内嵌的Tomcat, Jetty和Undertow服务器。多数开发者只需要使用合适的'Starter POM'来获取一个完全配置好的实例即可。默认情况下，内嵌的服务器会在8080端口监听HTTP请求。

###### 4.5.3.1 Servlets和Filters
当使用内嵌的servlet容器时，你可以直接将servlet和filter注册为Spring的beans。在配置期间，如果你想引用来自application.properties的值，这是非常方便的。默认情况下，如果上下文只包含单一的Servlet，那它将被映射到根路径（/）。在多Servlet beans的情况下，bean的名称将被用作路径的前缀。过滤器会被映射到/*。

如果基于约定（convention-based）的映射不够灵活，你可以使用ServletRegistrationBean和FilterRegistrationBean类实现完全的控制。如果你的bean实现了ServletContextInitializer接口，也可以直接注册它们。

###### 4.5.3.2 EmbeddedWebApplicationContext
Spring Boot底层使用了一个新的ApplicationContext类型，用于对内嵌servlet容器的支持。EmbeddedWebApplicationContext是一个特殊类型的WebApplicationContext，它通过搜索一个单一的EmbeddedServletContainerFactory bean来启动自己。通常，TomcatEmbeddedServletContainerFactory，JettyEmbeddedServletContainerFactory或UndertowEmbeddedServletContainerFactory将被自动配置。

注：你通常不需要知道这些实现类。大多数应用将被自动配置，并根据你的行为创建合适的ApplicationContext和EmbeddedServletContainerFactory。

###### 4.5.3.3 自定义内嵌servlet容器
常见的Servlet容器设置可以通过Spring Environment属性进行配置。通常，你会把这些属性定义到application.properties文件中。 常见的服务器设置包括：

1. server.port - 进来的HTTP请求的监听端口号
2. server.address - 绑定的接口地址
3. server.sessionTimeout - session超时时间

具体参考[ServerProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ServerProperties.java)。

*编程方式的自定义*
如果需要以编程的方式配置内嵌的servlet容器，你可以注册一个实现EmbeddedServletContainerCustomizer接口的Spring bean。EmbeddedServletContainerCustomizer提供对ConfigurableEmbeddedServletContainer的访问，ConfigurableEmbeddedServletContainer包含很多自定义的setter方法。

	import org.springframework.boot.context.embedded.*;
	import org.springframework.stereotype.Component;

	@Component
	public class CustomizationBean implements EmbeddedServletContainerCustomizer {
	    @Override
	    public void customize(ConfigurableEmbeddedServletContainer container) {
	        container.setPort(9000);
	    }
	}
直接自定义ConfigurableEmbeddedServletContainer
如果上面的自定义手法过于受限，你可以自己注册TomcatEmbeddedServletContainerFactory，JettyEmbeddedServletContainerFactory或UndertowEmbeddedServletContainerFactory。

	@Bean
	public EmbeddedServletContainerFactory servletContainer() {
	    TomcatEmbeddedServletContainerFactory factory = new TomcatEmbeddedServletContainerFactory();
	    factory.setPort(9000);
	    factory.setSessionTimeout(10, TimeUnit.MINUTES);
	    factory.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND, "/notfound.html");
	    return factory;
	}
很多可选的配置都提供了setter方法，也提供了一些受保护的钩子方法以满足你的某些特殊需求。具体参考相关文档。

###### 4.5.3.4 JSP的限制
在内嵌的servlet容器中运行一个Spring Boot应用时（并打包成一个可执行的存档archive），容器对JSP的支持有一些限制。

1. tomcat只支持war的打包方式，不支持可执行的jar。
2. 内嵌的Jetty目前不支持JSPs。
3. Undertow不支持JSPs。

这里有个[JSP示例](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-web-jsp)，你可以查看如何设置相关事项。

#### 4.6 安全
如果Spring Security在classpath下，那么web应用默认对所有的HTTP路径（也称为终点，端点，表示API的具体网址）使用'basic'认证。为了给web应用添加方法级别的保护，你可以添加@EnableGlobalMethodSecurity并使用想要的设置。其他信息参考[Spring Security Reference](http://docs.spring.io/spring-security/site/docs/3.2.5.RELEASE/reference/htmlsingle#jc-method)。

默认的AuthenticationManager有一个单一的user（'user'的用户名和随机密码会在应用启动时以INFO日志级别打印出来）。如下：

	Using default security password: 78fa095d-3f4c-48b1-ad50-e24c31d5cf35

注：如果你对日志配置进行微调，确保org.springframework.boot.autoconfigure.security类别能记录INFO信息，否则默认的密码不会被打印。

你可以通过提供security.user.password改变默认的密码。这些和其他有用的属性通过[SecurityProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/security/SecurityProperties.java)（以security为前缀的属性）被外部化了。

默认的安全配置（security configuration）是在SecurityAutoConfiguration和导入的类中实现的（SpringBootWebSecurityConfiguration用于web安全，AuthenticationManagerConfiguration用于与非web应用也相关的认证配置）。你可以添加一个@EnableWebSecurity bean来彻底关掉Spring Boot的默认配置。为了对它进行自定义，你需要使用外部的属性配置和WebSecurityConfigurerAdapter类型的beans（比如，添加基于表单的登陆）。在Spring Boot示例里有一些安全相关的应用可以带你体验常见的用例。

在一个web应用中你能得到的基本特性如下：

一个使用内存存储的AuthenticationManager bean和唯一的user（查看SecurityProperties.User获取user的属性）。
忽略（不保护）常见的静态资源路径（/css/**, /js/**, /images/**和 **/favicon.ico）。
对其他的路径实施HTTP Basic安全保护。
安全相关的事件会发布到Spring的ApplicationEventPublisher（成功和失败的认证，拒绝访问）。
Spring Security提供的常见底层特性（HSTS, XSS, CSRF, 缓存）默认都被开启。
上述所有特性都能打开和关闭，或使用外部的配置进行修改（security.*）。为了覆盖访问规则（access rules）而不改变其他自动配置的特性，你可以添加一个使用@Order(SecurityProperties.ACCESS_OVERRIDE_ORDER)注解的WebSecurityConfigurerAdapter类型的@Bean。

如果Actuator也在使用，你会发现：

即使应用路径不受保护，被管理的路径也会受到保护。
安全相关的事件被转换为AuditEvents（审计事件），并发布给AuditService。
默认的用户有ADMIN和USER的角色。
使用外部属性能够修改Actuator（执行器）的安全特性（management.security.*）。为了覆盖应用程序的访问规则，你可以添加一个WebSecurityConfigurerAdapter类型的@Bean。同时，如果不想覆盖执行器的访问规则，你可以使用@Order(SecurityProperties.ACCESS_OVERRIDE_ORDER)注解该bean，否则使用@Order(ManagementServerProperties.ACCESS_OVERRIDE_ORDER)注解该bean。

#### 4.7 使用sql数据库
Spring框架为使用SQL数据库提供了广泛的支持。从使用JdbcTemplate直接访问JDBC到完全的对象关系映射技术，比如Hibernate。Spring Data提供一个额外的功能，直接从接口创建Repository实现，并使用约定从你的方法名生成查询。

##### 4.7.1 配置DataSource
Java的javax.sql.DataSource接口提供了一个标准的使用数据库连接的方法。传统做法是，一个DataSource使用一个URL连同相应的证书去初始化一个数据库连接。

###### 4.7.1.1 对内嵌数据库的支持
开发应用时使用内存数据库是很实用的。显而易见地，内存数据库不需要提供持久化存储。你不需要在应用启动时填充数据库，也不需要在应用结束时丢弃数据。

Spring Boot可以自动配置的内嵌数据库包括[H2](http://www.h2database.com/), [HSQL](http://hsqldb.org/)和[Derby](http://db.apache.org/derby/)。你不需要提供任何连接URLs，只需要简单的添加你想使用的内嵌数据库依赖。

示例：典型的POM依赖如下：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-data-jpa</artifactId>
	</dependency>
	<dependency>
	    <groupId>org.hsqldb</groupId>
	    <artifactId>hsqldb</artifactId>
	    <scope>runtime</scope>
	</dependency>
注：对于自动配置的内嵌数据库，你需要依赖spring-jdbc。在示例中，它通过spring-boot-starter-data-jpa被传递地拉过来了。

###### 4.7.1.2 连接到一个生产环境数据库
在生产环境中，数据库连接可以使用DataSource池进行自动配置。下面是选取一个特定实现的算法：

* 由于Tomcat数据源连接池的性能和并发，在tomcat可用时，我们总是优先使用它。
* 如果HikariCP可用，我们将使用它。
* 如果Commons DBCP可用，我们将使用它，但在生产环境不推荐使用它。
* 最后，如果Commons DBCP2可用，我们将使用它。

如果你使用spring-boot-starter-jdbc或spring-boot-starter-data-jpa 'starter POMs'，你将会自动获取对tomcat-jdbc的依赖。

注：其他的连接池可以手动配置。如果你定义自己的DataSource bean，自动配置不会发生。

DataSource配置通过外部配置文件的spring.datasource.*属性控制。示例中，你可能会在application.properties中声明下面的片段：

	spring.datasource.url=jdbc:mysql://localhost/test
	spring.datasource.username=dbuser
	spring.datasource.password=dbpass
	spring.datasource.driver-class-name=com.mysql.jdbc.Driver

其他可选的配置可以查看[DataSourceProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/DataSourceProperties.java)。同时注意你可以通过spring.datasource.*配置任何DataSource实现相关的特定属性：具体参考你使用的连接池实现的文档。

注：既然Spring Boot能够从大多数数据库的url上推断出driver-class-name，那么你就不需要再指定它了。对于一个将要创建的DataSource连接池，我们需要能够验证Driver是否可用，所以我们会在做任何事情之前检查它。比如，如果你设置spring.datasource.driverClassName=com.mysql.jdbc.Driver，然后这个类就会被加载。

###### 4.7.1.3 连接到一个JNDI数据库
如果正在将Spring Boot应用部署到一个应用服务器，你可能想要用应用服务器内建的特性来配置和管理你的DataSource，并使用JNDI访问它。

spring.datasource.jndi-name属性可以用来替代spring.datasource.url，spring.datasource.username和spring.datasource.password去从一个特定的JNDI路径访问DataSource。比如，下面application.properties中的片段展示了如何获取JBoss定义的DataSource：

	spring.datasource.jndi-name=java:jboss/datasources/customers

##### 4.7.2 使用JdbcTemplate
Spring的JdbcTemplate和NamedParameterJdbcTemplate类是被自动配置的，你可以在自己的beans中通过@Autowire直接注入它们。

	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.jdbc.core.JdbcTemplate;
	import org.springframework.stereotype.Component;

	@Component
	public class MyBean {

	    private final JdbcTemplate jdbcTemplate;

	    @Autowired
	    public MyBean(JdbcTemplate jdbcTemplate) {
	        this.jdbcTemplate = jdbcTemplate;
	    }
	    // ...
	}

##### 4.7.3 JPA和Spring Data
Java持久化API是一个允许你将对象映射为关系数据库的标准技术。spring-boot-starter-data-jpa POM提供了一种快速上手的方式。它提供下列关键的依赖：

* Hibernate - 一个非常流行的JPA实现。
* Spring Data JPA - 让实现基于JPA的repositories更容易。
* Spring ORMs - Spring框架的核心ORM支持。

注：我们不想在这涉及太多关于JPA或Spring Data的细节。你可以参考来自[spring.io](http://spring.io/)的指南[使用JPA获取数据](http://spring.io/guides/gs/accessing-data-jpa/)，并阅读[Spring Data JPA](http://projects.spring.io/spring-data-jpa/)和[Hibernate](http://hibernate.org/orm/documentation/)的参考文档。

###### 4.7.3.1 实体类
传统上，JPA实体类被定义到一个persistence.xml文件中。在Spring Boot中，这个文件不是必需的，并被'实体扫描'替代。默认情况下，在你主（main）配置类（被@EnableAutoConfiguration或@SpringBootApplication注解的类）下的所有包都将被查找。

任何被@Entity，@Embeddable或@MappedSuperclass注解的类都将被考虑。一个普通的实体类看起来像下面这样：

	package com.example.myapp.domain;

	import java.io.Serializable;
	import javax.persistence.*;

	@Entity
	public class City implements Serializable {

    @Id
    @GeneratedValue
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(nullable = false)
    private String state;

    // ... additional members, often include @OneToMany mappings

    protected City() {
        // no-args constructor required by JPA spec
        // this one is protected since it shouldn't be used directly
    }

    public City(String name, String state) {
        this.name = name;
        this.country = country;
    }

    public String getName() {
        return this.name;
    }

    public String getState() {
        return this.state;
    }
    // ... etc
	}


注：你可以使用@EntityScan注解自定义实体扫描路径。具体参考[Section 67.4, “Separate @Entity definitions from Spring configuration”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/67.4.%20Separate%20@Entity%20definitions%20from%20Spring%20configuration.md)。

###### 4.7.3.2 Spring Data JPA仓库
Spring Data JPA仓库（repositories）是用来定义访问数据的接口。根据你的方法名，JPA查询会被自动创建。比如，一个CityRepository接口可能声明一个findAllByState(String state)方法，用来查找给定状态的所有城市。

对于比较复杂的查询，你可以使用Spring Data的Query来注解你的方法。

Spring Data仓库通常继承自Repository或CrudRepository接口。如果你使用自动配置，包括在你的主配置类（被@EnableAutoConfiguration或@SpringBootApplication注解的类）的包下的仓库将会被搜索。

下面是一个传统的Spring Data仓库：

	package com.example.myapp.domain;

	import org.springframework.data.domain.*;
	import org.springframework.data.repository.*;

	public interface CityRepository extends Repository<City, Long> {

	    Page<City> findAll(Pageable pageable);

	    City findByNameAndCountryAllIgnoringCase(String name, String country);
	}

注：我们仅仅触及了Spring Data JPA的表面。具体查看它的[参考指南](http://projects.spring.io/spring-data-jpa/)。

###### 4.7.3.2 创建和删除JPA数据库
默认情况下，只有在你使用内嵌数据库（H2, HSQL或Derby）时，JPA数据库才会被自动创建。你可以使用spring.jpa.*属性显示的设置JPA。比如，为了创建和删除表你可以将下面的配置添加到application.properties中：

	spring.jpa.hibernate.ddl-auto=create-drop

注：Hibernate自己内部对创建，删除表支持（如果你恰好记得这回事更好）的属性是hibernate.hbm2ddl.auto。使用spring.jpa.properties.*（前缀在被添加到实体管理器之前会被剥离掉），你可以设置Hibernate本身的属性，比如hibernate.hbm2ddl.auto。示例：`spring.jpa.properties.hibernate.globally_quoted_identifiers=true`将传递hibernate.globally_quoted_identifiers到Hibernate实体管理器。

默认情况下，DDL执行（或验证）被延迟到ApplicationContext启动。这也有一个spring.jpa.generate-ddl标识，如果Hibernate自动配置被激活，那该标识就不会被使用，因为ddl-auto设置粒度更细。

#### 4.8 使用NoSQL技术
Spring Data提供其他项目，用来帮你使用各种各样的NoSQL技术，包括MongoDB, Neo4J, Elasticsearch, Solr, Redis, Gemfire, Couchbase和Cassandra。Spring Boot为Redis, MongoDB, Elasticsearch, Solr和Gemfire提供自动配置。你可以充分利用其他项目，但你需要自己配置它们。具体查看projects.spring.io/spring-data中合适的参考文档。

##### 4.8.1 Redis
Redis是一个缓存，消息中间件及具有丰富特性的键值存储系统。Spring Boot为Jedis客户端库和由Spring Data Redis提供的基于Jedis客户端的抽象提供自动配置。spring-boot-starter-redis'Starter POM'为收集依赖提供一种便利的方式。

###### 4.8.1.1 连接Redis
你可以注入一个自动配置的RedisConnectionFactory，StringRedisTemplate或普通的跟其他Spring Bean相同的RedisTemplate实例。默认情况下，这个实例将尝试使用localhost:6379连接Redis服务器。

	@Component
	public class MyBean {

	    private StringRedisTemplate template;

	    @Autowired
	    public MyBean(StringRedisTemplate template) {
	        this.template = template;
	    }
	    // ...
	}

如果你添加一个你自己的任何自动配置类型的@Bean，它将替换默认的（除了RedisTemplate的情况，它是根据bean的名称'redisTemplate'而不是它的类型进行排除的）。如果在classpath路径下存在commons-pool2，默认你会获得一个连接池工厂。

##### 4.8.2 MONGODB
MongoDB是一个开源的NoSQL文档数据库，它使用一个JSON格式的模式（schema）替换了传统的基于表的关系数据。Spring Boot为使用MongoDB提供了很多便利，包括spring-boot-starter-data-mongodb'Starter POM'。

###### 4.8.2.1 连接MongoDB数据库
你可以注入一个自动配置的org.springframework.data.mongodb.MongoDbFactory来访问Mongo数据库。默认情况下，该实例将尝试使用URL：mongodb://localhost/test连接一个MongoDB服务器。

	import org.springframework.data.mongodb.MongoDbFactory;
	import com.mongodb.DB;

	@Component
	public class MyBean {

	    private final MongoDbFactory mongo;

	    @Autowired
	    public MyBean(MongoDbFactory mongo) {
	        this.mongo = mongo;
	    }

	    // ...
	    public void example() {
	        DB db = mongo.getDb();
	        // ...
	    }
	}
你可以通过设置spring.data.mongodb.uri来改变该url，或指定一个host/port。比如，你可能会在你的application.properties中设置如下的属性：

	spring.data.mongodb.host=mongoserver
	spring.data.mongodb.port=27017

注：如果没有指定spring.data.mongodb.port，那将使用默认的端口27017。你可以简单的从上面的示例中删除这一行。如果不使用Spring Data Mongo，你可以注入com.mongodb.Mongo beans而不是使用MongoDbFactory。

如果想全面控制MongoDB连接的建立，你也可以声明自己的MongoDbFactory或Mongo，@Beans。

###### 4.8.2.2 MongoDBTemplate
Spring Data Mongo提供了一个MongoTemplate类，它的设计和Spring的JdbcTemplate很相似。正如JdbcTemplate一样，Spring Boot会为你自动配置一个bean，你只需简单的注入它即可：

	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.data.mongodb.core.MongoTemplate;
	import org.springframework.stereotype.Component;

	@Component
	public class MyBean {

	    private final MongoTemplate mongoTemplate;

	    @Autowired
	    public MyBean(MongoTemplate mongoTemplate) {
	        this.mongoTemplate = mongoTemplate;
	    }
	    // ...
	}
具体参考MongoOperations Javadoc。

###### 4.8.1.3 Spring Data MongoDB仓库
Spring Data的仓库包括对MongoDB的支持。正如上面讨论的JPA仓库，基本的原则是查询会自动基于你的方法名创建。

实际上，不管是Spring Data JPA还是Spring Data MongoDB都共享相同的基础设施。所以你可以使用上面的JPA示例，并假设那个City现在是一个Mongo数据类而不是JPA　@Entity，它将以同样的方式工作。

	package com.example.myapp.domain;

	import org.springframework.data.domain.*;
	import org.springframework.data.repository.*;

	public interface CityRepository extends Repository<City, Long> {

	    Page<City> findAll(Pageable pageable);

	    City findByNameAndCountryAllIgnoringCase(String name, String country);

	}

##### 4.8.3 Gemfire
Spring Data Gemfire为使用Pivotal Gemfire数据管理平台提供了方便的，Spring友好的工具。Spring Boot提供了一个用于聚集依赖的spring-boot-starter-data-gemfire'Starter POM'。目前不支持Gemfire的自动配置，但你可以使用一个单一的注解使Spring Data仓库支持它。

##### 4.8.4 Solr
Apache Solr是一个搜索引擎。Spring Boot为solr客户端库及Spring Data Solr提供的基于solr客户端库的抽象提供了基本的配置。Spring Boot提供了一个用于聚集依赖的spring-boot-starter-data-solr'Starter POM'。

###### 4.8.4.1 连接Solr
你可以像其他Spring beans一样注入一个自动配置的SolrServer实例。默认情况下，该实例将尝试使用localhost:8983/solr连接一个服务器。

	@Component
	public class MyBean {

	    private SolrServer solr;

	    @Autowired
	    public MyBean(SolrServer solr) {
	        this.solr = solr;
	    }
	    // ...
	}
如果你添加一个自己的SolrServer类型的@Bean，它将会替换默认的。

###### 4.8.4.2 Spring Data Solr仓库
Spring Data的仓库包括了对Apache Solr的支持。正如上面讨论的JPA仓库，基本的原则是查询会自动基于你的方法名创建。

实际上，不管是Spring Data JPA还是Spring Data Solr都共享相同的基础设施。所以你可以使用上面的JPA示例，并假设那个City现在是一个@SolrDocument类而不是JPA　@Entity，它将以同样的方式工作。

注：具体参考[Spring Data Solr](http://projects.spring.io/spring-data-solr/)文档。

##### 4.8.5 Elasticsearch
[Elastic Search](http://www.elasticsearch.org/)是一个开源的，分布式，实时搜索和分析引擎。Spring Boot为Elasticsearch及Spring Data Elasticsearch提供的基于它的抽象提供了基本的配置。[Spring Boot](https://github.com/spring-projects/spring-data-elasticsearch)提供了一个用于聚集依赖的spring-boot-starter-data-elasticsearch'Starter POM'。

###### 4.8.5.1 连接Elasticsearch
你可以像其他Spring beans那样注入一个自动配置的ElasticsearchTemplate或Elasticsearch客户端实例。默认情况下，该实例将尝试连接到一个本地内存服务器（在Elasticsearch项目中的一个NodeClient），但你可以通过设置spring.data.elasticsearch.clusterNodes为一个以逗号分割的host:port列表来将其切换到一个远程服务器（比如，TransportClient）。

	@Component
	public class MyBean {

	    private ElasticsearchTemplate template;

	    @Autowired
	    public MyBean(ElasticsearchTemplate template) {
	        this.template = template;
	    }
	    // ...
	}
如果你添加一个你自己的ElasticsearchTemplate类型的@Bean，它将替换默认的。

###### 4.8.5.2 Spring Data Elasticseach仓库
Spring Data的仓库包括了对Elasticsearch的支持。正如上面讨论的JPA仓库，基本的原则是查询会自动基于你的方法名创建。

实际上，不管是Spring Data JPA还是Spring Data　Elasticsearch都共享相同的基础设施。所以你可以使用上面的JPA示例，并假设那个City现在是一个Elasticsearch @Document类而不是JPA　@Entity，它将以同样的方式工作。

注：具体参考[Spring Data Elasticsearch](http://docs.spring.io/spring-data/elasticsearch/docs/)文档。

#### 4.9 消息
Spring Framework框架为集成消息系统提供了扩展（extensive）支持：从使用JmsTemplate简化JMS　API，到实现一个完整异步消息接收的底层设施。

Spring AMQP提供一个相似的用于'高级消息队列协议'的特征集，并且Spring Boot也为RabbitTemplate和RabbitMQ提供了自动配置选项。

Spring Websocket提供原生的STOMP消息支持，并且Spring Boot通过starters和一些自动配置也提供了对它的支持。

##### 4.9.1 JMS
javax.jms.ConnectionFactory接口提供了一个标准的用于创建一个javax.jms.Connection的方法，javax.jms.Connection用于和JMS代理（broker）交互。

尽管为了使用JMS，Spring需要一个ConnectionFactory，但通常你不需要直接使用它，而是依赖于上层消息抽象（具体参考Spring框架的[相关章节](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#jms)）。Spring Boot也会自动配置发送和接收消息需要的设施（infrastructure）。

###### 4.9.1.1 HornetQ支持
如果在classpath下发现HornetQ，Spring Boot会自动配置ConnectionFactory。如果需要代理，将会开启一个内嵌的，已经自动配置好的代理（除非显式设置mode属性）。支持的modes有：embedded（显式声明使用一个内嵌的代理，如果该代理在classpath下不可用将导致一个错误），native（使用netty传输协议连接代理）。当后者被配置，Spring Boot配置一个连接到一个代理的ConnectionFactory，该代理运行在使用默认配置的本地机器上。

注：如果使用spring-boot-starter-hornetq，连接到一个已存在的HornetQ实例所需的依赖都会被提供，同时还有用于集成JMS的Spring基础设施。将org.hornetq:hornetq-jms-server添加到你的应用中，你就可以使用embedded模式。

HornetQ配置被spring.hornetq.*中的外部配置属性所控制。例如，你可能在application.properties声明以下片段：

	spring.hornetq.mode=native
	spring.hornetq.host=192.168.1.210
	spring.hornetq.port=9876
当内嵌代理时，你可以选择是否启用持久化，并且列表中的目标都应该是可用的。这些可以通过一个以逗号分割的列表来指定一些默认的配置项，或定义org.hornetq.jms.server.config.JMSQueueConfiguration或org.hornetq.jms.server.config.TopicConfiguration类型的bean(s)来配置更高级的队列和主题。具体参考[HornetQProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/hornetq/HornetQProperties.java)。

没有涉及JNDI查找，目标是通过名字解析的，名字即可以使用HornetQ配置中的name属性，也可以是配置中提供的names。

###### 4.9.1.2 ActiveQ支持
如果发现ActiveMQ在classpath下可用，Spring Boot会配置一个ConnectionFactory。如果需要代理，将会开启一个内嵌的，已经自动配置好的代理（只要配置中没有指定代理URL）。

ActiveMQ配置是通过spring.activemq.*中的外部配置来控制的。例如，你可能在application.properties中声明下面的片段：

	spring.activemq.broker-url=tcp://192.168.1.210:9876
	spring.activemq.user=admin
	spring.activemq.password=secret
具体参考[ActiveMQProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/activemq/ActiveMQProperties.java)。

默认情况下，如果目标还不存在，ActiveMQ将创建一个，所以目标是通过它们提供的名称解析出来的。

###### 4.9.1.3 使用JNDI ConnectionFactory
如果你在一个应用服务器中运行你的应用，Spring Boot将尝试使用JNDI定位一个JMS ConnectionFactory。默认情况会检查java:/JmsXA和java:/ XAConnectionFactory。如果需要的话，你可以使用spring.jms.jndi-name属性来指定一个替代位置。

	spring.jms.jndi-name=java:/MyConnectionFactory

###### 4.9.1.4 发送消息
Spring的JmsTemplate会被自动配置，你可以将它直接注入到你自己的beans中：

	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.jms.core.JmsTemplate;
	import org.springframework.stereotype.Component;
	@Component
	public class MyBean {
	private final JmsTemplate jmsTemplate;
	@Autowired
	public MyBean(JmsTemplate jmsTemplate) {
	this.jmsTemplate = jmsTemplate;
	}
	// ...
	}
注：[JmsMessagingTemplate](http://docs.spring.io/spring/docs/4.1.4.RELEASE/javadoc-api/org/springframework/jms/core/JmsMessagingTemplate.html)(Spring4.1新增的)也可以使用相同的方式注入

###### 4.9.1.5 接收消息
当JMS基础设施能够使用时，任何bean都能够被@JmsListener注解，以创建一个监听者端点。如果没有定义JmsListenerContainerFactory，一个默认的将会被自动配置。下面的组件在someQueue目标上创建一个监听者端点。

	@Component
	public class MyBean {
		@JmsListener(destination = "someQueue")
		public void processMessage(String content) {
		// ...
		}
	}
具体查看[@EnableJms javadoc](http://docs.spring.io/spring/docs/4.1.4.RELEASE/javadoc-api/org/springframework/jms/annotation/EnableJms.html)。

#### 4.10 发送邮件
Spring框架使用JavaMailSender接口为发送邮件提供了一个简单的抽象，并且Spring Boot也为它提供了自动配置和一个starter模块。 具体查看[JavaMailSender参考文档](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#mail)。

如果spring.mail.host和相关的库（通过spring-boot-starter-mail定义）都存在，一个默认的JavaMailSender将被创建。该sender可以通过spring.mail命名空间下的配置项进一步自定义，具体参考[MailProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/mail/MailProperties.java)。

#### 4.11 使用JTA处理分布式事务
Spring Boot使用一个[Atomkos](http://www.atomikos.com/)或[Bitronix](http://docs.codehaus.org/display/BTM/Home)的内嵌事务管理器来支持跨多个XA资源的分布式JTA事务。当部署到一个恰当的J2EE应用服务器时也会支持JTA事务。

当发现一个JTA环境时，Spring Boot将使用Spring的JtaTransactionManager来管理事务。自动配置的JMS，DataSource和JPA　beans将被升级以支持XA事务。你可以使用标准的Spring idioms，比如@Transactional，来参与到一个分布式事务中。如果你处于JTA环境里，但仍旧想使用本地事务，你可以将spring.jta.enabled属性设置为false来禁用JTA自动配置功能。

##### 4.11.1 使用一个Atomikos事务管理器
Atomikos是一个非常流行的开源事务管理器，它可以嵌入到你的Spring Boot应用中。你可以使用`spring-boot-starter-jta-atomikosStarter` POM去获取正确的Atomikos库。Spring Boot会自动配置Atomikos，并将合适的depends-on应用到你的Spring Beans上，确保它们以正确的顺序启动和关闭。

默认情况下，Atomikos事务日志将被记录在应用home目录（你的应用jar文件放置的目录）下的transaction-logs文件夹中。你可以在application.properties文件中通过设置spring.jta.log-dir属性来自定义该目录。以spring.jta.开头的属性能用来自定义Atomikos的UserTransactionServiceIml实现。具体参考[AtomikosProperties javadoc](http://docs.spring.io/spring-boot/docs/1.2.2.BUILD-SNAPSHOT/api/org/springframework/boot/jta/atomikos/AtomikosProperties.html)。

注：为了确保多个事务管理器能够安全地和相应的资源管理器配合，每个Atomikos实例必须设置一个唯一的ID。默认情况下，该ID是Atomikos实例运行的机器上的IP地址。为了确保生产环境中该ID的唯一性，你需要为应用的每个实例设置不同的spring.jta.transaction-manager-id属性值。

##### 4.11.2 使用一个Bitronix事务管理器
Bitronix是另一个流行的开源JTA事务管理器实现。你可以使用spring-boot-starter-jta-bitronixstarter POM为项目添加合适的Birtronix依赖。和Atomikos类似，Spring Boot将自动配置Bitronix，并对beans进行后处理（post-process）以确保它们以正确的顺序启动和关闭。

默认情况下，Bitronix事务日志将被记录到应用home目录下的transaction-logs文件夹中。通过设置spring.jta.log-dir属性，你可以自定义该目录。以spring.jta.开头的属性将被绑定到bitronix.tm.Configuration　bean，你可以通过这完成进一步的自定义。具体参考[Bitronix文档](http://btm.codehaus.org/api/2.0.1/bitronix/tm/Configuration.html)。

注：为了确保多个事务管理器能够安全地和相应的资源管理器配合，每个Bitronix实例必须设置一个唯一的ID。默认情况下，该ID是Bitronix实例运行的机器上的IP地址。为了确保生产环境中该ID的唯一性，你需要为应用的每个实例设置不同的spring.jta.transaction-manager-id属性值。

##### 4.11.3 使用一个J2EE管理的事务管理器
如果你将Spring Boot应用打包为一个war或ear文件，并将它部署到一个J2EE的应用服务器中，那你就能使用应用服务器内建的事务管理器。Spring Boot将尝试通过查找常见的JNDI路径（java:comp/UserTransaction, java:comp/TransactionManager等）来自动配置一个事务管理器。如果使用应用服务器提供的事务服务，你通常需要确保所有的资源都被应用服务器管理，并通过JNDI暴露出去。Spring Boot通过查找JNDI路径java:/JmsXA或java:/XAConnectionFactory获取一个ConnectionFactory来自动配置JMS，并且你可以使用spring.datasource.jndi-name属性配置你的DataSource。

#### 4.12 Spring集成
Spring集成提供基于消息和其他协议的，比如HTTP，TCP等的抽象。如果Spring集成在classpath下可用，它将会通过@EnableIntegration注解被初始化。如果classpath下'spring-integration-jmx'可用，则消息处理统计分析将被通过JMX发布出去。具体参考[IntegrationAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationAutoConfiguration.java)类。

#### 4.13 基于JMX的监控和管理
Java管理扩展（JMX）提供了一个标准的用于监控和管理应用的机制。默认情况下，Spring Boot将创建一个id为‘mbeanServer’的MBeanServer，并导出任何被Spring JMX注解（@ManagedResource,@ManagedAttribute,@ManagedOperation）的beans。具体参考[JmxAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jmx/JmxAutoConfiguration.java)类。

#### 4.14 测试
Spring Boot提供很多有用的测试应用的工具。spring-boot-starter-test POM提供Spring Test，JUnit，Hamcrest和Mockito的依赖。在spring-boot核心模块org.springframework.boot.test包下也有很多有用的测试工具。

##### 4.14.1 测试作用域依赖
如果使用spring-boot-starter-test ‘Starter POM’（在test作用域内），你将发现下列被提供的库：

* Spring Test - 对Spring应用的集成测试支持
* JUnit - 事实上的(de-facto)标准，用于Java应用的单元测试。
* Hamcrest - 一个匹配对象的库（也称为约束或前置条件），它允许assertThat等JUnit类型的断言。
* Mockito - 一个Java模拟框架。

这也有一些我们写测试用例时经常用到的库。如果它们不能满足你的要求，你可以随意添加其他的测试用的依赖库。

##### 4.14.2 测试Spring应用

依赖注入最大的优点就是它能够让你的代码更容易进行单元测试。你只需简单的通过new操作符实例化对象，而不需要涉及Spring。你也可以使用模拟对象替换真正的依赖。

你常常需要在进行单元测试后，开始集成测试（在这个过程中只需要涉及到Spring的ApplicationContext）。在执行集成测试时，不需要部署应用或连接到其他基础设施是非常有用的。

Spring框架包含一个dedicated测试模块，用于这样的集成测试。你可以直接声明对org.springframework:spring-test的依赖，或使用spring-boot-starter-test ‘Starter POM’以透明的方式拉取它。

如果你以前没有使用过spring-test模块，可以查看Spring框架参考文档中的[相关章节](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#testing)。

##### 4.14.3 测试Spring Boot应用
一个Spring Boot应用只是一个Spring ApplicationContext，所以在测试它时除了正常情况下处理一个vanilla Spring　context外不需要做其他特别事情。唯一需要注意的是，如果你使用SpringApplication创建上下文，外部配置，日志和Spring Boot的其他特性只会在默认的上下文中起作用。

Spring Boot提供一个@SpringApplicationConfiguration注解用来替换标准的spring-test　@ContextConfiguration注解。如果使用@SpringApplicationConfiguration来设置你的测试中使用的ApplicationContext，它最终将通过SpringApplication创建，并且你将获取到Spring Boot的其他特性。

示例如下：

	@RunWith(SpringJUnit4ClassRunner.class)
	@SpringApplicationConfiguration(classes = SampleDataJpaApplication.class)
	public class CityRepositoryIntegrationTests {
	@Autowired
	CityRepository repository;
	// ...
	}
提示：上下文加载器会通过查找@WebIntegrationTest或@WebAppConfiguration注解来猜测你想测试的是否是web应用（例如，是否使用MockMVC，MockMVC和@WebAppConfiguration是spring-test的一部分）。

如果想让一个web应用启动，并监听它的正常的端口，你可以使用HTTP来测试它（比如，使用RestTemplate），并使用@WebIntegrationTest注解你的测试类（或它的一个父类）。这很有用，因为它意味着你可以对你的应用进行全栈测试，但在一次HTTP交互后，你需要在你的测试类中注入相应的组件并使用它们断言应用的内部状态。

示例：

	@RunWith(SpringJUnit4ClassRunner.class)
	@SpringApplicationConfiguration(classes = SampleDataJpaApplication.class)
	@WebIntegrationTest
	public class CityRepositoryIntegrationTests {
	@Autowired
	CityRepository repository;
	RestTemplate restTemplate = new TestRestTemplate();
	// ... interact with the running server
	}
注：Spring测试框架在每次测试时会缓存应用上下文。因此，只要你的测试共享相同的配置，不管你实际运行多少测试，开启和停止服务器只会发生一次。

你可以为@WebIntegrationTest添加环境变量属性来改变应用服务器端口号，比如@WebIntegrationTest("server.port:9000")。此外，你可以将server.port和management.port属性设置为０来让你的集成测试使用随机的端口号，例如：

	@RunWith(SpringJUnit4ClassRunner.class)
	@SpringApplicationConfiguration(classes = MyApplication.class)
	@WebIntegrationTest({"server.port=0", "management.port=0"})
	public class SomeIntegrationTests {
	// ...
	}
可以查看[Section 64.4, “Discover the HTTP port at runtime”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/64.4.%20Discover%20the%20HTTP%20port%20at%20runtime.md)，它描述了如何在测试期间发现分配的实际端口。

###### 4.14.3.1 使用Spock测试Spring Boot应用
如果期望使用Spock测试一个Spring Boot应用，你应该将Spock的spock-spring模块依赖添加到应用的构建中。spock-spring将Spring的测试框架集成到了Spock里。

注意你不能使用上述提到的@SpringApplicationConfiguration注解，因为[Spock找不到@ContextConfiguration元注解](https://code.google.com/p/spock/issues/detail?id=349)。为了绕过该限制，你应该直接使用@ContextConfiguration注解，并使用Spring Boot特定的上下文加载器来配置它。

	@ContextConfiguration(loader = SpringApplicationContextLoader.class)
	class ExampleSpec extends Specification {
	// ...
	}
注：上面描述的注解在Spock中可以使用，比如，你可以使用@WebIntegrationTest注解你的Specification以满足测试需要。

##### 4.14.4 测试工具
打包进spring-boot的一些有用的测试工具类。

###### 4.14.4.1 ConfigFileApplicationContextInitializer
ConfigFileApplicationContextInitializer是一个ApplicationContextInitializer，可以用来测试加载Spring Boot的application.properties文件。当不需要使用@SpringApplicationConfiguration提供的全部特性时，你可以使用它。

	@ContextConfiguration(classes = Config.class,initializers = ConfigFileApplicationContextInitializer.class)

###### 4.14.4.2 EnvironmentTestUtils
EnvironmentTestUtils允许你快速添加属性到一个ConfigurableEnvironment或ConfigurableApplicationContext。只需简单的使用key=value字符串调用它： ```java EnvironmentTestUtils.addEnvironment(env, "org=Spring", "name=Boot");

###### 4.14.4.3 OutputCapture
OutputCapture是一个JUnit Rule，用于捕获System.out和System.err输出。只需简单的将捕获声明为一个@Rule，并使用toString()断言：

	import org.junit.Rule;
	import org.junit.Test;
	import org.springframework.boot.test.OutputCapture;
	import static org.hamcrest.Matchers.*;
	import static org.junit.Assert.*;

	public class MyTest {
	@Rule
	public OutputCapture capture = new OutputCapture();
	@Test
	public void testName() throws Exception {
	System.out.println("Hello World!");
	assertThat(capture.toString(), containsString("World"));
	}
	}

###### 4.14.4.4 TestRestTemplate
TestRestTemplate是一个方便进行集成测试的Spring RestTemplate子类。你会获取到一个普通的模板或一个发送基本HTTP认证（使用用户名和密码）的模板。在任何情况下，这些模板都表现出对测试友好：不允许重定向（这样你可以对响应地址进行断言），忽略cookies（这样模板就是无状态的），对于服务端错误不会抛出异常。推荐使用Apache HTTP Client(4.3.2或更好的版本)，但不强制这样做。如果在classpath下存在Apache HTTP Client，TestRestTemplate将以正确配置的client进行响应。

	public class MyTest {
	RestTemplate template = new TestRestTemplate();
	@Test
	public void testRequest() throws Exception {
	HttpHeaders headers = template.getForEntity("http://myhost.com", String.class).getHeaders();
	assertThat(headers.getLocation().toString(), containsString("myotherhost"));
	}
	}

#### 4.15 开发自动配置和使用条件
如果你在一个开发者共享库的公司工作，或你在从事一个开源或商业型的库，你可能想要开发自己的auto-configuration。Auto-configuration类能够在外部的jars中绑定，并仍能被Spring Boot发现。

##### 4.15.1 理解auto-configured beans
从底层来讲，auto-configured是使用标准的@Configuration实现的类，另外的@Conditional注解用来约束在什么情况下使用auto-configuration。通常auto-configuration类使用@ConditionalOnClass和@ConditionalOnMissingBean注解。这是为了确保只有在相关的类被发现，和你没有声明自己的@Configuration时才应用auto-configuration。

你可以浏览spring-boot-autoconfigure的源码，查看我们提供的@Configuration类（查看META-INF/spring.factories文件）。

##### 4.15.2 定位auto-configuration候选者
Spring Boot会检查你发布的jar中是否存在META-INF/spring.factories文件。该文件应该列出以EnableAutoConfiguration为key的配置类：

	org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
	com.mycorp.libx.autoconfigure.LibXAutoConfiguration,\
	com.mycorp.libx.autoconfigure.LibXWebAutoConfiguration
如果配置需要应用特定的顺序，你可以使用[@AutoConfigureAfter](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureAfter.java)或[@AutoConfigureBefore](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureBefore.java)注解。例如，你想提供web-specific配置，你的类就需要应用在WebMvcAutoConfiguration后面。

##### 4.15.3 Condition注解
你几乎总是需要在你的auto-configuration类里添加一个或更多的@Condition注解。@ConditionalOnMissingBean注解是一个常见的示例，它经常用于允许开发者覆盖auto-configuration，如果他们不喜欢你提供的默认行为。

Spring Boot包含很多@Conditional注解，你可以在自己的代码中通过注解@Configuration类或单独的@Bean方法来重用它们。

###### 4.15.3.1 Class条件
@ConditionalOnClass和@ConditionalOnMissingClass注解允许根据特定类是否出现来跳过配置。由于注解元数据是使用[ASM](http://asm.ow2.org/)来解析的，你实际上可以使用value属性来引用真正的类，即使该类可能实际上并没有出现在运行应用的classpath下。如果你倾向于使用一个String值来指定类名，你也可以使用name属性。

###### 4.15.3.2 Bean条件
@ConditionalOnBean和@ConditionalOnMissingBean注解允许根据特定beans是否出现来跳过配置。你可以使用value属性来指定beans（by type），也可以使用name来指定beans（by name）。search属性允许你限制搜索beans时需要考虑的ApplicationContext的层次。

注：当@Configuration类被解析时@Conditional注解会被处理。Auto-configure @Configuration总是最后被解析（在所有用户定义beans后面），然而，如果你将那些注解用到常规的@Configuration类，需要注意不能引用那些还没有创建好的bean定义。

###### 4.15.3.3 Property条件
@ConditionalOnProperty注解允许根据一个Spring Environment属性来决定是否包含配置。可以使用prefix和name属性指定要检查的配置属性。默认情况下，任何存在的只要不是false的属性都会匹配。你也可以使用havingValue和matchIfMissing属性创建更高级的检测。

###### 4.15.3.4 Resource条件
@ConditionalOnResource注解允许只有在特定资源出现时配置才会被包含。资源可以使用常见的Spring约定命名，例如file:/home/user/test.dat。

###### 4.15.3.5 Web Application条件
@ConditionalOnWebApplication和@ConditionalOnNotWebApplication注解允许根据应用是否为一个'web应用'来决定是否包含配置。一个web应用是任何使用Spring WebApplicationContext，定义一个session作用域或有一个StandardServletEnvironment的应用。

###### 4.15.3.6 SpEL表达式条件
@ConditionalOnExpression注解允许根据[SpEL表达式](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#expressions)结果来跳过配置。

#### 4.16 WebSockets
Spring Boot为内嵌的Tomcat(8和7)，Jetty 9和Undertow提供WebSockets自动配置。如果你正在将一个war包部署到一个单独的容器，Spring Boot会假设该容器会对它的WebSocket支持相关的配置负责。

Spring框架提供丰富的[WebSocket支持，通](http://docs.spring.io/spring/docs/4.1.4.RELEASE/spring-framework-reference/htmlsingle/#websocket)过spring-boot-starter-websocket模块可以轻易获取到。

### Spring Boot执行器：Production-ready特性
Spring Boot包含很多其他的特性，它们可以帮你监控和管理发布到生产环境的应用。你可以选择使用HTTP端点，JMX或远程shell（SSH或Telnet）来管理和监控应用。审计（Auditing），健康（health）和数据采集（metrics gathering）会自动应用到你的应用。

#### 5.1 开启production-ready特性
[spring-boot-actuator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator)模块提供了Spring Boot所有的production-ready特性。启用该特性的最简单方式就是添加对spring-boot-starter-actuator ‘Starter POM’的依赖。

执行器（Actuator）的定义：执行器是一个制造业术语，指的是用于移动或控制东西的一个机械装置。一个很小的改变就能让执行器产生大量的运动。

基于Maven的项目想要添加执行器只需添加下面的'starter'依赖：

	<dependencies>
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-actuator</artifactId>
	    </dependency>
	</dependencies>
对于Gradle，使用下面的声明：

	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-actuator")
	}

#### 5.2 端点
执行器端点允许你监控应用及与应用进行交互。Spring Boot包含很多内置的端点，你也可以添加自己的。例如，health端点提供了应用的基本健康信息。

端点暴露的方式取决于你采用的技术类型。大部分应用选择HTTP监控，端点的ID映射到一个URL。例如，默认情况下，health端点将被映射到/health。

下面的端点都是可用的：

|ID					|描述　|			敏感（Sensitive）|
|:--|:--|:--|
|autoconfig	|		显示一个auto-configuration的报告，该报告展示所有auto-configuration候选者及它们被应用或未被应用的原因	|true|
|beans		|显示一个应用中所有Spring Beans的完整列表						|true|
|configprops|		显示一个所有@ConfigurationProperties的整理列表				|	true|
|dump	|	执行一个线程转储								|true|
|env	|	暴露来自Spring　ConfigurableEnvironment的属性	|								true|
|health	|	展示应用的健康信息（当使用一个未认证连接访问时显示一个简单的'status'，使用认证连接访问则显示全部信息详情）	|false|
|info	|		显示任意的应用信息					|false|
|metrics|		展示当前应用的'指标'信息			|true|
|mappings|		显示一个所有@RequestMapping路径的整理列表	|		true|
|shutdown|		允许应用以优雅的方式关闭（默认情况下不启用）	|true|
|trace|		显示trace信息（默认为最新的一些HTTP请求）		|	true|

注：根据一个端点暴露的方式，sensitive参数可能会被用做一个安全提示。例如，在使用HTTP访问sensitive端点时需要提供用户名/密码（如果没有启用web安全，可能会简化为禁止访问该端点）。

##### 5.2.1 自定义端点
使用Spring属性可以自定义端点。你可以设置端点是否开启（enabled），是否敏感（sensitive），甚至它的id。例如，下面的application.properties改变了敏感性和beans端点的id，也启用了shutdown。

	endpoints.beans.id=springbeans
	endpoints.beans.sensitive=false
	endpoints.shutdown.enabled=true
注：前缀endpoints + . + name被用来唯一的标识被配置的端点。

默认情况下，除了shutdown外的所有端点都是启用的。如果希望指定选择端点的启用，你可以使用endpoints.enabled属性。例如，下面的配置禁用了除info外的所有端点：

	endpoints.enabled=false
	endpoints.info.enabled=true

##### 5.2.2 健康信息
健康信息可以用来检查应用的运行状态。它经常被监控软件用来提醒人们生产系统是否停止。health端点暴露的默认信息取决于端点是如何被访问的。对于一个非安全，未认证的连接只返回一个简单的'status'信息。对于一个安全或认证过的连接其他详细信息也会展示（具体参考[Section 41.6, “HTTP Health endpoint access restrictions”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/V.%20Spring%20Boot%20Actuator/41.6.%20HTTP%20Health%20endpoint%20access%20restrictions.md) ）。

健康信息是从你的ApplicationContext中定义的所有[HealthIndicator ](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java)beans收集过来的。Spring Boot包含很多auto-configured的HealthIndicators，你也可以写自己的。

##### 5.2.3 安全与HealthIndicators
HealthIndicators返回的信息常常性质上有点敏感。例如，你可能不想将数据库服务器的详情发布到外面。因此，在使用一个未认证的HTTP连接时，默认只会暴露健康状态（health status）。如果想将所有的健康信息暴露出去，你可以把endpoints.health.sensitive设置为false。

为防止'拒绝服务'攻击，Health响应会被缓存。你可以使用endpoints.health.time-to-live属性改变默认的缓存时间（1000毫秒）。

###### 5.2.3.1 自动配置的HealthIndicators
下面的HealthIndicators会被Spring Boot自动配置（在合适的时候）：

|名称	|描述|
|:--|:--|
|[DiskSpaceHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/DiskSpaceHealthIndicator.java)	|低磁盘空间检测|
|[DataSourceHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/DataSourceHealthIndicator.java)	|检查是否能从DataSource获取连接|
|[MongoHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/MongoHealthIndicator.java)	|检查一个Mongo数据库是否可用（up）|
|[RabbitHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/RabbitHealthIndicator.java)	|检查一个Rabbit服务器是否可用（up）|
|[RedisHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/RedisHealthIndicator.java)	|检查一个Redis服务器是否可用（up）|
|[SolrHealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/SolrHealthIndicator.java)	|检查一个Solr服务器是否可用（up）|

###### 5.2.3.2 编写自定义HealthIndicators
想提供自定义健康信息，你可以注册实现了[HealthIndicator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java)接口的Spring beans。你需要提供一个health()方法的实现，并返回一个Health响应。Health响应需要包含一个status和可选的用于展示的详情。

	import org.springframework.boot.actuate.health.HealthIndicator;
	import org.springframework.stereotype.Component;

	@Component
	public class MyHealth implements HealthIndicator {

	    @Override
	    public Health health() {
	        int errorCode = check(); // perform some specific health check
	        if (errorCode != 0) {
	            return Health.down().withDetail("Error Code", errorCode).build();
	        }
	        return Health.up().build();
	    }

	}
除了Spring Boot预定义的[Status](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/Status.java)类型，Health也可以返回一个代表新的系统状态的自定义Status。在这种情况下，需要提供一个[HealthAggregator](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthAggregator.java)接口的自定义实现，或使用management.health.status.order属性配置默认的实现。

例如，假设一个新的，代码为FATAL的Status被用于你的一个HealthIndicator实现中。为了配置严重程度，你需要将下面的配置添加到application属性文件中：

	management.health.status.order: DOWN, OUT_OF_SERVICE, UNKNOWN, UP
如果使用HTTP访问health端点，你可能想要注册自定义的status，并使用HealthMvcEndpoint进行映射。例如，你可以将FATAL映射为HttpStatus.SERVICE_UNAVAILABLE。

##### 5.2.4 自定义应用info信息
通过设置Spring属性info.*，你可以定义info端点暴露的数据。所有在info关键字下的Environment属性都将被自动暴露。例如，你可以将下面的配置添加到application.properties：

	info.app.name=MyService
	info.app.description=My awesome service
	info.app.version=1.0.0

###### 5.2.4.1 在构建时期自动扩展info属性
你可以使用已经存在的构建配置自动扩展info属性，而不是对在项目构建配置中存在的属性进行硬编码。这在Maven和Gradle都是可能的。

**使用Maven自动扩展属性**

对于Maven项目，你可以使用资源过滤来自动扩展info属性。如果使用spring-boot-starter-parent，你可以通过@..@占位符引用Maven的'project properties'。

	project.artifactId=myproject
	project.name=Demo
	project.version=X.X.X.X
	project.description=Demo project for info endpoint
	info.build.artifact=@project.artifactId@
	info.build.name=@project.name@
	info.build.description=@project.description@
	info.build.version=@project.version@
注：在上面的示例中，我们使用project.*来设置一些值以防止由于某些原因Maven的资源过滤没有开启。Maven目标spring-boot:run直接将src/main/resources添加到classpath下（出于热加载的目的）。这就绕过了资源过滤和自动扩展属性的特性。你可以使用exec:java替换该目标或自定义插件的配置，具体参考plugin usage page。

如果你不使用starter parent，在你的pom.xml你需要添加（处于元素内）：

	<resources>
	    <resource>
	        <directory>src/main/resources</directory>
	        <filtering>true</filtering>
	    </resource>
	</resources>
和（处于内）：

	<plugin>
	    <groupId>org.apache.maven.plugins</groupId>
	    <artifactId>maven-resources-plugin</artifactId>
	    <version>2.6</version>
	    <configuration>
	        <delimiters>
	            <delimiter>@</delimiter>
	        </delimiters>
	    </configuration>
	</plugin>
**使用Gradle自动扩展属性**

通过配置Java插件的processResources任务，你也可以自动使用来自Gradle项目的属性扩展info属性。

	processResources {
	    expand(project.properties)
	}
然后你可以通过占位符引用Gradle项目的属性：

	info.build.name=${name}
	info.build.description=${description}
	info.build.version=${version}

###### 5.2.4.2 Git提交信息
info端点的另一个有用特性是，当项目构建完成后，它可以发布关于你的git源码仓库状态的信息。如果在你的jar中包含一个git.properties文件，git.branch和git.commit属性将被加载。

对于Maven用户，spring-boot-starter-parent POM包含一个能够产生git.properties文件的预配置插件。只需要简单的将下面的声明添加到你的POM中：

	<build>
	    <plugins>
	        <plugin>
	            <groupId>pl.project13.maven</groupId>
	            <artifactId>git-commit-id-plugin</artifactId>
	        </plugin>
	    </plugins>
	</build>
对于Gradle用户可以使用一个相似的插件gradle-git，尽管为了产生属性文件可能需要稍微多点工作。

#### 5.3 基于HTTP的监控和管理
如果你正在开发一个Spring MVC应用，Spring Boot执行器自动将所有启用的端点通过HTTP暴露出去。默认约定使用端点的id作为URL路径，例如，health暴露为/health。

##### 5.3.1 保护敏感端点
如果你的项目中添加的有Spring Security，所有通过HTTP暴露的敏感端点都会受到保护。默认情况下会使用基本认证（basic authentication，用户名为user，密码为应用启动时在控制台打印的密码）。

你可以使用Spring属性改变用户名，密码和访问端点需要的安全角色。例如，你可能会在application.properties中添加下列配置：

	security.user.name=admin
	security.user.password=secret
	management.security.role=SUPERUSER

注：如果你不使用Spring Security，那你的HTTP端点就被公开暴露，你应该慎重考虑启用哪些端点。具体参考[Section 40.1, “Customizing endpoints”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/V.%20Spring%20Boot%20Actuator/40.1.%20Customizing%20endpoints.md)。

##### 5.3.2 自定义管理服务器的上下文路径
有时候将所有的管理端口划分到一个路径下是有用的。例如，你的应用可能已经将/info作为他用。你可以用management.contextPath属性为管理端口设置一个前缀：

	management.context-path=/manage
上面的application.properties示例将把端口从/{id}改为/manage/{id}（比如，/manage/info）。

##### 5.3.3 自定义管理服务器的端口
对于基于云的部署，使用默认的HTTP端口暴露管理端点（endpoints）是明智的选择。然而，如果你的应用是在自己的数据中心运行，那你可能倾向于使用一个不同的HTTP端口来暴露端点。

management.port属性可以用来改变HTTP端口：

	management.port=8081
由于你的管理端口经常被防火墙保护，不对外暴露也就不需要保护管理端点，即使你的主要应用是安全的。在这种情况下，classpath下会存在Spring Security库，你可以设置下面的属性来禁用安全管理策略（management security）：

	management.security.enabled=false
（如果classpath下不存在Spring Security，那也就不需要显示的以这种方式来禁用安全管理策略，它甚至可能会破坏应用程序。）

##### 5.3.4 自定义管理服务器的地址
你可以通过设置`management.address`属性来定义管理端点可以使用的地址。这在你只想监听内部或面向生产环境的网络，或只监听来自localhost的连接时非常有用。

下面的application.properties示例不允许远程管理连接：

	management.port=8081
	management.address=127.0.0.1

##### 5.3.5 禁用HTTP端点
如果不想通过HTTP暴露端点，你可以将管理端口设置为-1： `management.port=-1`

##### 5.3.6 HTTP Health端点访问限制
通过health端点暴露的信息根据是否为匿名访问而不同。默认情况下，当匿名访问时，任何有关服务器的健康详情都被隐藏了，该端点只简单的指示服务器是运行（up）还是停止（down）。此外，当匿名访问时，响应会被缓存一个可配置的时间段以防止端点被用于'拒绝服务'攻击。`endpoints.health.time-to-live`属性被用来配置缓存时间（单位为毫秒），默认为1000毫秒，也就是1秒。

上述的限制可以被禁止，从而允许匿名用户完全访问health端点。想达到这个效果，可以将`endpoints.health.sensitive`设为`false`。

#### 5.4 基于JMX的监控和管理
Java管理扩展（JMX）提供了一种标准的监控和管理应用的机制。默认情况下，Spring Boot在`org.springframework.boot`域下将管理端点暴露为JMX MBeans。

##### 5.4.1 自定义MBean名称
MBean的名称通常产生于端点的id。例如，health端点被暴露为`org.springframework.boot/Endpoint/HealthEndpoint`。

如果你的应用包含多个Spring ApplicationContext，你会发现存在名称冲突。为了解决这个问题，你可以将`endpoints.jmx.uniqueNames`设置为true，这样MBean的名称总是唯一的。

你也可以自定义JMX域，所有的端点都在该域下暴露。这里有个application.properties示例： ···java endpoints.jmx.domain=myapp endpoints.jmx.uniqueNames=true

##### 5.4.2 禁用JMX端点
如果不想通过JMX暴露端点，你可以将spring.jmx.enabled属性设置为false：

	spring.jmx.enabled=false

##### 5.4.3 使用Jolokia通过HTTP实现JMX远程管理
Jolokia是一个JMX-HTTP桥，它提供了一种访问JMX beans的替代方法。想要使用Jolokia，只需添加`org.jolokia:jolokia-core`的依赖。例如，使用Maven需要添加下面的配置：

	<dependency>
	    <groupId>org.jolokia</groupId>
	    <artifactId>jolokia-core</artifactId>
	 </dependency>
在你的管理HTTP服务器上可以通过`/jolokia`访问Jolokia。

###### 5.4.3.1 自定义Jolokia
Jolokia有很多配置，传统上一般使用servlet参数进行设置。使用Spring Boot，你可以在application.properties中通过把参数加上jolokia.config.前缀来设置：

	jolokia.config.debug=true

###### 5.4.3.2 禁用Jolokia
如果你正在使用Jolokia，但不想让Spring Boot配置它，只需要简单的将endpoints.jolokia.enabled属性设置为false：

	endpoints.jolokia.enabled=false

##### 5.4.4 使用远程shell来进行监控和管理
Spring Boot支持集成一个称为'CRaSH'的Java shell。你可以在CRaSH中使用ssh或telnet命令连接到运行的应用。为了启用远程shell支持，你只需添加`spring-boot-starter-remote-shell`的依赖：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-remote-shell</artifactId>
	 </dependency>
注：如果想使用telnet访问，你还需添加对`org.crsh:crsh.shell.telnet`的依赖。

###### 5.4.4.1 连接远程shell
默认情况下，远程shell监听端口2000以等待连接。默认用户名为user，密码为随机生成的，并且在输出日志中会显示。如果应用使用Spring Security，该shell默认使用相同的配置。如果不是，将使用一个简单的认证策略，你可能会看到类似这样的信息：

	Using default password for shell access: ec03e16c-4cf4-49ee-b745-7c8255c1dd7e
Linux和OSX用户可以使用ssh连接远程shell，Windows用户可以下载并安装PuTTY。

	$ ssh -p 2000 user@localhost

	user@localhost's password:
	  .   ____          _            __ _ _
	 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
	( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
	 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
	  '  |____| .__|_| |_|_| |_\__, | / / / /
	 =========|_|==============|___/=/_/_/_/
	 :: Spring Boot ::  (v1.3.0.BUILD-SNAPSHOT) on myhost
输入help可以获取一系列命令的帮助。Spring boot提供`metrics`，`beans`，`autoconfig`和`endpoint`命令。

5.4.4.1.1 远程shell证书
你可以使用shell.auth.simple.user.name和shell.auth.simple.user.password属性配置自定义的连接证书。也可以使用Spring Security的AuthenticationManager处理登录职责。具体参考Javadoc[CrshAutoConfiguration](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/api/org/springframework/boot/actuate/autoconfigure/CrshAutoConfiguration.html)和[ShellProperties](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/api/org/springframework/boot/actuate/autoconfigure/ShellProperties.html)。

###### 5.4.4.2 扩展远程shell
有很多有趣的方式可以用来扩展远程shell。

5.4.4.2.1 远程shell命令
你可以使用Groovy或Java编写其他的shell命令（具体参考CRaSH文档）。默认情况下，Spring Boot会搜索以下路径的命令：

* classpath*:/commands/**
* classpath*:/crash/commands/**

注：可以通过shell.commandPathPatterns属性改变搜索路径。

下面是一个从src/main/resources/commands/hello.groovy加载的'hello world'命令：

	package commands

	import org.crsh.cli.Usage
	import org.crsh.cli.Command

	class hello {

	    @Usage("Say Hello")
	    @Command
	    def main(InvocationContext context) {
	        return "Hello"
	    }

	}
Spring Boot将一些额外属性添加到了InvocationContext，你可以在命令中访问它们：

|属性名称|	描述|
|:--|:--|
|spring.boot.version	|Spring Boot的版本|
|spring.version	|Spring框架的核心版本|
|spring.beanfactory	|获取Spring的BeanFactory|
|spring.environment	|获取Spring的Environment|

5.4.4.2.2 远程shell插件
除了创建新命令，也可以扩展CRaSH shell的其他特性。所有继承org.crsh.plugin.CRaSHPlugin的Spring Beans将自动注册到shell。

具体查看[CRaSH参考文档](http://www.crashub.org/)。

##### 5.4.5 度量指标
Spring Boot执行器包括一个支持'gauge'和'counter'级别的度量指标服务。'gauge'记录一个单一值；'counter'记录一个增量（增加或减少）。同时，Spring Boot提供一个[PublicMetrics](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/endpoint/PublicMetrics.java)接口，你可以实现它，从而暴露以上两种机制不能记录的指标。具体参考[SystemPublicMetrics](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/endpoint/SystemPublicMetrics.java)。

所有HTTP请求的指标都被自动记录，所以如果点击metrics端点，你可能会看到类似以下的响应：

```json
{
    "counter.status.200.root": 20,
    "counter.status.200.metrics": 3,
    "counter.status.200.star-star": 5,
    "counter.status.401.root": 4,
    "gauge.response.star-star": 6,
    "gauge.response.root": 2,
    "gauge.response.metrics": 3,
    "classes": 5808,
    "classes.loaded": 5808,
    "classes.unloaded": 0,
    "heap": 3728384,
    "heap.committed": 986624,
    "heap.init": 262144,
    "heap.used": 52765,
    "mem": 986624,
    "mem.free": 933858,
    "processors": 8,
    "threads": 15,
    "threads.daemon": 11,
    "threads.peak": 15,
    "uptime": 494836,
    "instance.uptime": 489782,
    "datasource.primary.active": 5,
    "datasource.primary.usage": 0.25
}
```
此处我们可以看到基本的memory，heap，class loading，processor和thread pool信息，连同一些HTTP指标。在该实例中，root('/')，/metrics URLs分别返回20次，3次HTTP 200响应。同时可以看到root URL返回了4次HTTP 401（unauthorized）响应。双asterix（star-star）来自于被Spring MVC /**匹配到的一个请求（通常为一个静态资源）。

gauge级别展示了一个请求的最后响应时间。所以，root的最后请求被响应耗时2毫秒，/metrics耗时3毫秒。

###### 5.4.5.1 系统指标
Spring Boot暴露以下系统指标：

* 系统内存总量（mem），单位:Kb
* 空闲内存数量（mem.free），单位:Kb
* 处理器数量（processors）
* 系统正常运行时间（uptime），单位:毫秒
* 应用上下文（就是一个应用实例）正常运行时间（instance.uptime），单位:毫秒
* 系统平均负载（systemload.average）
* 堆信息（heap，heap.committed，heap.init，heap.used），单位:Kb
* 线程信息（threads，thread.peak，thead.daemon）
* 类加载信息（classes，classes.loaded，classes.unloaded）
* 垃圾收集信息（gc.xxx.count, gc.xxx.time）

###### 5.4.5.2 数据源指标
Spring Boot会为你应用中定义的支持的DataSource暴露以下指标：

* 最大连接数（datasource.xxx.max）
* 最小连接数（datasource.xxx.min）
* 活动连接数（datasource.xxx.active）
* 连接池的使用情况（datasource.xxx.usage）

所有的数据源指标共用datasoure.前缀。该前缀对每个数据源都非常合适：

* 如果是主数据源（唯一可用的数据源或存在的数据源中被@Primary标记的）前缀为datasource.primary
* 如果数据源bean名称以dataSource结尾，那前缀就是bean的名称去掉dataSource的部分（例如，batchDataSource的前缀是datasource.batch）
* 其他情况使用bean的名称作为前缀

通过注册一个自定义版本的DataSourcePublicMetrics bean，你可以覆盖部分或全部的默认行为。默认情况下，Spring Boot提供支持所有数据源的元数据；如果你喜欢的数据源恰好不被支持，你可以添加另外的DataSourcePoolMetadataProvider beans。具体参考DataSourcePoolMetadataProvidersConfiguration。

###### 5.4.5.3 Tomcat session指标
如果你使用Tomcat作为内嵌的servlet容器，session指标将被自动暴露出去。 `httpsessions.active`和`httpsessions.max`提供了活动的和最大的session数量。

###### 5.4.5.4 记录自己的指标
想要记录你自己的指标，只需将[CounterService](https://github.com/spring-projects/spring-boot/blob/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/metrics/CounterService.java)或[GaugeService](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/metrics/GaugeService.java)注入到你的bean中。CounterService暴露increment，decrement和reset方法；GaugeService提供一个submit方法。

下面是一个简单的示例，它记录了方法调用的次数：



	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.boot.actuate.metrics.CounterService;
	import org.springframework.stereotype.Service;

	@Service
	public class MyService {

	    private final CounterService counterService;

	    @Autowired
	    public MyService(CounterService counterService) {
	        this.counterService = counterService;
	    }

	    public void exampleMethod() {
	        this.counterService.increment("services.system.myservice.invoked");
	    }

	}

注：你可以将任何的字符串用作指标的名称，但最好遵循所选存储或图技术的指南。[Matt Aimonetti’s Blog](http://matt.aimonetti.net/posts/2013/06/26/practical-guide-to-graphite-monitoring/)中有一些好的关于图（Graphite）的指南。

###### 5.4.5.5 添加你自己的公共指标
想要添加额外的，每次指标端点被调用时都会重新计算的度量指标，只需简单的注册其他的PublicMetrics实现bean(s)。默认情况下，端点会聚合所有这样的beans，通过定义自己的MetricsEndpoint可以轻易改变这种情况。

###### 5.4.5.6 指标仓库
通过绑定一个[MetricRepository](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/metrics/repository/MetricRepository.java)来实现指标服务。`MetricRepository`负责存储和追溯指标信息。Spring Boot提供一个`InMemoryMetricRepository`和一个`RedisMetricRepository`（默认使用in-memory仓库），不过你可以编写自己的`MetricRepository`。`MetricRepository`接口实际是`MetricReader`接口和MetricWriter接口的上层组合。具体参考Javadoc

没有什么能阻止你直接将`MetricRepository`的数据导入应用中的后端存储，但我们建议你使用默认的`InMemoryMetricRepository`（如果担心堆使用情况，你可以使用自定义的Map实例），然后通过一个scheduled export job填充后端仓库（意思是先将数据保存到内存中，然后通过异步job将数据持久化到数据库，可以提高系统性能）。通过这种方式，你可以将指标数据缓存到内存中，然后通过低频率或批量导出来减少网络拥堵。Spring Boot提供一个Exporter接口及一些帮你开始的基本实现。

###### 5.4.5.7 Dropwizard指标
Dropwizard ‘Metrics’库的用户会发现Spring Boot指标被发布到了com.codahale.metrics.MetricRegistry。当你声明对io.dropwizard.metrics:metrics-core库的依赖时会创建一个默认的com.codahale.metrics.MetricRegistry Spring bean；如果需要自定义，你可以注册自己的@Bean实例。来自于MetricRegistry的指标也是自动通过/metrics端点暴露的。

用户可以通过使用合适类型的指标名称作为前缀来创建Dropwizard指标（比如，histogram.* , meter.*）。

###### 5.4.5.8 消息渠道集成
如果你的classpath下存在'Spring Messaging' jar，一个名为metricsChannel的MessageChannel将被自动创建（除非已经存在一个）。此外，所有的指标更新事件作为'messages'发布到该渠道上。订阅该渠道的客户端可以进行额外的分析或行动。

##### 5.4.6 审计
Spring Boot执行器具有一个灵活的审计框架，一旦Spring Security处于活动状态（默认抛出'authentication success'，'failure'和'access denied'异常），它就会发布事件。这对于报告非常有用，同时可以基于认证失败实现一个锁定策略。

你也可以使用审计服务处理自己的业务事件。为此，你可以将存在的AuditEventRepository注入到自己的组件，并直接使用它，或者只是简单地通过Spring ApplicationEventPublisher发布AuditApplicationEvent（使用ApplicationEventPublisherAware）。

##### 5.4.7 追踪（Tracing）
对于所有的HTTP请求Spring Boot自动启用追踪。你可以查看trace端点，并获取最近一些请求的基本信息：

	[{
	    "timestamp": 1394343677415,
	    "info": {
	        "method": "GET",
	        "path": "/trace",
	        "headers": {
	            "request": {
	                "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
	                "Connection": "keep-alive",
	                "Accept-Encoding": "gzip, deflate",
	                "User-Agent": "Mozilla/5.0 Gecko/Firefox",
	                "Accept-Language": "en-US,en;q=0.5",
	                "Cookie": "_ga=GA1.1.827067509.1390890128; ..."
	                "Authorization": "Basic ...",
	                "Host": "localhost:8080"
	            },
	            "response": {
	                "Strict-Transport-Security": "max-age=31536000 ; includeSubDomains",
	                "X-Application-Context": "application:8080",
	                "Content-Type": "application/json;charset=UTF-8",
	                "status": "200"
	            }
	        }
	    }
	},{
	    "timestamp": 1394343684465,
	    ...
	}]

###### 5.4.7.1 自定义追踪
如果需要追踪其他的事件，你可以将一个[TraceRepository](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/trace/TraceRepository.java)注入到你的Spring Beans中。add方法接收一个将被转化为JSON的Map结构，该数据将被记录下来。

默认情况下，使用的InMemoryTraceRepository将存储最新的100个事件。如果需要扩展该容量，你可以定义自己的InMemoryTraceRepository实例。如果需要，你可以创建自己的替代TraceRepository实现。

##### 5.4.8 进程监控
在Spring Boot执行器中，你可以找到几个创建有利于进程监控的文件的类：

* ApplicationPidFileWriter创建一个包含应用PID的文件（默认位于应用目录，文件名为application.pid）
* EmbeddedServerPortFileWriter创建一个或多个包含内嵌服务器端口的文件（默认位于应用目录，文件名为application.port）

默认情况下，这些writers没有被激活，但你可以使用下面描述的任何方式来启用它们。

###### 5.4.8.1 扩展属性
你需要激活META-INF/spring.factories文件里的listener(s)：

	org.springframework.context.ApplicationListener=\
	org.springframework.boot.actuate.system.ApplicationPidFileWriter,
	org.springframework.boot.actuate.system.EmbeddedServerPortFileWriter

###### 5.4.8.2 以编程方式
你也可以通过调用SpringApplication.addListeners(…)方法来激活一个监听器，并传递相应的Writer对象。该方法允许你通过Writer构造器自定义文件名和路径。

### 部署到云端
对于大多数流行云PaaS（平台即服务）提供商，Spring Boot的可执行jars就是为它们准备的。这些提供商往往要求你带上自己的容器；它们管理应用的进程（不特别针对Java应用程序），所以它们需要一些中间层来将你的应用适配到云概念中的一个运行进程。

两个流行的云提供商，Heroku和Cloud Foundry，采取一个打包（'buildpack'）方法。为了启动你的应用程序，不管需要什么，buildpack都会将它们打包到你的部署代码：它可能是一个JDK和一个java调用，也可能是一个内嵌的webserver，或者是一个成熟的应用服务器。buildpack是可插拔的，但你最好尽可能少的对它进行自定义设置。这可以减少不受你控制的功能范围，最小化部署和生产环境的发散。

理想情况下，你的应用就像一个Spring Boot可执行jar，所有运行需要的东西都打包到它内部。

#### 6.1 Cloud Foundry
如果不指定其他打包方式，Cloud Foundry会启用它提供的默认打包方式。Cloud Foundry的Java buildpack对Spring应用有出色的支持，包括Spring Boot。你可以部署独立的可执行jar应用，也可以部署传统的.war形式的应用。

一旦你构建了应用（比如，使用mvn clean package）并安装了cf命令行工具，你可以使用下面的cf push命令（将路径指向你编译后的.jar）来部署应用。在发布一个应用前，确保你已登陆cf命令行客户端。

	$ cf push acloudyspringtime -p target/demo-0.0.1-SNAPSHOT.jar
查看cf push文档获取更多可选项。如果相同目录下存在manifest.yml，Cloud Foundry会使用它。

就此，cf开始上传你的应用：

	Uploading acloudyspringtime... OK
	Preparing to start acloudyspringtime... OK
	-----> Downloaded app package (8.9M)
	-----> Java Buildpack source: system
	-----> Downloading Open JDK 1.7.0_51 from .../x86_64/openjdk-1.7.0_51.tar.gz (1.8s)
	       Expanding Open JDK to .java-buildpack/open_jdk (1.2s)
	-----> Downloading Spring Auto Reconfiguration from  0.8.7 .../auto-reconfiguration-0.8.7.jar (0.1s)
	-----> Uploading droplet (44M)
	Checking status of app 'acloudyspringtime'...
	  0 of 1 instances running (1 starting)
	  ...
	  0 of 1 instances running (1 down)
	  ...
	  0 of 1 instances running (1 starting)
	  ...
	  1 of 1 instances running (1 running)

	App started
恭喜！应用现在处于运行状态！

检验部署应用的状态是很简单的：

	$ cf apps
	Getting applications in ...
	OK

	name                 requested state   instances   memory   disk   urls
	...
	acloudyspringtime    started           1/1         512M     1G     acloudyspringtime.cfapps.io
	...
一旦Cloud Foundry意识到你的应用已经部署，你就可以点击给定的应用URI，此处是[acloudyspringtime.cfapps.io/](http://acloudyspringtime.cfapps.io/)。

##### 6.1.1 绑定服务
默认情况下，运行应用的元数据和服务连接信息被暴露为应用的环境变量（比如，$VCAP_SERVICES）。采用这种架构的原因是因为Cloud Foundry多语言特性（任何语言和平台都支持作为buildpack）。进程级别的环境变量是语言无关（language agnostic）的。

环境变量并不总是有利于设计最简单的API，所以Spring Boot自动提取它们，然后将这些数据导入能够通过Spring Environment抽象访问的属性里：


	@Component
	class MyBean implements EnvironmentAware {

	    private String instanceId;

	    @Override
	    public void setEnvironment(Environment environment) {
	        this.instanceId = environment.getProperty("vcap.application.instance_id");
	    }

	    // ...

	}

所有的Cloud Foundry属性都以vcap作为前缀。你可以使用vcap属性获取应用信息（比如应用的公共URL）和服务信息（比如数据库证书）。具体参考VcapApplicationListener Javadoc。

注：[Spring Cloud Connectors](http://cloud.spring.io/spring-cloud-connectors/)项目很适合比如配置数据源的任务。Spring Boot提供自动配置支持和一个spring-boot-starter-cloud-connectors starter POM。

#### 6.2 Heroku
Heroku是另外一个流行的Paas平台。想要自定义Heroku的构建过程，你可以提供一个Procfile，它提供部署一个应用所需的指令。Heroku为Java应用分配一个端口，确保能够路由到外部URI。

你必须配置你的应用监听正确的端口。下面是用于我们的starter REST应用的Procfile：

	web: java -Dserver.port=$PORT -jar target/demo-0.0.1-SNAPSHOT.jar
Spring Boot将-D参数作为属性，通过一个Spring的Environment实例访问。server.port配置属性适合于内嵌的Tomcat，Jetty或Undertow实例启用时使用。$PORT环境变量被分配给Heroku Paas使用。

Heroku默认使用Java 1.6。只要你的Maven或Gradle构建时使用相同的版本就没问题（Maven用户可以设置java.version属性）。如果你想使用JDK 1.7，在你的pom.xml和Procfile临近处创建一个system.properties文件。在该文件中添加以下设置：

	java.runtime.version=1.7

这就是你需要做的一切。对于Heroku部署来说，经常做的工作就是使用git push将代码推送到生产环境。



	$ git push heroku master
	Initializing repository, done.
	Counting objects: 95, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (78/78), done.
	Writing objects: 100% (95/95), 8.66 MiB | 606.00 KiB/s, done.
	Total 95 (delta 31), reused 0 (delta 0)

	-----> Java app detected
	-----> Installing OpenJDK 1.7... done
	-----> Installing Maven 3.2.3... done
	-----> Installing settings.xml... done
	-----> executing /app/tmp/cache/.maven/bin/mvn -B
	       -Duser.home=/tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229
	       -Dmaven.repo.local=/app/tmp/cache/.m2/repository
	       -s /app/tmp/cache/.m2/settings.xml -DskipTests=true clean install

	       [INFO] Scanning for projects...
	       Downloading: http://repo.spring.io/...
	       Downloaded: http://repo.spring.io/... (818 B at 1.8 KB/sec)
	        ....
	       Downloaded: http://s3pository.heroku.com/jvm/... (152 KB at 595.3 KB/sec)
	       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/target/...
	       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/pom.xml ...
	       [INFO] ------------------------------------------------------------------------
	       [INFO] BUILD SUCCESS
	       [INFO] ------------------------------------------------------------------------
	       [INFO] Total time: 59.358s
	       [INFO] Finished at: Fri Mar 07 07:28:25 UTC 2014
	       [INFO] Final Memory: 20M/493M
	       [INFO] ------------------------------------------------------------------------

	-----> Discovering process types
	       Procfile declares types -> web

	-----> Compressing... done, 70.4MB
	-----> Launching... done, v6
	       http://agile-sierra-1405.herokuapp.com/ deployed to Heroku

	To git@heroku.com:agile-sierra-1405.git
	 * [new branch]      master -> master
现在你的应用已经启动并运行在Heroku。

#### 6.3 Openshift
Openshift是RedHat公共（和企业）PaaS解决方案。和Heroku相似，它也是通过运行被git提交触发的脚本来工作的，所以你可以使用任何你喜欢的方式编写Spring Boot应用启动脚本，只要Java运行时环境可用（这是在Openshift上可以要求的一个标准特性）。为了实现这样的效果，你可以使用DIY Cartridge，并在.openshift/action_scripts下hooks你的仓库：

基本模式如下：

1.确保Java和构建工具已被远程安装，比如使用一个pre_build hook（默认会安装Java和Maven，不会安装Gradle）。

2.使用一个build hook去构建你的jar（使用Maven或Gradle），比如

	#!/bin/bash
	cd $OPENSHIFT_REPO_DIR
	mvn package -s .openshift/settings.xml -DskipTests=true
3.添加一个调用java -jar …​的start hook

	#!/bin/bash
	cd $OPENSHIFT_REPO_DIR
	nohup java -jar target/*.jar --server.port=${OPENSHIFT_DIY_PORT} --server.address=${OPENSHIFT_DIY_IP} &
4.使用一个stop hook

	#!/bin/bash
	source $OPENSHIFT_CARTRIDGE_SDK_BASH
	PID=$(ps -ef | grep java.*\.jar | grep -v grep | awk '{ print $2 }')
	if [ -z "$PID" ]
	then
	    client_result "Application is already stopped"
	else
	    kill $PID
	fi
5.将内嵌的服务绑定到平台提供的在application.properties定义的环境变量，比如

	spring.datasource.url: jdbc:mysql://${OPENSHIFT_MYSQL_DB_HOST}:${OPENSHIFT_MYSQL_DB_PORT}/${OPENSHIFT_APP_NAME}
	spring.datasource.username: ${OPENSHIFT_MYSQL_DB_USERNAME}
	spring.datasource.password: ${OPENSHIFT_MYSQL_DB_PASSWORD}

在Openshift的网站上有一篇running Gradle in Openshift博客，如果想使用gradle构建运行的应用可以参考它。由于一个Gradle bug，你不能使用高于1.6版本的Gradle。


##### 6.4 Google App Engine
Google App Engine跟Servlet 2.5 API是有联系的，所以在不修改的情况系你是不能部署一个Spring应用的。具体查看本指南的Servlet 2.5章节 Container.md)。

### Spring Boot CLI
Spring Boot CLI是一个命令行工具，如果想使用Spring进行快速开发可以使用它。它允许你运行Groovy脚本，这意味着你可以使用熟悉的类Java语法，并且没有那么多的模板代码。你也可以启动一个新的项目或为Spring Boot CLI编写自己的命令。

#### 7.1 安装CLI
你可以手动安装Spring Boot CLI，也可以使用GVM（Groovy环境管理工具）或Homebrew，MacPorts（如果你是一个OSX用户）。参考"Getting started"的[Section 10.2, “Installing the Spring Boot CLI”](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/II.%20Getting%20started/10.2.%20Installing%20the%20Spring%20Boot%20CLI.md) 可以看到全面的安装指令。

#### 7.2 使用CLI
一旦安装好CLI，你可以输入spring来运行它。如果你不使用任何参数运行spring，将会展现一个简单的帮助界面：

	$ spring
	usage: spring [--help] [--version]
	        []

	Available commands are:

	  run [options]  [--] [args]
	    Run a spring groovy script

	  ... more command help is shown here
你可以使用help获取任何支持命令的详细信息。例如：

	$ spring help run
	spring run - Run a spring groovy script

	usage: spring run [options]  [--] [args]

	Option                     Description
	------                     -----------
	--autoconfigure [Boolean]  Add autoconfigure compiler
	                             transformations (default: true)
	--classpath, -cp           Additional classpath entries
	-e, --edit                 Open the file with the default system
	                             editor
	--no-guess-dependencies    Do not attempt to guess dependencies
	--no-guess-imports         Do not attempt to guess imports
	-q, --quiet                Quiet logging
	-v, --verbose              Verbose logging of dependency
	                             resolution
	--watch                    Watch the specified file for changes
version命令提供一个检查你正在使用的Spring Boot版本的快速方式：

	$ spring version
	Spring CLI v1.3.0.BUILD-SNAPSHOT

##### 7.2.1 使用CLI运行应用
你可以使用run命令编译和运行Groovy源代码。Spring Boot CLI完全自包含，以致于你不需要安装任何外部的Groovy。

下面是一个使用Groovy编写的"hello world" web应用： hello.grooy

	@RestController
	class WebApplication {

	    @RequestMapping("/")
	    String home() {
	        "Hello World!"
	    }

	}
想要编译和运行应用，输入：

$ spring run hello.groovy
想要给应用传递命令行参数，你需要使用一个--来将它们和"spring"命令参数区分开来。例如：

	$ spring run hello.groovy -- --server.port=9000
想要设置JVM命令行参数，你可以使用JAVA_OPTS环境变量，例如：

	$ JAVA_OPTS=-Xmx1024m spring run hello.groovy

###### 7.2.1.1 推断"grab"依赖
标准的Groovy包含一个`@Grab`注解，它允许你声明对第三方库的依赖。这项有用的技术允许Groovy以和Maven或Gradle相同的方式下载jars，但不需要使用构建工具。

Spring Boot进一步延伸了该技术，它会基于你的代码尝试推导你"grab"哪个库。例如，由于WebApplication代码上使用了`@RestController`注解，"Tomcat"和"Spring MVC"将被获取（grabbed）。

下面items被用作"grab hints"：

|items	|Grabs|
|:--|:--|
|JdbcTemplate,NamedParameterJdbcTemplate,DataSource	|JDBC应用|
|@EnableJms	|JMS应用|
|@EnableCaching	|Caching abstraction|
|@Test	|JUnit|
|@EnableRabbit	|RabbitMQ|
|@EnableReactor	|Project Reactor|
|继承Specification	|Spock test|
|@EnableBatchProcessing	|Spring Batch|
|@MessageEndpoint,@EnableIntegrationPatterns	|Spring Integration|
|@EnableDeviceResolver	|Spring Mobile|
|@Controller,@RestController,@EnableWebMvc	|Spring MVC + Embedded Tomcat|
|@EnableWebSecurity	|Spring Security|
|@EnableTransactionManagement	|Spring Transaction Management|


注：想要理解自定义是如何生效，可以查看Spring Boot CLI源码中的[CompilerAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-cli/src/main/java/org/springframework/boot/cli/compiler/CompilerAutoConfiguration.java)子类。

###### 7.2.1.2  推断"grab"坐标
Spring Boot扩展Groovy标准"@Grab"注解使其能够允许你指定一个没有group或version的依赖，例如@Grab('freemarker')。 artifact’s的组和版本是通过查看Spring Boot的依赖元数据推断出来的。注意默认的元数据是和你使用的CLI版本绑定的－只有在你迁移到一个CLI新版本时它才会改变，这样当你的依赖改变时你就可以控制了。在附录的表格中可以查看默认元数据包含的依赖和它们的版本。

###### 7.2.1.3 默认import语句
为了帮助你减少Groovy代码量，一些import语句被自动包含进来了。注意上面的示例中引用@Component，@RestController和@RequestMapping而没有使用全限定名或import语句。

注：很多Spring注解在不使用import语句的情况下可以正常工作。尝试运行你的应用，看一下在添加imports之前哪些会失败。

###### 7.2.1.4 自动创建main方法
跟等效的Java应用不同，你不需要在Groovy脚本中添加一个public static void main(String[] args)方法。Spring Boot 会使用你编译后的代码自动创建一个SpringApplication。

###### 7.2.1.5 自定义"grab"元数据
Spring Boot提供一个新的@GrabMetadata注解，你可以使用它提供自定义的依赖元数据，以覆盖Spring Boot的默认配置。该元数据通过使用提供一个或多个配置文件坐标的注解来指定（使用一个属性标识符"type"部署到Maven仓库）.。配置文件中的每个实体必须遵循group:module=version的格式。

例如，下面的声明：

	`@GrabMetadata("com.example.custom-versions:1.0.0")`
将会加载Maven仓库处于`com/example/custom-versions/1.0.0/`下的`custom-versions-1.0.0.properties`文件。

可以通过注解指定多个属性文件，它们会以声明的顺序被使用。例如：

	`@GrabMetadata(["com.example.custom-versions:1.0.0",
	        "com.example.more-versions:1.0.0"])`
意味着位于more-versions的属性将覆盖位于custom-versions的属性。

你可以在任何能够使用@Grab的地方使用@GrabMetadata，然而，为了确保元数据的顺序一致，你在应用程序中最多只能使用一次@GrabMetadata。Spring IO Platform是一个非常有用的依赖元数据源(Spring Boot的超集)，例如：

	@GrabMetadata('io.spring.platform:platform-versions:1.0.4.RELEASE')

##### 7.2.2 测试你的代码
test命令允许你编译和运行应用程序的测试用例。常规使用方式如下：

	$ spring test app.groovy tests.groovy
	Total: 1, Success: 1, : Failures: 0
	Passed? true
在这个示例中，test.groovy包含JUnit @Test方法或Spock Specification类。所有的普通框架注解和静态方法在不使用import导入的情况下，仍旧可以使用。

下面是我们使用的test.groovy文件（含有一个JUnit测试）：

	class ApplicationTests {

	    @Test
	    void homeSaysHello() {
	        assertEquals("Hello World!", new WebApplication().home())
	    }

	}
注：如果有多个测试源文件，你可以倾向于使用一个test目录来组织它们。

##### 7.2.3 多源文件应用
你可以在所有接收文件输入的命令中使用shell通配符。这允许你轻松处理来自一个目录下的多个文件，例如：

	$ spring run *.groovy
如果你想将'test'或'spec'代码从主应用代码中分离，这项技术就十分有用了：

	$ spring test app/*.groovy test/*.groovy

##### 7.2.4 应用打包
你可以使用jar命令打包应用程序为一个可执行的jar文件。例如：

	$ spring jar my-app.jar *.groovy
最终的jar包括编译应用产生的类和所有依赖，这样你就可以使用java -jar来执行它了。该jar文件也包括来自应用classpath的实体。你可以使用--include和--exclude添加明确的路径（两者都是用逗号分割，同样都接收值为'+'和'-'的前缀，'-'意味着它们将从默认设置中移除）。默认包含（includes）：

	public/**, resources/**, static/**, templates/**, META-INF/**, *
默认排除(excludes)：

	.*, repository/**, build/**, target/**, **/*.jar, **/*.groovy
查看spring help jar可以获得更多信息。

##### 7.2.5 初始化新工程
init命令允许你使用start.spring.io在不离开shell的情况下创建一个新的项目。例如：

	$ spring init --dependencies=web,data-jpa my-project
	Using service at https://start.spring.io
	Project extracted to '/Users/developer/example/my-project'
这创建了一个my-project目录，它是一个基本Maven且依赖spring-boot-starter-web和spring-boot-starter-data-jpa的项目。你可以使用--list参数列出该服务的能力。

	$ spring init --list
	=======================================
	Capabilities of https://start.spring.io
	=======================================

	Available dependencies:
	-----------------------
	actuator - Actuator: Production ready features to help you monitor and manage your application
	...
	web - Web: Support for full-stack web development, including Tomcat and spring-webmvc
	websocket - Websocket: Support for WebSocket development
	ws - WS: Support for Spring Web Services

	Available project types:
	------------------------
	gradle-build -  Gradle Config [format:build, build:gradle]
	gradle-project -  Gradle Project [format:project, build:gradle]
	maven-build -  Maven POM [format:build, build:maven]
	maven-project -  Maven Project [format:project, build:maven] (default)

	...
init命令支持很多选项，查看help输出可以获得更多详情。例如，下面的命令创建一个使用Java8和war打包的gradle项目：

	$ spring init --build=gradle --java-version=1.8 --dependencies=websocket --packaging=war sample-app.zip
	Using service at https://start.spring.io
	Content saved to 'sample-app.zip'


##### 7.2.6 使用内嵌shell
Spring Boot包括完整的BASH和zsh shells的命令行脚本。如果你不使用它们中的任何一个（可能你是一个Window用户），那你可以使用shell命令启用一个集成shell。

	$ spring shell
	Spring Boot (v1.3.0.BUILD-SNAPSHOT)
	Hit TAB to complete. Type \'help' and hit RETURN for help, and \'exit' to quit.
从内嵌shell中可以直接运行其他命令：

	$ version
	Spring CLI v1.3.0.BUILD-SNAPSHOT

内嵌shell支持ANSI颜色输出和tab补全。如果需要运行一个原生命令，你可以使用$前缀。点击ctrl-c将退出内嵌shell。

##### 7.2.7 为CLI添加扩展
使用install命令可以为CLI添加扩展。该命令接收一个或多个格式为group:artifact:version的artifact坐标集。例如：

	$ spring install com.example:spring-boot-cli-extension:1.0.0.RELEASE
除了安装你提供坐标的artifacts标识外，所有依赖也会被安装。使用uninstall可以卸载一个依赖。和install命令一样，它接收一个或多个格式为group:artifact:version的artifact坐标集。例如：

	$ spring uninstall com.example:spring-boot-cli-extension:1.0.0.RELEASE
它会通过你提供的坐标卸载相应的artifacts标识和它们的依赖。

为了卸载所有附加依赖，你可以使用--all选项。例如：

	$ spring uninstall --all

#### 7.3 使用Groovy beans DSL开发应用

Spring框架4.0版本对beans{} DSL（借鉴自[Grails](http://grails.org/)）提供原生支持，你可以使用相同的格式在你的Groovy应用程序脚本中嵌入bean定义。有时候这是一个包括外部特性的很好的方式，比如中间件声明。例如：

	@Configuration
	class Application implements CommandLineRunner {

	    @Autowired
	    SharedService service

	    @Override
	    void run(String... args) {
	        println service.message
	    }

	}

	import my.company.SharedService

	beans {
	    service(SharedService) {
	        message = "Hello World"
	    }
	}
你可以使用beans{}混合位于相同文件的类声明，只要它们都处于顶级，或如果你喜欢的话，可以将beans DSL放到一个单独的文件中。


### 构建工具插件
Spring Boot为Maven和Gradle提供构建工具插件。该插件提供各种各样的特性，包括打包可执行jars。本节提供关于插件的更多详情及用于扩展一个不支持的构建系统所需的帮助信息。如果你是刚刚开始，那可能需要先阅读Part III, `“Using Spring Boot”`章节的`“Chapter 13, Build systems”`。

#### 8.1 Spring Boot Maven插件
Spring Boot Maven插件为Maven提供Spring Boot支持，它允许你打包可执行jar或war存档，然后就地运行应用。为了使用它，你需要使用Maven 3.2 （或更高版本）。

注：参考[Spring Boot Maven Plugin Site](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/maven-plugin/)可以获取全部的插件文档。

##### 8.1.1 包含该插件
想要使用Spring Boot Maven插件只需简单地在你的pom.xml的plugins部分包含相应的XML：

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <modelVersion>4.0.0</modelVersion>
	    <!-- ... -->
	    <build>
	        <plugins>
	            <plugin>
	                <groupId>org.springframework.boot</groupId>
	                <artifactId>spring-boot-maven-plugin</artifactId>
	                <version>1.3.0.BUILD-SNAPSHOT</version>
	                <executions>
	                    <execution>
	                        <goals>
	                            <goal>repackage</goal>
	                        </goals>
	                    </execution>
	                </executions>
	            </plugin>
	        </plugins>
	    </build>
	</project>
该配置会在Maven生命周期的package阶段重新打包一个jar或war。下面的示例显示在target目录下既有重新打包后的jar，也有原始的jar：

	$ mvn package
	$ ls target/*.jar
	target/myproject-1.0.0.jar target/myproject-1.0.0.jar.original
如果不包含像上面那样的<execution/>，你可以自己运行该插件（但只有在package目标也被使用的情况）。例如：

	$ mvn package spring-boot:repackage
	$ ls target/*.jar
	target/myproject-1.0.0.jar target/myproject-1.0.0.jar.original
如果使用一个里程碑或快照版本，你还需要添加正确的pluginRepository元素：

	<pluginRepositories>
	    <pluginRepository>
	        <id>spring-snapshots</id>
	        <url>http://repo.spring.io/snapshot</url>
	    </pluginRepository>
	    <pluginRepository>
	        <id>spring-milestones</id>
	        <url>http://repo.spring.io/milestone</url>
	    </pluginRepository>
	</pluginRepositories>

##### 8.1.2 打包可执行jar和war文件
一旦spring-boot-maven-plugin被包含到你的pom.xml中，它就会自动尝试使用spring-boot:repackage目标重写存档以使它们能够执行。为了构建一个jar或war，你应该使用常规的packaging元素配置你的项目：

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <!-- ... -->
	    <packaging>jar</packaging>
	    <!-- ... -->
	</project>
生成的存档在package阶段会被Spring Boot增强。你想启动的main类即可以通过指定一个配置选项，也可以通过为manifest添加一个Main-Class属性这种常规的方式实现。如果你没有指定一个main类，该插件会搜索带有public static void main(String[] args)方法的类。

为了构建和运行一个项目的artifact，你可以输入以下命令：

	$ mvn package
	$ java -jar target/mymodule-0.0.1-SNAPSHOT.jar
为了构建一个即是可执行的，又能部署到一个外部容器的war文件，你需要标记内嵌容器依赖为"provided"，例如：

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <!-- ... -->
	    <packaging>war</packaging>
	    <!-- ... -->
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-web</artifactId>
	        </dependency>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-tomcat</artifactId>
	            <scope>provided</scope>
	        </dependency>
	        <!-- ... -->
	    </dependencies>
	</project>
注：具体参考`“Section 74.1, “Create a deployable war file”`章节。

在插件信息页面有高级的配置选项和示例。

#### 8.2 Spring Boot Gradle插件
Spring Boot Gradle插件为Gradle提供Spring Boot支持，它允许你打包可执行jar或war存档，运行Spring Boot应用，对于"神圣的"依赖可以在你的build.gradle文件中省略版本信息。

##### 8.2.1 包含该插件
想要使用Spring Boot Gradle插件，你只需简单的包含一个buildscript依赖，并应用spring-boot插件：

	buildscript {
	    dependencies {
	        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.0.BUILD-SNAPSHOT")
	    }
	}
	apply plugin: 'spring-boot'

如果想使用一个里程碑或快照版本，你可以添加相应的repositories引用：

	buildscript {
	    repositories {
	        maven.url "http://repo.spring.io/snapshot"
	        maven.url "http://repo.spring.io/milestone"
	    }
	    // ...
	}

##### 8.2.2 声明不带版本的依赖
spring-boot插件会为你的构建注册一个自定义的Gradle ResolutionStrategy，它允许你在声明对"神圣"的artifacts的依赖时获取版本号。为了充分使用该功能，只需要想通常那样声明依赖，但将版本号设置为空：

	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web")
	    compile("org.thymeleaf:thymeleaf-spring4")
	    compile("nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect")
	}
注：你声明的spring-boot Gradle插件的版本决定了"blessed"依赖的实际版本（确保可以重复构建）。你最好总是将spring-boot gradle插件版本设置为你想用的Spring Boot实际版本。提供的版本详细信息可以在附录中找到。

spring-boot插件对于没有指定版本的依赖只会提供一个版本。如果不想使用插件提供的版本，你可以像平常那样在声明依赖的时候指定版本。例如：

	dependencies {
	    compile("org.thymeleaf:thymeleaf-spring4:2.1.1.RELEASE")
	}

###### 8.2.2.1  自定义版本管理
如果你需要不同于Spring Boot的"blessed"依赖，有可能的话可以自定义ResolutionStrategy使用的版本。替代的版本元数据使用versionManagement配置。例如：

	dependencies {
	    versionManagement("com.mycorp:mycorp-versions:1.0.0.RELEASE@properties")
	    compile("org.springframework.data:spring-data-hadoop")
	}
版本信息需要作为一个.properties文件发布到一个仓库中。对于上面的示例，mycorp-versions.properties文件可能包含以下内容：

	org.springframework.data\:spring-data-hadoop=2.0.0.RELEASE
属性文件优先于Spring Boot默认设置，如果有必要的话可以覆盖版本号。

##### 8.2.3 默认排除规则
Gradle处理"exclude rules"的方式和Maven稍微有些不同，在使用starter POMs时这可能会引起无法预料的结果。特别地，当一个依赖可以通过不同的路径访问时，对该依赖声明的exclusions将不会生效。例如，如果一个starter POM声明以下内容：

	<dependencies>
	    <dependency>
	        <groupId>org.springframework</groupId>
	        <artifactId>spring-core</artifactId>
	        <version>4.0.5.RELEASE</version>
	        <exclusions>
	            <exclusion>
	                <groupId>commons-logging</groupId>
	                <artifactId>commons-logging</artifactId>
	            </exclusion>
	        </exclusions>
	    </dependency>
	    <dependency>
	        <groupId>org.springframework</groupId>
	        <artifactId>spring-context</artifactId>
	        <version>4.0.5.RELEASE</version>
	    </dependency>
	</dependencies>
commons-logging jar不会被Gradle排除，因为通过没有exclusion元素的spring-context可以传递性的拉取到它（spring-context → spring-core → commons-logging）。

为了确保正确的排除被实际应用，Spring Boot Gradle插件将自动添加排除规则。所有排除被定义在spring-boot-dependencies POM，并且针对"starter" POMs的隐式规则也会被添加。

如果不想自动应用排除规则，你可以使用以下配置：

	springBoot {
	    applyExcludeRules=false
	}

##### 8.2.4 打包可执行jar和war文件
一旦spring-boot插件被应用到你的项目，它将使用bootRepackage任务自动尝试重写存档以使它们能够执行。为了构建一个jar或war，你需要按通常的方式配置项目。

你想启动的main类既可以通过一个配置选项指定，也可以通过向manifest添加一个Main-Class属性。如果你没有指定main类，该插件会搜索带有public static void main(String[] args)方法的类。

为了构建和运行一个项目artifact，你可以输入以下内容：

	$ gradle build
	$ java -jar build/libs/mymodule-0.0.1-SNAPSHOT.jar
为了构建一个即能执行也可以部署到外部容器的war包，你需要将内嵌容器依赖标记为"providedRuntime"，比如：

	...
	apply plugin: 'war'

	war {
	    baseName = 'myapp'
	    version =  '0.5.0'
	}

	repositories {
	    jcenter()
	    maven { url "http://repo.spring.io/libs-snapshot" }
	}

	configurations {
	    providedRuntime
	}

	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web")
	    providedRuntime("org.springframework.boot:spring-boot-starter-tomcat")
	    ...
	}
注：具体参考[“Section 74.1, “Create a deployable war file””](https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IX.%20‘How-to’%20guides/74.1.%20Create%20a%20deployable%20war%20file.md)。

##### 8.2.5 就地（in-place）运行项目
为了在不先构建jar的情况下运行项目，你可以使用"bootRun"任务：

	$ gradle bootRun
默认情况下，以这种方式运行项目可以让你的静态classpath资源（比如，默认位于src/main/resources下）在应用运行期间被重新加载。使静态资源可以重新加载意味着bootRun任务不会使用processResources任务的输出，比如，当调用bootRun时，你的应用将以资源未处理的形式来使用它们。

你可以禁止直接使用静态classpath资源。这意味着资源不再是可重新加载的，但processResources任务的输出将会被使用。想要这样做，只需将bootRun任务的addResources设为false：

	bootRun {
	    addResources = false
	}

##### 8.2.6 Spring Boot插件配置
Gradle插件自动扩展你的构建脚本DSL，它为脚本添加一个springBoot元素以此作为Boot插件的全局配置。你可以像配置其他Gradle扩展那样为springBoot设置相应的属性（下面有配置选项列表）。

	springBoot {
	    backupSource = false
	}

##### 8.2.7 Repackage配置
该插件添加了一个bootRepackage任务，你可以直接配置它，比如：

	bootRepackage {
	    mainClass = 'demo.Application'
	}
下面是可用的配置选项：

|名称	|描述|
|:--|:--|
|enabled	|布尔值，用于控制repackager的开关（如果你只想要Boot的其他特性而不是这个，那它就派上用场了）|
|mainClass	|要运行的main类。如果没有指定，则使用project属性mainClassName。如果没有定义mainClassName id，则搜索存档以寻找一个合适的类。"合适"意味着一个唯一的，具有良好格式的main()方法的类（如果找到多个则构建会失败）。你也可以通过"run"任务（main属性）指定main类的名称，和/或将"startScripts"（mainClassName属性）作为"springBoot"配置的替代。|
|classifier	|添加到存档的一个文件名字段（在扩展之前），这样最初保存的存档仍旧存放在最初的位置。在存档被重新打包（repackage）的情况下，该属性默认为null。默认值适用于多数情况，但如果你想在另一个项目中使用原jar作为依赖，最好使用一个扩展来定义该可执行jar|
|withJarTask	|Jar任务的名称或值，用于定位要被repackage的存档|
|customConfiguration	|自定义配置的名称，用于填充内嵌的lib目录（不指定该属性，你将获取所有编译和运行时依赖）|

##### 8.2.8 使用Gradle自定义配置进行Repackage
有时候不打包解析自compile，runtime和provided作用域的默认依赖可能更合适些。如果创建的可执行jar被原样运行，你需要将所有的依赖内嵌进该jar中；然而，如果目的是explode一个jar文件，并手动运行main类，你可能在CLASSPATH下已经有一些可用的库了。在这种情况下，你可以使用不同的依赖集重新打包（repackage）你的jar。

使用自定义的配置将自动禁用来自compile，runtime和provided作用域的依赖解析。自定义配置即可以定义为全局的（处于springBoot部分内），也可以定义为任务级的。

	task clientJar(type: Jar) {
	    appendix = 'client'
	    from sourceSets.main.output
	    exclude('**/*Something*')
	}

	task clientBoot(type: BootRepackage, dependsOn: clientJar) {
	    withJarTask = clientJar
	    customConfiguration = "mycustomconfiguration"
	}
在以上示例中，我们创建了一个新的clientJar Jar任务从你编译后的源中打包一个自定义文件集。然后我们创建一个新的clientBoot BootRepackage任务，并让它使用clientJar任务和mycustomconfiguration。

	configurations {
	    mycustomconfiguration.exclude group: 'log4j'
	}

	dependencies {
	    mycustomconfiguration configurations.runtime
	}
在BootRepackage中引用的配置是一个正常的[Gradle配置](http://www.gradle.org/docs/current/dsl/org.gradle.api.artifacts.Configuration.html)。在上面的示例中，我们创建了一个新的名叫mycustomconfiguration的配置，指示它来自一个runtime，并排除对log4j的依赖。如果clientBoot任务被执行，重新打包的jar将含有所有来自runtime作用域的依赖，除了log4j jars。

###### 8.2.8.1 配置选项
可用的配置选项如下：

|名称	|描述|
|:--|:--|
|mainClass	|可执行jar运行的main类|
|providedConfiguration	|provided配置的名称（默认为providedRuntime）|
|backupSource	|在重新打包之前，原先的存档是否备份（默认为true）|
|customConfiguration	|自定义配置的名称|
|layout	|存档类型，对应于内部依赖是如何制定的（默认基于存档类型进行推测）|
|requiresUnpack	|一个依赖列表（格式为"groupId:artifactId"，为了运行，它们需要从fat jars中解压出来。）所有节点被打包进胖jar，但运行的时候它们将被自动解压|

##### 8.2.9 理解Gradle插件是如何工作的
当spring-boot被应用到你的Gradle项目，一个默认的名叫bootRepackage的任务被自动创建。bootRepackage任务依赖于Gradle assemble任务，当执行时，它会尝试找到所有限定符为空的jar artifacts（也就是说，tests和sources jars被自动跳过）。

由于bootRepackage查找'所有'创建jar artifacts的事实，Gradle任务执行的顺序就非常重要了。多数项目只创建一个单一的jar文件，所以通常这不是一个问题。然而，如果你正打算创建一个更复杂的，使用自定义jar和BootRepackage任务的项目setup，有几个方面需要考虑。

如果'仅仅'从项目创建自定义jar文件，你可以简单地禁用默认的jar和bootRepackage任务：

	jar.enabled = false
	bootRepackage.enabled = false
另一个选项是指示默认的bootRepackage任务只能使用一个默认的jar任务：

	bootRepackage.withJarTask = jar
如果你有一个默认的项目setup，在该项目中，主（main）jar文件被创建和重新打包。并且，你仍旧想创建额外的自定义jars，你可以将自定义的repackage任务结合起来，然后使用dependsOn，这样bootJars任务就会在默认的bootRepackage任务执行以后运行：

	task bootJars
	bootJars.dependsOn = [clientBoot1,clientBoot2,clientBoot3]
	build.dependsOn(bootJars)
上面所有方面经常用于避免一个已经创建的boot jar又被重新打包的情况。重新打包一个存在的boot jar不是什么大问题，但你可能会发现它包含不必要的依赖。

#### 8.3 对其他构建系统的支持
如果想使用除了Maven和Gradle之外的构建工具，你可能需要开发自己的插件。可执行jars需要遵循一个特定格式，并且一些实体需要以不压缩的方式写入（详情查看附录中的[可执行jar格式](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#executable-jar)章节）。

Spring Boot Maven和Gradle插件都利用spring-boot-loader-tools来实际地产生jars。如果需要，你也可以自由地直接使用该库。

##### 8.3.1 重新打包存档
使用org.springframework.boot.loader.tools.Repackager可以将一个存在的存档重新打包，这样它就变成一个自包含的可执行存档。Repackager类需要提供单一的构造器参数，它引用一个存在的jar或war包。使用两个可用的repackage()方法中的一个来替换原始的文件或写入一个新的目标。在repackager运行前还可以设置各种配置。

##### 8.3.2 内嵌的库
当重新打包一个存档时，你可以使用org.springframework.boot.loader.tools.Libraries接口来包含对依赖文件的引用。在这里我们不提供任何该Libraries接口的具体实现，因为它们通常跟具体的构建系统相关。

如果你的存档已经包含libraries，你可以使用Libraries.NONE。

##### 8.3.3 查找main类
如果你没有使用Repackager.setMainClass()指定一个main类，该repackager将使用ASM去读取class文件，然后尝试查找一个合适的，具有public static void main(String[] args)方法的类。如果发现多个候选者，将会抛出异常。

##### 8.3.4 repackage实现示例
这里是一个传统的repackage示例：

	Repackager repackager = new Repackager(sourceJarFile);
	repackager.setBackupSource(false);
	repackager.repackage(new Libraries() {
	            @Override
	            public void doWithLibraries(LibraryCallback callback) throws IOException {
	                // Build system specific implementation, callback for each dependency
	                // callback.library(new Library(nestedFile, LibraryScope.COMPILE));
	            }
	        });



### How-to指南
本章节将回答一些常见的"我该怎么做"类型的问题，这些问题在我们使用Spring Boot时经常遇到。这绝不是一个详尽的列表，但它覆盖了很多方面。

如果遇到一个特殊的我们没有覆盖的问题，你可能想去查看[stackoverflow.com](http://stackoverflow.com/tags/spring-boot)，看是否有人已经给出了答案;这也是一个很好的提新问题的地方（请使用spring-boot标签）。

我们也乐意扩展本章节;如果想添加一个'how-to'，你可以给我们发一个[pull请求](http://github.com/spring-projects/spring-boot/tree/master)。

#### 9.1 Spring Boot应用
##### 9.1.1 解决自动配置问题
Spring Boot自动配置总是尝试尽最大努力去做正确的事，但有时候会失败并且很难说出失败原因。

在每个Spring Boot ApplicationContext中都存在一个相当有用的ConditionEvaluationReport。如果开启DEBUG日志输出，你将会看到它。如果你使用spring-boot-actuator，则会有一个autoconfig的端点，它将以JSON形式渲染该报告。可以使用它调试应用程序，并能查看Spring Boot运行时都添加了哪些特性（及哪些没添加）。

通过查看源码和javadoc可以获取更多问题的答案。以下是一些经验：

* 查找名为* AutoConfiguration的类并阅读源码，特别是@Conditional*注解，这可以帮你找出它们启用哪些特性及何时启用。 将--debug添加到命令行或添加系统属性-Ddebug可以在控制台查看日志，该日志会记录你的应用中所有自动配置的决策。在一个运行的Actuator app中，通过查看autoconfig端点（/autoconfig或等效的JMX）可以获取相同信息。
* 查找是@ConfigurationProperties的类（比如ServerProperties）并看下有哪些可用的外部配置选项。@ConfigurationProperties类有一个用于充当外部配置前缀的name属性，因此ServerProperties的值为prefix="server"，它的配置属性有server.port，server.address等。在运行的Actuator应用中可以查看configprops端点。
* 查看使用RelaxedEnvironment明确地将配置从Environment暴露出去。它经常会使用一个前缀。
* 查看@Value注解，它直接绑定到Environment。相比RelaxedEnvironment，这种方式稍微缺乏灵活性，但它也允许松散的绑定，特别是OS环境变量（所以CAPITALS_AND_UNDERSCORES是period.separated的同义词）。
* 查看@ConditionalOnExpression注解，它根据SpEL表达式的结果来开启或关闭特性，通常使用解析自Environment的占位符进行计算。

##### 9.1.2 启动前自定义Environment或ApplicationContext
每个SpringApplication都有ApplicationListeners和ApplicationContextInitializers，用于自定义上下文（context）或环境(environment)。Spring Boot从META-INF/spring.factories下加载很多这样的内部使用的自定义。有很多方法可以注册其他的自定义：

* 以编程方式为每个应用注册自定义，通过在SpringApplication运行前调用它的addListeners和addInitializers方法来实现。
* 以声明方式为每个应用注册自定义，通过设置context.initializer.classes或context.listener.classes来实现。
* 以声明方式为所有应用注册自定义，通过添加一个META-INF/spring.factories并打包成一个jar文件（该应用将它作为一个库）来实现。

SpringApplication会给监听器（即使是在上下文被创建之前就存在的）发送一些特定的ApplicationEvents，然后也会注册监听ApplicationContext发布的事件的监听器。查看Spring Boot特性章节中的`Section 22.4, “Application events and listeners”` 可以获取一个完整列表。

##### 9.1.4 创建一个非web（non-web）应用
不是所有的Spring应用都必须是web应用（或web服务）。如果你想在main方法中执行一些代码，但需要启动一个Spring应用去设置需要的底层设施，那使用Spring Boot的SpringApplication特性可以很容易实现。SpringApplication会根据它是否需要一个web应用来改变它的ApplicationContext类。首先你需要做的是去掉servlet API依赖，如果不能这样做（比如，基于相同的代码运行两个应用），那你可以明确地调用SpringApplication.setWebEnvironment(false)或设置applicationContextClass属性（通过Java API或使用外部配置）。你想运行的，作为业务逻辑的应用代码可以实现为一个CommandLineRunner，并将上下文降级为一个@Bean定义。

#### 9.2 属性&配置
##### 9.2.1 外部化SpringApplication配置
SpringApplication已经被属性化（主要是setters），所以你可以在创建应用时使用它的Java API修改它的行为。或者你可以使用properties文件中的spring.main.*来外部化（在应用代码外配置）这些配置。比如，在application.properties中可能会有以下内容：

	spring.main.web_environment=false
	spring.main.show_banner=false
然后Spring Boot在启动时将不会显示banner，并且该应用也不是一个web应用。

##### 9.2.2 改变应用程序外部配置文件的位置
默认情况下，来自不同源的属性以一个定义好的顺序添加到Spring的Environment中（查看'Sprin Boot特性'章节的`Chapter 23, Externalized Configuration`获取精确的顺序）。

为应用程序源添加@PropertySource注解是一种很好的添加和修改源顺序的方法。传递给SpringApplication静态便利设施（convenience）方法的类和使用setSources()添加的类都会被检查，以查看它们是否有@PropertySources，如果有，这些属性会被尽可能早的添加到Environment里，以确保ApplicationContext生命周期的所有阶段都能使用。以这种方式添加的属性优先于任何使用默认位置添加的属性，但低于系统属性，环境变量或命令行参数。

你也可以提供系统属性（或环境变量）来改变该行为：

* spring.config.name（SPRING_CONFIG_NAME）是根文件名，默认为application。
* spring.config.location（SPRING_CONFIG_LOCATION）是要加载的文件（例如，一个classpath资源或一个URL）。Spring Boot为该文档设置一个单独的Environment属性，它可以被系统属性，环境变量或命令行参数覆盖。

不管你在environment设置什么，Spring Boot都将加载上面讨论过的application.properties。如果使用YAML，那具有'.yml'扩展的文件默认也会被添加到该列表。

详情参考ConfigFileApplicationListener

##### 9.2.3 使用'short'命令行参数
有些人喜欢使用（例如）--port=9000代替--server.port=9000来设置命令行配置属性。你可以通过在application.properties中使用占位符来启用该功能，比如：

	server.port=${port:8080}
注：如果你继承自spring-boot-starter-parent POM，为了防止和Spring-style的占位符产生冲突，maven-resources-plugins默认的过滤令牌（filter token）已经从${*}变为@（即@maven.token@代替了${maven.token}）。如果已经直接启用maven对application.properties的过滤，你可能也想使用[其他的分隔符](http://maven.apache.org/plugins/maven-resources-plugin/resources-mojo.html#delimiters)替换默认的过滤令牌。

注：在这种特殊的情况下，端口绑定能够在一个PaaS环境下工作，比如Heroku和Cloud Foundry，因为在这两个平台中PORT环境变量是自动设置的，并且Spring能够绑定Environment属性的大写同义词。

##### 9.2.4 使用YAML配置外部属性
YAML是JSON的一个超集，可以非常方便的将外部配置以层次结构形式存储起来。比如：

	spring:
	    application:
	        name: cruncher
	    datasource:
	        driverClassName: com.mysql.jdbc.Driver
	        url: jdbc:mysql://localhost/test
	server:
	    port: 9000
创建一个application.yml文件，将它放到classpath的根目录下，并添加snakeyaml依赖（Maven坐标为org.yaml:snakeyaml，如果你使用spring-boot-starter那就已经被包含了）。一个YAML文件会被解析为一个Java Map<String,Object>（和一个JSON对象类似），Spring Boot会平伸该map，这样它就只有1级深度，并且有period-separated的keys，跟人们在Java中经常使用的Properties文件非常类似。 上面的YAML示例对应于下面的application.properties文件：

	spring.application.name=cruncher
	spring.datasource.driverClassName=com.mysql.jdbc.Driver
	spring.datasource.url=jdbc:mysql://localhost/test
	server.port=9000
查看'Spring Boot特性'章节的Section 23.6, “Using YAML instead of Properties”可以获取更多关于YAML的信息。

##### 9.2.5 设置生效的Spring profiles
Spring Environment有一个API可以设置生效的profiles，但通常你会设置一个系统profile（spring.profiles.active）或一个OS环境变量（SPRING_PROFILES_ACTIVE）。比如，使用一个-D参数启动应用程序（记着把它放到main类或jar文件之前）：

	$ java -jar -Dspring.profiles.active=production demo-0.0.1-SNAPSHOT.jar
在Spring Boot中，你也可以在application.properties里设置生效的profile，例如：

	spring.profiles.active=production
通过这种方式设置的值会被系统属性或环境变量替换，但不会被SpringApplicationBuilder.profiles()方法替换。因此，后面的Java API可用来在不改变默认设置的情况下增加profiles。

想要获取更多信息可查看'Spring Boot特性'章节的`Chapter 24, Profiles`。

##### 9.2.6 根据环境改变配置
一个YAML文件实际上是一系列以---线分割的文档，每个文档都被单独解析为一个平坦的（flattened）map。

如果一个YAML文档包含一个spring.profiles关键字，那profiles的值（以逗号分割的profiles列表）将被传入Spring的Environment.acceptsProfiles()方法，并且如果这些profiles的任何一个被激活，对应的文档被包含到最终的合并中（否则不会）。

示例：

	server:
	    port: 9000
	---

	spring:
	    profiles: development
	server:
	    port: 9001

	---

	spring:
	    profiles: production
	server:
	    port: 0
在这个示例中，默认的端口是9000，但如果Spring profile 'development'生效则该端口是9001，如果'production'生效则它是0。

YAML文档以它们遇到的顺序合并（所以后面的值会覆盖前面的值）。

想要使用profiles文件完成同样的操作，你可以使用application-${profile}.properties指定特殊的，profile相关的值。

##### 9.2.7 发现外部属性的内置选项
Spring Boot在运行时将来自application.properties（或.yml）的外部属性绑定进一个应用中。在一个地方不可能存在详尽的所有支持属性的列表（技术上也是不可能的），因为你的classpath下的其他jar文件也能够贡献。

每个运行中且有Actuator特性的应用都会有一个configprops端点，它能够展示所有边界和可通过@ConfigurationProperties绑定的属性。

附录中包含一个[application.properties](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#common-application-properties)示例，它列举了Spring Boot支持的大多数常用属性。获取权威列表可搜索@ConfigurationProperties和@Value的源码，还有不经常使用的RelaxedEnvironment。


#### 9.3 内嵌的servlet容器
##### 9.3.1 为应用添加Servlet，Filter或ServletContextListener
Servlet规范支持的Servlet，Filter，ServletContextListener和其他监听器可以作为@Bean定义添加到你的应用中。需要格外小心的是，它们不会引起太多的其他beans的热初始化，因为在应用生命周期的早期它们已经被安装到容器里了（比如，让它们依赖你的DataSource或JPA配置就不是一个好主意）。你可以通过延迟初始化它们到第一次使用而不是初始化时来突破该限制。

在Filters和Servlets的情况下，你也可以通过添加一个FilterRegistrationBean或ServletRegistrationBean代替或以及底层的组件来添加映射（mappings）和初始化参数。

##### 9.3.2 改变HTTP端口
在一个单独的应用中，主HTTP端口默认为8080，但可以使用server.port设置（比如，在application.properties中或作为一个系统属性）。由于Environment值的宽松绑定，你也可以使用SERVER_PORT（比如，作为一个OS环境变）。

为了完全关闭HTTP端点，但仍创建一个WebApplicationContext，你可以设置server.port=-1（测试时可能有用）。

想获取更多详情可查看'Spring Boot特性'章节的`Section 26.3.3, “Customizing embedded servlet containers”`，或`ServerProperties`源码。

##### 9.3.3 使用随机未分配的HTTP端口
想扫描一个未使用的端口（为了防止冲突使用OS本地端口）可以使用server.port=0。

##### 9.3.4 发现运行时的HTTP端口
你可以通过日志输出或它的EmbeddedServletContainer的EmbeddedWebApplicationContext获取服务器正在运行的端口。获取和确认服务器已经初始化的最好方式是添加一个`ApplicationListener<EmbeddedServletContainerInitializedEvent>`类型的@Bean，然后当事件发布时将容器pull出来。

使用@WebIntegrationTests的一个有用实践是设置server.port=0，然后使用@Value注入实际的（'local'）端口。例如：

	@RunWith(SpringJUnit4ClassRunner.class)
	@SpringApplicationConfiguration(classes = SampleDataJpaApplication.class)
	@WebIntegrationTest("server.port:0")
	public class CityRepositoryIntegrationTests {

	    @Autowired
	    EmbeddedWebApplicationContext server;

	    @Value("${local.server.port}")
	    int port;

	    // ...

	}

##### 9.3.5 配置SSL
SSL能够以声明方式进行配置，一般通过在application.properties或application.yml设置各种各样的server.ssl.*属性。例如：

	server.port = 8443
	server.ssl.key-store = classpath:keystore.jks
	server.ssl.key-store-password = secret
	server.ssl.key-password = another-secret
获取所有支持的配置详情可查看[Ssl](http://github.com/spring-projects/spring-boot/tree/master/spring-boot/src/main/java/org/springframework/boot/context/embedded/Ssl.java)。

注：Tomcat要求key存储（如果你正在使用一个可信存储）能够直接在文件系统上访问，即它不能从一个jar文件内读取。Jetty和Undertow没有该限制。

使用类似于以上示例的配置意味着该应用将不在支持端口为8080的普通HTTP连接。Spring Boot不支持通过application.properties同时配置HTTP连接器和HTTPS连接器。如果你两个都想要，那就需要以编程的方式配置它们中的一个。推荐使用application.properties配置HTTPS，因为HTTP连接器是两个中最容易以编程方式进行配置的。获取示例可查看[spring-boot-sample-tomcat-multi-connectors](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat-multi-connectors)示例项目。

##### 9.3.6 配置Tomcat
通常你可以遵循Section 63.7, `“Discover built-in options for external properties”`关于@ConfigurationProperties（这里主要的是ServerProperties）的建议，但也看下EmbeddedServletContainerCustomizer和各种你可以添加的Tomcat-specific的*Customizers。

Tomcat APIs相当丰富，一旦获取到TomcatEmbeddedServletContainerFactory，你就能够以多种方式修改它。或核心选择是添加你自己的TomcatEmbeddedServletContainerFactory。

##### 9.3.7 启用Tomcat的多连接器（Multiple Connectors）
你可以将一个`org.apache.catalina.connector.Connector`添加到TomcatEmbeddedServletContainerFactory，这就能够允许多连接器，比如HTTP和HTTPS连接器：

	@Bean
	public EmbeddedServletContainerFactory servletContainer() {
	    TomcatEmbeddedServletContainerFactory tomcat = new TomcatEmbeddedServletContainerFactory();
	    tomcat.addAdditionalTomcatConnectors(createSslConnector());
	    return tomcat;
	}

	private Connector createSslConnector() {
	    Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
	    Http11NioProtocol protocol = (Http11NioProtocol) connector.getProtocolHandler();
	    try {
	        File keystore = new ClassPathResource("keystore").getFile();
	        File truststore = new ClassPathResource("keystore").getFile();
	        connector.setScheme("https");
	        connector.setSecure(true);
	        connector.setPort(8443);
	        protocol.setSSLEnabled(true);
	        protocol.setKeystoreFile(keystore.getAbsolutePath());
	        protocol.setKeystorePass("changeit");
	        protocol.setTruststoreFile(truststore.getAbsolutePath());
	        protocol.setTruststorePass("changeit");
	        protocol.setKeyAlias("apitester");
	        return connector;
	    }
	    catch (IOException ex) {
	        throw new IllegalStateException("can't access keystore: [" + "keystore"
	                + "] or truststore: [" + "keystore" + "]", ex);
	    }
	}


##### 9.3.8 在前端代理服务器后使用Tomcat
Spring Boot将自动配置Tomcat的RemoteIpValve，如果你启用它的话。这允许你透明地使用标准的x-forwarded-for和x-forwarded-proto头，很多前端代理服务器都会添加这些头信息（headers）。通过将这些属性中的一个或全部设置为非空的内容来开启该功能（它们是大多数代理约定的值，如果你只设置其中的一个，则另一个也会被自动设置）。

	server.tomcat.remote_ip_header=x-forwarded-for
	server.tomcat.protocol_header=x-forwarded-proto
如果你的代理使用不同的头部（headers），你可以通过向application.properties添加一些条目来自定义该值的配置，比如：

	server.tomcat.remote_ip_header=x-your-remote-ip-header
	server.tomcat.protocol_header=x-your-protocol-header
该值也可以配置为一个默认的，能够匹配信任的内部代理的正则表达式。默认情况下，受信任的IP包括 10/8, 192.168/16, 169.254/16 和 127/8。可以通过向application.properties添加一个条目来自定义该值的配置，比如：

	server.tomcat.internal_proxies=192\\.168\\.\\d{1,3}\\.\\d{1,3}
注：只有在你使用一个properties文件作为配置的时候才需要双反斜杠。如果你使用YAML，单个反斜杠就足够了，192\.168\.\d{1,3}\.\d{1,3}和上面的等价。

另外，通过在一个`TomcatEmbeddedServletContainerFactory` bean中配置和添加RemoteIpValve，你就可以完全控制它的设置了。

##### 9.3.9 使用Jetty替代Tomcat
Spring Boot starters（特别是spring-boot-starter-web）默认都是使用Tomcat作为内嵌容器的。你需要排除那些Tomcat的依赖并包含Jetty的依赖。为了让这种处理尽可能简单，Spring Boot将Tomcat和Jetty的依赖捆绑在一起，然后提供单独的starters。

Maven示例：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-web</artifactId>
	    <exclusions>
	        <exclusion>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-tomcat</artifactId>
	        </exclusion>
	    </exclusions>
	</dependency>
	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-jetty</artifactId>
	</dependency>
Gradle示例：

	configurations {
	    compile.exclude module: "spring-boot-starter-tomcat"
	}

	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web:1.3.0.BUILD-SNAPSHOT")
	    compile("org.springframework.boot:spring-boot-starter-jetty:1.3.0.BUILD-SNAPSHOT")
	    // ...
	}

##### 9.3.10 配置jetty
通常你可以遵循[Section 63.7, “Discover built-in options for external properties”](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto-discover-build-in-options-for-external-properties)关于@ConfigurationProperties（此处主要是ServerProperties）的建议，但也要看下EmbeddedServletContainerCustomizer。Jetty API相当丰富，一旦获取到JettyEmbeddedServletContainerFactory，你就可以使用很多方式修改它。或更彻底地就是添加你自己的JettyEmbeddedServletContainerFactory。

##### 9.3.11 使用Undertow替代Tomcat

使用Undertow替代Tomcat和使用Jetty替代Tomcat非常类似。你需要排除Tomat依赖，并包含Undertow starter。

Maven示例：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-web</artifactId>
	    <exclusions>
	        <exclusion>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-tomcat</artifactId>
	        </exclusion>
	    </exclusions>
	</dependency>
	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-undertow</artifactId>
	</dependency>
Gradle示例：

	configurations {
	    compile.exclude module: "spring-boot-starter-tomcat"
	}

	dependencies {
	    compile 'org.springframework.boot:spring-boot-starter-web:1.3.0.BUILD-SNAPSHOT")
	    compile 'org.springframework.boot:spring-boot-starter-undertow:1.3.0.BUILD-SNAPSHOT")
	    // ...
	}


##### 9.3.12 配置Undertow
通常你可以遵循[Section 63.7, “Discover built-in options for external properties”](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto-discover-build-in-options-for-external-properties)关于@ConfigurationProperties（此处主要是ServerProperties和ServerProperties.Undertow），但也要看下EmbeddedServletContainerCustomizer。一旦获取到UndertowEmbeddedServletContainerFactory，你就可以使用一个UndertowBuilderCustomizer修改Undertow的配置以满足你的需求。或更彻底地就是添加你自己的UndertowEmbeddedServletContainerFactory。

##### 9.3.13 启用Undertow的多监听器（Multiple Listeners）

往`UndertowEmbeddedServletContainerFactory`添加一个`UndertowBuilderCustomizer`，然后添加一个监听者到Builder：

	@Bean
	public UndertowEmbeddedServletContainerFactory embeddedServletContainerFactory() {
	    UndertowEmbeddedServletContainerFactory factory = new UndertowEmbeddedServletContainerFactory();
	    factory.addBuilderCustomizers(new UndertowBuilderCustomizer() {

	        @Override
	        public void customize(Builder builder) {
	            builder.addHttpListener(8080, "0.0.0.0");
	        }

	    });
	    return factory;
	}


##### 9.3.14 使用Tomcat7
Tomcat7可用于Spring Boot，但默认使用的是Tomcat8。如果不能使用Tomcat8（例如，你使用的是Java1.6），你需要改变classpath去引用Tomcat7。

###### 9.3.14.1 通过Maven使用Tomcat7

如果正在使用starter pom和parent，你只需要改变Tomcat的version属性，比如，对于一个简单的webapp或service：

	<properties>
	    <tomcat.version>7.0.59</tomcat.version>
	</properties>
	<dependencies>
	    ...
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-web</artifactId>
	    </dependency>
	    ...
	</dependencies>

###### 9.3.14.2  通过Gradle使用Tomcat7
你可以通过设置tomcat.version属性改变Tomcat的版本：

	ext['tomcat.version'] = '7.0.59'
	dependencies {
	    compile 'org.springframework.boot:spring-boot-starter-web'
	}

##### 9.3.15  使用Jetty8
Jetty8可用于Spring Boot，但默认使用的是Jetty9。如果不能使用Jetty9（例如，因为你使用的是Java1.6），你只需改变classpath去引用Jetty8。你也需要排除Jetty的WebSocket相关的依赖。

###### 9.3.15.1 通过Maven使用Jetty8
如果正在使用starter pom和parent，你只需添加Jetty starter，去掉WebSocket依赖，并改变version属性，比如，对于一个简单的webapp或service：

	<properties>
	    <jetty.version>8.1.15.v20140411</jetty.version>
	    <jetty-jsp.version>2.2.0.v201112011158</jetty-jsp.version>
	</properties>
	<dependencies>
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-web</artifactId>
	        <exclusions>
	            <exclusion>
	                <groupId>org.springframework.boot</groupId>
	                <artifactId>spring-boot-starter-tomcat</artifactId>
	            </exclusion>
	        </exclusions>
	    </dependency>
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-jetty</artifactId>
	        <exclusions>
	            <exclusion>
	                <groupId>org.eclipse.jetty.websocket</groupId>
	                <artifactId>*</artifactId>
	            </exclusion>
	        </exclusions>
	    </dependency>
	</dependencies>

###### 9.3.15.2 通过Gradle使用Jetty8
你可以设置jetty.version属性并排除相关的WebSocket依赖，比如对于一个简单的webapp或service：

	ext['jetty.version'] = '8.1.15.v20140411'
	dependencies {
	    compile ('org.springframework.boot:spring-boot-starter-web') {
	        exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
	    }
	    compile ('org.springframework.boot:spring-boot-starter-jetty') {
	        exclude group: 'org.eclipse.jetty.websocket'
	    }
	}

##### 9.3.16 使用@ServerEndpoint创建WebSocket端点
如果想在一个使用内嵌容器的Spring Boot应用中使用@ServerEndpoint，你需要声明一个单独的ServerEndpointExporter @Bean：

	@Bean
	public ServerEndpointExporter serverEndpointExporter() {
	    return new ServerEndpointExporter();
	}
该bean将用底层的WebSocket容器注册任何的被@ServerEndpoint注解的beans。当部署到一个单独的servlet容器时，该角色将被一个servlet容器初始化方法履行，ServerEndpointExporter bean也就不是必需的了。

##### 9.3.17 启用HTTP响应压缩
Spring Boot提供两种启用HTTP压缩的机制;一种是Tomcat特有的，另一种是使用一个filter，可以配合Jetty，Tomcat和Undertow。

###### 9.3.17.1 启用Tomcat的HTTP响应压缩
Tomcat对HTTP响应压缩提供内建支持。默认是禁用的，但可以通过application.properties轻松的启用：

	server.tomcat.compression: on
当设置为on时，Tomcat将压缩响应的长度至少为2048字节。你可以配置一个整型值来设置该限制而不只是on，比如：

	server.tomcat.compression: 4096
默认情况下，Tomcat只压缩某些MIME类型的响应（text/html，text/xml和text/plain）。你可以使用server.tomcat.compressableMimeTypes属性进行自定义，比如：

	server.tomcat.compressableMimeTypes=application/json,application/xml

###### 9.3.17.2 使用GzipFilter开启HTTP响应压缩
如果你正在使用Jetty或Undertow，或想要更精确的控制HTTP响应压缩，Spring Boot为Jetty的GzipFilter提供自动配置。虽然该过滤器是Jetty的一部分，但它也兼容Tomcat和Undertow。想要启用该过滤器，只需简单的为你的应用添加org.eclipse.jetty:jetty-servlets依赖。

GzipFilter可以使用spring.http.gzip.*属性进行配置。具体参考[GzipFilterProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/GzipFilterProperties.java)。

#### 9.4 Spring MVC
##### 9.4.1 编写一个JSON REST服务
在Spring Boot应用中，任何Spring @RestController默认应该渲染为JSON响应，只要classpath下存在Jackson2。例如：

	@RestController
	public class MyController {

	    @RequestMapping("/thing")
	    public MyThing thing() {
	            return new MyThing();
	    }

	}
只要MyThing能够通过Jackson2序列化（比如，一个标准的POJO或Groovy对象），localhost:8080/thing默认响应一个JSON表示。有时在一个浏览器中你可能看到XML响应因为浏览器倾向于发送XML 响应头。

##### 9.4.2 编写一个XML REST服务
如果classpath下存在Jackson XML扩展（jackson-dataformat-xml），它会被用来渲染XML响应，示例和JSON的非常相似。想要使用它，只需为你的项目添加以下的依赖：

	<dependency>
	    <groupId>com.fasterxml.jackson.dataformat</groupId>
	    <artifactId>jackson-dataformat-xml</artifactId>
	</dependency>
你可能也想添加对Woodstox的依赖。它比JDK提供的默认Stax实现快很多，并且支持良好的格式化输出，提高了namespace处理能力：

	<dependency>
	    <groupId>org.codehaus.woodstox</groupId>
	    <artifactId>woodstox-core-asl</artifactId>
	</dependency>
如果Jackson的XML扩展不可用，Spring Boot将使用JAXB（JDK默认提供），不过你需要为MyThing添加额外的注解@XmlRootElement：

	@XmlRootElement
	public class MyThing {
	    private String name;
	    // .. getters and setters
	}
想要服务器渲染XML而不是JSON，你可能需要发送一个Accept: text/xml头部（或使用浏览器）。

##### 9.4.3 自定义Jackson ObjectMapper
在一个HTTP交互中，Spring MVC（客户端和服务端）使用HttpMessageConverters协商内容转换。如果classpath下存在Jackson，你就已经获取到Jackson2ObjectMapperBuilder提供的默认转换器。

创建的ObjectMapper（或用于Jackson XML转换的XmlMapper）实例默认有以下自定义属性：

* MapperFeature.DEFAULT_VIEW_INCLUSION禁用
* DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES禁用

Spring Boot也有一些简化自定义该行为的特性。

你可以使用当前的environment配置ObjectMapper和XmlMapper实例。Jackson提供一个扩展套件，可以用来简单的关闭或开启一些特性，你可以用它们配置Jackson处理的不同方面。这些特性在Jackson中使用5个枚举进行描述的，并被映射到environment的属性上：

|Jackson枚举	|Environment属性 |
|:---|:----|
|com.fasterxml.jackson.databind.DeserializationFeature	|`spring.jackson.deserialization.=true	|false`|
|com.fasterxml.jackson.core.JsonGenerator.Feature|	`spring.jackson.generator.=true	|false`|
|com.fasterxml.jackson.databind.MapperFeature	|`spring.jackson.mapper.=true	|false`|
|com.fasterxml.jackson.core.JsonParser.Feature	|`spring.jackson.parser.=true	|false`|
|com.fasterxml.jackson.databind.SerializationFeature	|`spring.jackson.serialization.=true	|false`|

例如，设置spring.jackson.serialization.indent_output=true可以开启漂亮打印。注意，由于松绑定的使用，indent_output不必匹配对应的枚举常量INDENT_OUTPUT。

如果想彻底替换默认的ObjectMapper，你需要定义一个该类型的@Bean并将它标记为@Primary。

定义一个Jackson2ObjectMapperBuilder类型的@Bean将允许你自定义默认的ObjectMapper和XmlMapper（分别用于MappingJackson2HttpMessageConverter和MappingJackson2XmlHttpMessageConverter）。

另一种自定义Jackson的方法是向你的上下文添加com.fasterxml.jackson.databind.Module类型的beans。它们会被注册入每个ObjectMapper类型的bean，当为你的应用添加新特性时，这就提供了一种全局机制来贡献自定义模块。

最后，如果你提供任何MappingJackson2HttpMessageConverter类型的@Beans，那它们将替换MVC配置中的默认值。同时，也提供一个HttpMessageConverters类型的bean，它有一些有用的方法可以获取默认的和用户增强的message转换器。

想要获取更多细节可查看[Section 65.4, “Customize the @ResponseBody rendering”](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto-customize-the-responsebody-rendering)和[WebMvcAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/WebMvcAutoConfiguration.java)源码。

##### 9.4.4 自定义@ResponseBody渲染
Spring使用HttpMessageConverters渲染@ResponseBody（或来自@RestController的响应）。你可以通过在Spring Boot上下文中添加该类型的beans来贡献其他的转换器。如果你添加的bean类型默认已经包含了（像用于JSON转换的MappingJackson2HttpMessageConverter），那它将替换默认的。Spring Boot提供一个方便的HttpMessageConverters类型的bean，它有一些有用的方法可以访问默认的和用户增强的message转换器（有用，比如你想要手动将它们注入到一个自定义的RestTemplate）。

在通常的MVC用例中，任何你提供的WebMvcConfigurerAdapter beans通过覆盖configureMessageConverters方法也能贡献转换器，但不同于通常的MVC，你可以只提供你需要的转换器（因为Spring Boot使用相同的机制来贡献它默认的转换器）。最终，如果你通过提供自己的@EnableWebMvc注解覆盖Spring Boot默认的MVC配置，那你就可以完全控制，并使用来自WebMvcConfigurationSupport的getMessageConverters手动做任何事。

具体参考[WebMvcAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/WebMvcAutoConfiguration.java)源码。

##### 9.4.5 处理Multipart文件上传
Spring Boot采用Servlet 3 javax.servlet.http.Part API来支持文件上传。默认情况下，Spring Boot配置Spring MVC在单个请求中每个文件最大1Mb，最多10Mb的文件数据。你可以覆盖那些值，也可以设置临时文件存储的位置（比如，存储到/tmp文件夹下）及传递数据刷新到磁盘的阀值（通过使用MultipartProperties类暴露的属性）。如果你需要设置文件不受限制，例如，可以设置multipart.maxFileSize属性值为-1。

当你想要接收部分（multipart）编码文件数据作为Spring MVC控制器（controller）处理方法中被@RequestParam注解的MultipartFile类型的参数时，multipart支持就非常有用了。

具体参考[MultipartAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/MultipartAutoConfiguration.java)源码。

##### 9.4.6 关闭Spring MVC DispatcherServlet
Spring Boot想要服务来自应用程序root /下的所有内容。如果你想将自己的servlet映射到该目录下也是可以的，但当然你可能失去一些Boot MVC特性。为了添加你自己的servlet，并将它映射到root资源，你只需声明一个Servlet类型的@Bean，并给它特定的bean名称dispatcherServlet（如果只想关闭但不替换它，你可以使用该名称创建不同类型的bean）。

##### 9.4.7 关闭默认的MVC配置
完全控制MVC配置的最简单方式是提供你自己的被@EnableWebMvc注解的@Configuration。这样所有的MVC配置都逃不出你的掌心。

##### 9.4.8 自定义ViewResolvers

ViewResolver是Spring MVC的核心组件，它负责转换@Controller中的视图名称到实际的View实现。注意ViewResolvers主要用在UI应用中，而不是REST风格的服务（View不是用来渲染@ResponseBody的）。Spring有很多你可以选择的ViewResolver实现，并且Spring自己对如何选择相应实现也没发表意见。另一方面，Spring Boot会根据classpath上的依赖和应用上下文为你安装一或两个ViewResolver实现。DispatcherServlet使用所有在应用上下文中找到的解析器（resolvers），并依次尝试每一个直到它获取到结果，所以如果你正在添加自己的解析器，那就要小心顺序和你的解析器添加的位置。

WebMvcAutoConfiguration将会为你的上下文添加以下ViewResolvers：

* bean id为defaultViewResolver的InternalResourceViewResolver。这个会定位可以使用DefaultServlet渲染的物理资源（比如，静态资源和JSP页面）。它在视图（view name）上应用了一个前缀和后缀（默认都为空，但你可以通过spring.view.prefix和spring.view.suffix外部配置设置），然后查找在servlet上下文中具有该路径的物理资源。可以通过提供相同类型的bean覆盖它。
* id为beanNameViewResolver的BeanNameViewResolver。这是视图解析器链的一个非常有用的成员，它可以在View被解析时收集任何具有相同名称的beans。
* id为viewResolver的ContentNegotiatingViewResolver只会在实际View类型的beans出现时添加。这是一个'主'解析器，它的职责会代理给其他解析器，它会尝试找到客户端发送的一个匹配'Accept'的HTTP头部。这有一篇有用的，关于你需要更多了解的ContentNegotiatingViewResolver的博客，也要具体查看下源码。通过定义一个名叫'viewResolver'的bean，你可以关闭自动配置的ContentNegotiatingViewResolver。
* 如果使用Thymeleaf，你将有一个id为thymeleafViewResolver的ThymeleafViewResolver。它会通过加前缀和后缀的视图名来查找资源（外部配置为spring.thymeleaf.prefix和spring.thymeleaf.suffix，对应的默认为'classpath:/templates/'和'.html'）。你可以通过提供相同名称的bean来覆盖它。
* 如果使用FreeMarker，你将有一个id为freeMarkerViewResolver的FreeMarkerViewResolver。它会使用加前缀和后缀（外部配置为spring.freemarker.prefix和spring.freemarker.suffix，对应的默认值为空和'.ftl'）的视图名从加载路径（外部配置为spring.freemarker.templateLoaderPath，默认为'classpath:/templates/'）下查找资源。你可以通过提供一个相同名称的bean来覆盖它。
* 如果使用Groovy模板（实际上只要你把groovy-templates添加到classpath下），你将有一个id为groovyTemplateViewResolver的Groovy TemplateViewResolver。它会使用加前缀和后缀（外部属性为spring.groovy.template.prefix和spring.groovy.template.suffix，对应的默认值为'classpath:/templates/'和'.tpl'）的视图名从加载路径下查找资源。你可以通过提供一个相同名称的bean来覆盖它。
* 如果使用Velocity，你将有一个id为velocityViewResolver的VelocityViewResolver。它会使用加前缀和后缀（外部属性为spring.velocity.prefix和spring.velocity.suffix，对应的默认值为空和'.vm'）的视图名从加载路径（外部属性为spring.velocity.resourceLoaderPath，默认为'classpath:/templates/'）下查找资源。你可以通过提供一个相同名称的bean来覆盖它。

具体参考： [WebMvcAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/WebMvcAutoConfiguration.java)，[ThymeleafAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/thymeleaf/ThymeleafAutoConfiguration.java)，[FreeMarkerAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/thymeleaf/ThymeleafAutoConfiguration.java)，[GroovyTemplateAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/thymeleaf/ThymeleafAutoConfiguration.java)，[VelocityAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/thymeleaf/ThymeleafAutoConfiguration.java)。

#### 9.5 日志
Spring Boot除了commons-logging API外没有其他强制性的日志依赖，你有很多可选的日志实现。想要使用Logback，你需要包含它，及一些对classpath下commons-logging的绑定。最简单的方式是通过依赖spring-boot-starter-logging的starter pom。对于一个web应用程序，你只需添加spring-boot-starter-web依赖，因为它依赖于logging starter。例如，使用Maven：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-web</artifactId>
	</dependency>
Spring Boot有一个LoggingSystem抽象，用于尝试通过classpath上下文配置日志系统。如果Logback可用，则首选它。如果你唯一需要做的就是设置不同日志的级别，那可以通过在application.properties中使用logging.level前缀实现，比如：

	logging.level.org.springframework.web: DEBUG
	logging.level.org.hibernate: ERROR

你也可以使用`logging.file`设置日志文件的位置（除控制台之外，默认会输出到控制台）。

想要对日志系统进行更细粒度的配置，你需要使用正在说的LoggingSystem支持的原生配置格式。默认情况下，Spring Boot从系统的默认位置加载原生配置（比如对于Logback为classpath:logback.xml），但你可以使用`logging.config`属性设置配置文件的位置。

##### 9.5.1 配置Logback
如果你将一个logback.xml放到classpath根目录下，那它将会被从这加载。Spring Boot提供一个默认的基本配置，如果你只是设置日志级别，那你可以包含它，比如：

	<?xml version="1.0" encoding="UTF-8"?>
	<configuration>
	    <include resource="org/springframework/boot/logging/logback/base.xml"/>
	    <logger name="org.springframework.web" level="DEBUG"/>
	</configuration>
如果查看spring-boot jar包中的默认logback.xml，你将会看到LoggingSystem为你创建的很多有用的系统属性，比如：

* ${PID}，当前进程id
* ${LOG_FILE}，如果在Boot外部配置中设置了logging.file
* ${LOG_PATH}，如果设置了logging.path（表示日志文件产生的目录）

Spring Boot也提供使用自定义的Logback转换器在控制台上输出一些漂亮的彩色ANSI日志信息（不是日志文件）。具体参考默认的base.xml配置。

如果Groovy在classpath下，你也可以使用logback.groovy配置Logback。

##### 9.5.2  配置Log4j

Spring Boot也支持Log4j或Log4j 2作为日志配置，但只有在它们中的某个在classpath下存在的情况。如果你正在使用starter poms进行依赖装配，这意味着你需要排除Logback，然后包含你选择的Log4j版本。如果你不使用starter poms，那除了你选择的Log4j版本外还要提供commons-logging（至少）。

最简单的方式可能就是通过starter poms，尽管它需要排除一些依赖，比如，在Maven中：

	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter</artifactId>
	    <exclusions>
	        <exclusion>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-logging</artifactId>
	        </exclusion>
	    </exclusions>
	</dependency>
	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-log4j</artifactId>
	</dependency>
想要使用Log4j 2，只需要依赖spring-boot-starter-log4j2而不是spring-boot-starter-log4j。

注：使用Log4j各版本的starters都会收集好依赖以满足common logging的要求（比如，Tomcat中使用java.util.logging，但使用Log4j或 Log4j 2作为输出）。具体查看Actuator Log4j或Log4j 2的示例，了解如何将它用于实战。

###### 9.5.2.1 使用YAML或JSON配置Log4j2
除了它的默认XML配置格式，Log4j 2也支持YAML和JSON配置文件。想要使用其他配置文件格式来配置Log4j 2，你需要添加合适的依赖到classpath。为了使用YAML，你需要添加com.fasterxml.jackson.dataformat:jackson-dataformat-yaml依赖，Log4j 2将查找名称为log4j2.yaml或log4j2.yml的配置文件。为了使用JSON，你需要添加com.fasterxml.jackson.core:jackson-databind依赖，Log4j 2将查找名称为log4j2.json或log4j2.jsn的配置文件

#### 9.6 数据访问
##### 9.6.1 配置一个数据源
想要覆盖默认的设置只需要定义一个你自己的DataSource类型的@Bean。Spring Boot提供一个工具构建类DataSourceBuilder，可用来创建一个标准的DataSource（如果它处于classpath下），或者仅创建你自己的DataSource，然后将它和在Section 23.7.1, “Third-party configuration”解释的一系列Environment属性绑定。

比如：

	@Bean
	@ConfigurationProperties(prefix="datasource.mine")
	public DataSource dataSource() {
	    return new FancyDataSource();
	}


	datasource.mine.jdbcUrl=jdbc:h2:mem:mydb
	datasource.mine.user=sa
	datasource.mine.poolSize=30
具体参考'Spring Boot特性'章节中的·Section 28.1, “Configure a DataSource”·和[DataSourceAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/DataSourceAutoConfiguration.java)类源码。

##### 9.6.2 配置两个数据源
创建多个数据源和创建第一个工作都是一样的。如果使用针对JDBC或JPA的默认自动配置，你可能想要将其中一个设置为@Primary（然后它就能被任何@Autowired注入获取）。

	@Bean
	@Primary
	@ConfigurationProperties(prefix="datasource.primary")
	public DataSource primaryDataSource() {
	    return DataSourceBuilder.create().build();
	}

	@Bean
	@ConfigurationProperties(prefix="datasource.secondary")
	public DataSource secondaryDataSource() {
	    return DataSourceBuilder.create().build();
	}

##### 9.6.3 使用Spring Data仓库
Spring Data可以为你的@Repository接口创建各种风格的实现。Spring Boot会为你处理所有事情，只要那些@Repositories接口跟你的@EnableAutoConfiguration类处于相同的包（或子包）。

对于很多应用来说，你需要做的就是将正确的Spring Data依赖添加到classpath下（对于JPA有一个spring-boot-starter-data-jpa，对于Mongodb有一个spring-boot-starter-data-mongodb），创建一些repository接口来处理@Entity对象。具体参考[JPA sample](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-data-jpa)或[Mongodb sample](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-data-mongodb)。

Spring Boot会基于它找到的@EnableAutoConfiguration来尝试猜测你的@Repository定义的位置。想要获取更多控制，可以使用@EnableJpaRepositories注解（来自Spring Data JPA）。

##### 9.6.4 从Spring配置分离@Entity定义
Spring Boot会基于它找到的@EnableAutoConfiguration来尝试猜测你的@Entity定义的位置。想要获取更多控制，你可以使用@EntityScan注解，比如：

	@Configuration
	@EnableAutoConfiguration
	@EntityScan(basePackageClasses=City.class)
	public class Application {

	    //...

	}

##### 9.6.5 配置JPA属性
Spring Data JPA已经提供了一些独立的配置选项（比如，针对SQL日志），并且Spring Boot会暴露它们，针对hibernate的外部配置属性也更多些。最常见的选项如下：

	spring.jpa.hibernate.ddl-auto: create-drop
	spring.jpa.hibernate.naming_strategy: org.hibernate.cfg.ImprovedNamingStrategy
	spring.jpa.database: H2
	spring.jpa.show-sql: true
（由于宽松的数据绑定策略，连字符或下划线作为属性keys作用应该是等效的）ddl-auto配置是个特殊情况，它有不同的默认设置，这取决于你是否使用一个内嵌数据库（create-drop）。当本地EntityManagerFactory被创建时，所有spring.jpa.properties.*属性都被作为正常的JPA属性（去掉前缀）传递进去了。

具体参考[HibernateJpaAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaAutoConfiguration.java)和[JpaBaseConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/orm/jpa/JpaBaseConfiguration.java)。

##### 9.6.6 使用自定义的EntityManagerFactory
为了完全控制EntityManagerFactory的配置，你需要添加一个名为entityManagerFactory的@Bean。Spring Boot自动配置会根据是否存在该类型的bean来关闭它的实体管理器（entity manager）。

##### 9.6.7 使用两个EntityManagers
即使默认的EntityManagerFactory工作的很好，你也需要定义一个新的EntityManagerFactory，因为一旦出现第二个该类型的bean，默认的将会被关闭。为了轻松的实现该操作，你可以使用Spring Boot提供的EntityManagerBuilder，或者如果你喜欢的话可以直接使用来自Spring ORM的LocalContainerEntityManagerFactoryBean。

示例：

	// add two data sources configured as above

	@Bean
	public LocalContainerEntityManagerFactoryBean customerEntityManagerFactory(
	        EntityManagerFactoryBuilder builder) {
	    return builder
	            .dataSource(customerDataSource())
	            .packages(Customer.class)
	            .persistenceUnit("customers")
	            .build();
	}

	@Bean
	public LocalContainerEntityManagerFactoryBean orderEntityManagerFactory(
	        EntityManagerFactoryBuilder builder) {
	    return builder
	            .dataSource(orderDataSource())
	            .packages(Order.class)
	            .persistenceUnit("orders")
	            .build();
	}

上面的配置靠自己基本可以运行。想要完成作品你也需要为两个EntityManagers配置TransactionManagers。其中的一个会被Spring Boot默认的JpaTransactionManager获取，如果你将它标记为@Primary。另一个需要显式注入到一个新实例。或你可以使用一个JTA事物管理器生成它两个。

##### 9.6.8 使用普通的persistence.xml
Spring不要求使用XML配置JPA提供者（provider），并且Spring Boot假定你想要充分利用该特性。如果你倾向于使用persistence.xml，那你需要定义你自己的id为'entityManagerFactory'的LocalEntityManagerFactoryBean类型的@Bean，并在那设置持久化单元的名称。

默认设置可查看[JpaBaseConfiguration](https://github.com/spring-projects/spring-boot/blob/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/orm/jpa/JpaBaseConfiguration.java)

##### 9.6.9 使用Spring Data JPA和Mongo仓库

Spring Data JPA和Spring Data Mongo都能自动为你创建Repository实现。如果它们同时出现在classpath下，你可能需要添加额外的配置来告诉Spring Boot你想要哪个（或两个）为你创建仓库。最明确地方式是使用标准的Spring Data @Enable* Repositories，然后告诉它你的Repository接口的位置（此处*即可以是Jpa，也可以是Mongo，或者两者都是）。

这里也有spring.data.*.repositories.enabled标志，可用来在外部配置中开启或关闭仓库的自动配置。这在你想关闭Mongo仓库，但仍旧使用自动配置的MongoTemplate时非常有用。

相同的障碍和特性也存在于其他自动配置的Spring Data仓库类型（Elasticsearch, Solr）。只需要改变对应注解的名称和标志。

##### 9.6.10 将Spring Data仓库暴露为REST端点
Spring Data REST能够将Repository的实现暴露为REST端点，只要该应用启用Spring MVC。

Spring Boot暴露一系列来自spring.data.rest命名空间的有用属性来定制化RepositoryRestConfiguration。如果需要提供其他定制，你可以创建一个继承自[SpringBootRepositoryRestMvcConfiguration](http://docs.spring.io/spring-data/rest/docs/current/api/org/springframework/data/rest/core/config/RepositoryRestConfiguration.html)的@Configuration类。该类功能和RepositoryRestMvcConfiguration相同，但允许你继续使用spring.data.rest.*属性。

#### 9.7 数据库初始化
一个数据库可以使用不同的方式进行初始化，这取决于你的技术栈。或者你可以手动完成该任务，只要数据库是单独的过程。

##### 9.7.1 使用JPA初始化数据库
JPA有个生成DDL的特性，这些可以设置为在数据库启动时运行。这可以通过两个外部属性进行控制：

* spring.jpa.generate-ddl（boolean）控制该特性的关闭和开启，跟实现者没关系
* spring.jpa.hibernate.ddl-auto（enum）是一个Hibernate特性，用于更细力度的控制该行为。更多详情参考以下内容。

##### 9.7.2 使用Hibernate初始化数据库
你可以显式设置spring.jpa.hibernate.ddl-auto，标准的Hibernate属性值有none，validate，update，create，create-drop。Spring Boot根据你的数据库是否为内嵌数据库来选择相应的默认值，如果是内嵌型的则默认值为create-drop，否则为none。通过查看Connection类型可以检查是否为内嵌型数据库，hsqldb，h2和derby是内嵌的，其他都不是。当从内存数据库迁移到一个真正的数据库时，你需要当心，在新的平台中不能对数据库表和数据是否存在进行臆断。你也需要显式设置ddl-auto，或使用其他机制初始化数据库。

此外，启动时处于classpath根目录下的import.sql文件会被执行。这在demos或测试时很有用，但在生产环境中你可能不期望这样。这是Hibernate的特性，和Spring没有一点关系。

##### 9.7.3 使用Spring JDBC初始化数据库

Spring JDBC有一个DataSource初始化特性。Spring Boot默认启用了该特性，并从标准的位置schema.sql和data.sql（位于classpath根目录）加载SQL。此外，Spring Boot将加载schema-${platform}.sql和data-${platform}.sql文件（如果存在），在这里platform是spring.datasource.platform的值，比如，你可以将它设置为数据库的供应商名称（hsqldb, h2, oracle, mysql, postgresql等）。Spring Boot默认启用Spring JDBC初始化快速失败特性，所以如果脚本导致异常产生，那应用程序将启动失败。脚本的位置可以通过设置spring.datasource.schema和spring.datasource.data来改变，如果设置spring.datasource.initialize=false则哪个位置都不会被处理。

你可以设置spring.datasource.continueOnError=true禁用快速失败特性。一旦应用程序成熟并被部署了很多次，那该设置就很有用，因为脚本可以充当"可怜人的迁移"-例如，插入失败时意味着数据已经存在，也就没必要阻止应用继续运行。

如果你想要在一个JPA应用中使用schema.sql，那如果Hibernate试图创建相同的表，ddl-auto=create-drop将导致错误产生。为了避免那些错误，可以将ddl-auto设置为“”（推荐）或“none”。不管是否使用ddl-auto=create-drop，你总可以使用data.sql初始化新数据。

##### 9.7.4 初始化Spring Batch数据库
如果你正在使用Spring Batch，那么它会为大多数的流行数据库平台预装SQL初始化脚本。Spring Boot会检测你的数据库类型，并默认执行那些脚本，在这种情况下将关闭快速失败特性（错误被记录但不会阻止应用启动）。这是因为那些脚本是可信任的，通常不会包含bugs，所以错误会被忽略掉，并且对错误的忽略可以让脚本具有幂等性。你可以使用spring.batch.initializer.enabled=false显式关闭初始化功能。

##### 9.7.5 使用一个高级别的数据迁移工具
Spring Boot跟高级别的数据迁移工具Flyway(基于SQL)和Liquibase(XML)工作的很好。通常我们倾向于Flyway，因为它一眼看去好像很容易，另外它通常不需要平台独立：一般一个或至多需要两个平台。

###### 9.7.5.1 启动时执行Flyway数据库迁移
想要在启动时自动运行Flyway数据库迁移，需要将org.flywaydb:flyway-core添加到你的classpath下。

迁移是一些V<VERSION>__<NAME>.sql格式的脚本（<VERSION>是一个下划线分割的版本号，比如'1'或'2_1'）。默认情况下，它们存放在一个classpath:db/migration的文件夹中，但你可以使用flyway.locations（一个列表）来改变它。详情可参考flyway-core中的Flyway类，查看一些可用的配置，比如schemas。Spring Boot在[FlywayProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/flyway/FlywayProperties.java)中提供了一个小的属性集，可用于禁止迁移，或关闭位置检测。

默认情况下，Flyway将自动注入（@Primary）DataSource到你的上下文，并用它进行数据迁移。如果你想使用一个不同的DataSource，你可以创建一个，并将它标记为@FlywayDataSource的@Bean-如果你这样做了，且想要两个数据源，记得创建另一个并将它标记为@Primary。或者你可以通过在外部配置文件中设置flyway.[url,user,password]来使用Flyway的原生DataSource。

这是一个[Flyway](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-flyway)示例，你可以作为参考。

###### 9.7.5.2 启动时执行Liquibase数据库迁移

想要在启动时自动运行Liquibase数据库迁移，你需要将org.liquibase:liquibase-core添加到classpath下。

主改变日志（master change log）默认从db/changelog/db.changelog-master.yaml读取，但你可以使用liquibase.change-log进行设置。详情查看[LiquibaseProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/liquibase/LiquibaseProperties.java)以获取可用设置，比如上下文，默认的schema等。

这里有个[Liquibase示例](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-liquibase)可作为参考。

#### 9.8 批处理应用
##### 9.8.1 在启动时执行Spring Batch作业
你可以在上下文的某个地方添加@EnableBatchProcessing来启用Spring Batch的自动配置功能。

默认情况下，在启动时它会执行应用的所有作业（Jobs），具体查看[JobLauncherCommandLineRunner](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/batch/JobLauncherCommandLineRunner.java)。你可以通过指定spring.batch.job.names（多个作业名以逗号分割）来缩小到一个特定的作业或多个作业。

如果应用上下文包含一个JobRegistry，那么处于spring.batch.job.names中的作业将会从registry中查找，而不是从上下文中自动装配。这是复杂系统中常见的一个模式，在这些系统中多个作业被定义在子上下文和注册中心。

具体参考[BatchAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/batch/BatchAutoConfiguration.java)和[@EnableBatchProcessing](https://github.com/spring-projects/spring-batch/blob/master/spring-batch-core/src/main/java/org/springframework/batch/core/configuration/annotation/EnableBatchProcessing.java)。

#### 9.9 执行器
##### 9.9.1 改变HTTP端口或执行器端点的地址
在一个单独的应用中，执行器的HTTP端口默认和主HTTP端口相同。想要让应用监听不同的端口，你可以设置外部属性management.port。为了监听一个完全不同的网络地址（比如，你有一个用于管理的内部网络和一个用于用户应用程序的外部网络），你可以将management.address设置为一个可用的IP地址，然后将服务器绑定到该地址。

查看[ManagementServerProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/autoconfigure/ManagementServerProperties.java)源码和`'Production-ready特性'章节中的Section 41.3, “Customizing the management server port”`来获取更多详情。

##### 9.9.2 自定义'白标'（whitelabel，可以了解下相关理念）错误页面
Spring Boot安装了一个'whitelabel'错误页面，如果你遇到一个服务器错误（机器客户端消费的是JSON，其他媒体类型则会看到一个具有正确错误码的合乎情理的响应），那就能在客户端浏览器中看到该页面。你可以设置error.whitelabel.enabled=false来关闭该功能，但通常你想要添加自己的错误页面来取代whitelabel。确切地说，如何实现取决于你使用的模板技术。例如，你正在使用Thymeleaf，你将添加一个error.html模板。如果你正在使用FreeMarker，那你将添加一个error.ftl模板。通常，你需要的只是一个名称为error的View，和/或一个处理/error路径的@Controller。除非你替换了一些默认配置，否则你将在你的ApplicationContext中找到一个BeanNameViewResolver，所以一个id为error的@Bean可能是完成该操作的一个简单方式。详情参考[ErrorMvcAutoConfiguration](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ErrorMvcAutoConfiguration.java)。

查看[Error Handling](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#boot-features-error-handling)章节，了解下如何将处理器（handlers）注册到servlet容器中。

#### 9.10 安全
##### 9.10.1 关闭Spring Boot安全配置
不管你在应用的什么地方定义了一个使用@EnableWebSecurity注解的@Configuration，它将会关闭Spring Boot中的默认webapp安全设置。想要调整默认值，你可以尝试设置security.*属性（具体查看[SecurityProperties](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/security/SecurityProperties.java)和[常见应用属性](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#common-application-properties-security)的SECURITY章节）。

##### 9.10.2 改变AuthenticationManager并添加用户账号
如果你提供了一个AuthenticationManager类型的@Bean，那么默认的就不会被创建了，所以你可以获得Spring Security可用的全部特性（比如，不同的认证选项）。

Spring Security也提供了一个方便的AuthenticationManagerBuilder，可用于构建具有常见选项的AuthenticationManager。在一个webapp中，推荐将它注入到WebSecurityConfigurerAdapter的一个void方法中，比如：

	@Configuration
	public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

	    @Autowired
	    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
	            auth.inMemoryAuthentication()
	                .withUser("barry").password("password").roles("USER"); // ... etc.
	    }

	    // ... other stuff for application security
	}
如果把它放到一个内部类或一个单独的类中，你将得到最好的结果（也就是不跟很多其他@Beans混合在一起将允许你改变实例化的顺序）。secure web sample是一个有用的参考模板。

如果你遇到了实例化问题（比如，使用JDBC或JPA进行用户详细信息的存储），那将AuthenticationManagerBuilder回调提取到一个GlobalAuthenticationConfigurerAdapter（放到init()方法内以防其他地方也需要authentication manager）可能是个不错的选择，比如：

	@Configuration
	public class AuthenticationManagerConfiguration extends

	    GlobalAuthenticationConfigurerAdapter {
	    @Override
	    public void init(AuthenticationManagerBuilder auth) {
	        auth.inMemoryAuthentication() // ... etc.
	    }

	}

##### 9.10.3 当前端使用代理服务器时，启用HTTPS
对于任何应用来说，确保所有的主端点（URL）都只在HTTPS下可用是个重要的苦差事。如果你使用Tomcat作为servlet容器，那Spring Boot如果发现一些环境设置的话，它将自动添加Tomcat自己的RemoteIpValve，你也可以依赖于HttpServletRequest来报告是否请求是安全的（即使代理服务器的downstream处理真实的SSL终端）。这个标准行为取决于某些请求头是否出现（x-forwarded-for和x-forwarded-proto），这些请求头的名称都是约定好的，所以对于大多数前端和代理都是有效的。

你可以向application.properties添加以下设置里开启该功能，比如：

	server.tomcat.remote_ip_header=x-forwarded-for
	server.tomcat.protocol_header=x-forwarded-proto
（这些属性出现一个就会开启该功能，或者你可以通过添加一个TomcatEmbeddedServletContainerFactory bean自己添加RemoteIpValve）

Spring Security也可以配置成针对所以或某些请求需要一个安全渠道（channel）。想要在一个Spring Boot应用中开启它，你只需将application.properties中的security.require_ssl设置为true即可。


#### 9.11 热交换
##### 9.11.1 重新加载静态内容
Spring Boot有很多用于热加载的选项。使用IDE开发是一个不错的方式，特别是需要调试的时候（所有的现代IDEs都允许重新加载静态资源，通常也支持对变更的Java类进行热交换）。Maven和Gradle插件也支持命令行下的静态文件热加载。如果你使用其他高级工具编写css/js，并使用外部的css/js编译器，那你就可以充分利用该功能。

##### 9.11.2  在不重启容器的情况下重新加载Thymeleaf模板
如果你正在使用Thymeleaf，那就将spring.thymeleaf.cache设置为false。查看ThymeleafAutoConfiguration可以获取其他Thymeleaf自定义选项。

##### 9.11.3 在不重启容器的情况下重新加载FreeMarker模板
如果你正在使用FreeMarker，那就将spring.freemarker.cache设置为false。查看FreeMarkerAutoConfiguration 可以获取其他FreeMarker自定义选项。

##### 9.11.4 在不重启容器的情况下重新加载Groovy模板
如果你正在使用Groovy模板，那就将spring.groovy.template.cache设置为false。查看GroovyTemplateAutoConfiguration可以获取其他Groovy自定义选项。

##### 9.11.5 在不重启容器的情况下重新加载Velocity模板
如果你正在使用Velocity，那就将spring.velocity.cache设置为false。查看VelocityAutoConfiguration可以获取其他Velocity自定义选项。

##### 9.11.6 在不重启容器的情况下重新加载Java类
现代IDEs（Eclipse, IDEA等）都支持字节码的热交换，所以如果你做了一个没有影响类或方法签名的改变，它会利索地重新加载并没有任何影响。

Spring Loaded在这方面走的更远，它能够重新加载方法签名改变的类定义。如果对它进行一些自定义配置可以强制ApplicationContext刷新自己（但没有通用的机制来确保这对一个运行中的应用总是安全的，所以它可能只是一个开发时间的技巧）。

###### 9.11.6.1 使用Maven配置Spring Loaded
为了在Maven命令行下使用Spring Loaded，你只需将它作为一个依赖添加到Spring Boot插件声明中即可，比如：

	<plugin>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-maven-plugin</artifactId>
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework</groupId>
	            <artifactId>springloaded</artifactId>
	            <version>1.2.0.RELEASE</version>
	        </dependency>
	    </dependencies>
	</plugin>
正常情况下，这在Eclipse和IntelliJ中工作的相当漂亮，只要它们有相应的，和Maven默认一致的构建配置（Eclipse m2e对此支持的更好，开箱即用）。

###### 9.11.6.2 使用Gradle和IntelliJ配置Spring Loaded
如果想将Spring Loaded和Gradle，IntelliJ结合起来，那你需要付出代价。默认情况下，IntelliJ将类编译到一个跟Gradle不同的位置，这会导致Spring Loaded监控失败。

为了正确配置IntelliJ，你可以使用idea Gradle插件：

	buildscript {
	    repositories { jcenter() }
	    dependencies {
	        classpath "org.springframework.boot:spring-boot-gradle-plugin:1.3.0.BUILD-SNAPSHOT"
	        classpath 'org.springframework:springloaded:1.2.0.RELEASE'
	    }
	}

	apply plugin: 'idea'

	idea {
	    module {
	        inheritOutputDirs = false
	        outputDir = file("$buildDir/classes/main/")
	    }
	}

	// ...
注：IntelliJ必须配置跟命令行Gradle任务相同的Java版本，并且springloaded必须作为一个buildscript依赖被包含进去。

此外，你也可以启用Intellij内部的Make Project Automatically，这样不管什么时候只要文件被保存都会自动编译你的代码。

#### 9.12 构建
##### 9.12.1 使用Maven自定义依赖版本
如果你使用Maven进行一个直接或间接继承spring-boot-dependencies（比如spring-boot-starter-parent）的构建，并想覆盖一个特定的第三方依赖，那你可以添加合适的<properties>元素。浏览spring-boot-dependencies POM可以获取一个全面的属性列表。例如，想要选择一个不同的slf4j版本，你可以添加以下内容：

	<properties>
	    <slf4j.version>1.7.5<slf4j.version>
	</properties>
注：这只在你的Maven项目继承（直接或间接）自spring-boot-dependencies才有用。如果你使用<scope>import</scope>，将spring-boot-dependencies添加到自己的dependencyManagement片段，那你必须自己重新定义artifact而不是覆盖属性。

注：每个Spring Boot发布都是基于一些特定的第三方依赖集进行设计和测试的，覆盖版本可能导致兼容性问题。

##### 9.12.2 使用Maven创建可执行JAR
spring-boot-maven-plugin能够用来创建可执行的'胖'JAR。如果你正在使用spring-boot-starter-parent POM，你可以简单地声明该插件，然后你的jar将被重新打包：

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	        </plugin>
	    </plugins>
	</build>
如果没有使用parent POM，你仍旧可以使用该插件。不过，你需要另外添加一个<executions>片段：

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	            <version>1.3.0.BUILD-SNAPSHOT</version>
	            <executions>
	                <execution>
	                    <goals>
	                        <goal>repackage</goal>
	                    </goals>
	                </execution>
	            </executions>
	        </plugin>
	    </plugins>
	</build>
查看[插件文档](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/maven-plugin/usage.html)获取详细的用例。

##### 9.12.3 创建其他的可执行JAR
如果你想将自己的项目以library jar的形式被其他项目依赖，并且需要它是一个可执行版本（例如demo），你需要使用略微不同的方式来配置该构建。

对于Maven来说，正常的JAR插件和Spring Boot插件都有一个'classifier'，你可以添加它来创建另外的JAR。示例如下（使用Spring Boot Starter Parent管理插件版本，其他配置采用默认设置）：

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	            <configuration>
	                <classifier>exec</classifier>
	            </configuration>
	        </plugin>
	    </plugins>
	</build>
上述配置会产生两个jars，默认的一个和使用带有classifier 'exec'的Boot插件构建的可执行的一个。

对于Gradle用户来说，步骤类似。示例如下：

	bootRepackage  {
	    classifier = 'exec'
	}

##### 9.12.4 在可执行jar运行时提取特定的版本
在一个可执行jar中，为了运行，多数内嵌的库不需要拆包（unpacked），然而有一些库可能会遇到问题。例如，JRuby包含它自己的内嵌jar，它假定jruby-complete.jar本身总是能够直接作为文件访问的。

为了处理任何有问题的库，你可以标记那些特定的内嵌jars，让它们在可执行jar第一次运行时自动解压到一个临时文件夹中。例如，为了将JRuby标记为使用Maven插件拆包，你需要添加如下的配置：

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	            <configuration>
	                <requiresUnpack>
	                    <dependency>
	                        <groupId>org.jruby</groupId>
	                        <artifactId>jruby-complete</artifactId>
	                    </dependency>
	                </requiresUnpack>
	            </configuration>
	        </plugin>
	    </plugins>
	</build>
使用Gradle完全上述操作：

	springBoot  {
	    requiresUnpack = ['org.jruby:jruby-complete']
	}

##### 9.12.6  远程调试一个使用Maven启动的Spring Boot项目
想要为使用Maven启动的Spring Boot应用添加一个远程调试器，你可以使用mave插件的jvmArguments属性。详情参考[示例](http://docs.spring.io/spring-boot/docs/1.3.0.BUILD-SNAPSHOT/maven-plugin/examples/run-debug.html)。

##### 9.12.7  远程调试一个使用Gradle启动的Spring Boot项目
想要为使用Gradle启动的Spring Boot应用添加一个远程调试器，你可以使用build.gradle的applicationDefaultJvmArgs属性或--debug-jvm命令行选项。

	build.gradle：

	applicationDefaultJvmArgs = [
	    "-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5005"
	]
命令行：

	$ gradle run --debug-jvm
详情查看[Gradle应用插件](http://www.gradle.org/docs/current/userguide/application_plugin.html)。

##### 9.12.8 使用Ant构建可执行存档（archive）

想要使用Ant进行构建，你需要抓取依赖，编译，然后像通常那样创建一个jar或war存档。为了让它可以执行：

1. 使用合适的启动器配置Main-Class，比如对于jar文件使用JarLauncher，然后将其他需要的属性以manifest实体指定，主要是一个Start-Class。
2. 将运行时依赖添加到一个内嵌的'lib'目录（对于jar），provided（内嵌容器）依赖添加到一个内嵌的lib-provided目录。记住不要压缩存档中的实体。
3. 在存档的根目录添加spring-boot-loader类（这样Main-Class就可用了）。

示例：
	<target name="build" depends="compile">
	    <copy todir="target/classes/lib">
	        <fileset dir="lib/runtime" />
	    </copy>
	    <jar destfile="target/spring-boot-sample-actuator-${spring-boot.version}.jar" compress="false">
	        <fileset dir="target/classes" />
	        <fileset dir="src/main/resources" />
	        <zipfileset src="lib/loader/spring-boot-loader-jar-${spring-boot.version}.jar" />
	        <manifest>
	            <attribute name="Main-Class" value="org.springframework.boot.loader.JarLauncher" />
	            <attribute name="Start-Class" value="${start-class}" />
	        </manifest>
	    </jar>
	</target>
该Actuator示例中有一个build.xml文件，可以使用以下命令来运行：

	$ ant -lib /ivy-2.2.jar
在上述操作之后，你可以使用以下命令运行该应用：

	$ java -jar target/*.jar

##### 9.12.9 如何使用Java6
如果想在Java6环境中使用Spring Boot，你需要改变一些配置。具体的变化取决于你应用的功能。

###### 9.12.9.1 内嵌Servlet容器兼容性
如果你在使用Boot的内嵌Servlet容器，你需要使用一个兼容Java6的容器。Tomcat 7和Jetty 8都是Java 6兼容的。具体参考[Section 63.15, “Use Tomcat 7”](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto-use-tomcat-7)和[Section 63.16, “Use Jetty 8”](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto-use-jetty-8)。

###### 9.12.9.2 JTA API兼容性
Java事务API自身并不要求Java 7，而是官方的API jar包含的已构建类要求Java 7。如果你正在使用JTA，那么你需要使用能够在Java 6工作的构建版本替换官方的JTA 1.2 API jar。为了完成该操作，你需要排除任何对javax.transaction:javax.transaction-api的传递依赖，并使用org.jboss.spec.javax.transaction:jboss-transaction-api_1.2_spec:1.0.0.Final依赖替换它们。

#### 9.13 传统部署
##### 9.13.1 创建一个可部署的war文件
产生一个可部署war包的第一步是提供一个SpringBootServletInitializer子类，并覆盖它的configure方法。这充分利用了Spring框架对Servlet 3.0的支持，并允许你在应用通过servlet容器启动时配置它。通常，你只需把应用的主类改为继承SpringBootServletInitializer即可：

	@SpringBootApplication
	public class Application extends SpringBootServletInitializer {

	    @Override
	    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
	        return application.sources(Application.class);
	    }

	    public static void main(String[] args) throws Exception {
	        SpringApplication.run(Application.class, args);
	    }

	}
下一步是更新你的构建配置，这样你的项目将产生一个war包而不是jar包。如果你使用Maven，并使用spring-boot-starter-parent（为了配置Maven的war插件），所有你需要做的就是更改pom.xml的packaging为war：

	<packaging>war</packaging>
如果你使用Gradle，你需要修改build.gradle来将war插件应用到项目上：

	apply plugin: 'war'
该过程最后的一步是确保内嵌的servlet容器不能干扰war包将部署的servlet容器。为了达到这个目的，你需要将内嵌容器的依赖标记为provided。

如果使用Maven：

	<dependencies>
	    <!-- … -->
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-tomcat</artifactId>
	        <scope>provided</scope>
	    </dependency>
	    <!-- … -->
	</dependencies>
	如果使用Gradle：

	dependencies {
	    // …
	    providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'
	    // …
	}
如果你使用[Spring Boot构建工具](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#build-tool-plugins)，将内嵌容器依赖标记为provided将产生一个可执行war包，在lib-provided目录有该war包的provided依赖。这意味着，除了部署到servlet容器，你还可以通过使用命令行java -jar命令来运行应用。

注：查看Spring Boot基于以上配置的一个[Maven示例应用](http://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-traditional/pom.xml)。

##### 9.13.2 为老的servlet容器创建一个可部署的war文件
老的Servlet容器不支持在Servlet 3.0中使用的ServletContextInitializer启动处理。你仍旧可以在这些容器使用Spring和Spring Boot，但你需要为应用添加一个web.xml，并将它配置为通过一个DispatcherServlet加载一个ApplicationContext。

##### 9.13.3 将现有的应用转换为Spring Boot

对于一个非web项目，转换为Spring Boot应用很容易（抛弃创建ApplicationContext的代码，取而代之的是调用SpringApplication或SpringApplicationBuilder）。Spring MVC web应用通常先创建一个可部署的war应用，然后将它迁移为一个可执行的war或jar。建议阅读Getting Started Guide on Converting a jar to a war.。

通过继承SpringBootServletInitializer创建一个可执行war（比如，在一个名为Application的类中），然后添加Spring Boot的@EnableAutoConfiguration注解。示例：

	@Configuration
	@EnableAutoConfiguration
	@ComponentScan
	public class Application extends SpringBootServletInitializer {

	    @Override
	    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
	        // Customize the application or call application.sources(...) to add sources
	        // Since our example is itself a @Configuration class we actually don't
	        // need to override this method.
	        return application;
	    }

	}
记住不管你往sources放什么东西，它仅是一个Spring ApplicationContext，正常情况下，任何生效的在这里也会起作用。有一些beans你可以先移除，然后让Spring Boot提供它的默认实现，不过有可能需要先完成一些事情。

静态资源可以移到classpath根目录下的/public（或/static，/resources，/META-INF/resources）。同样的方式也适合于messages.properties（Spring Boot在classpath根目录下自动发现这些配置）。

美妙的（Vanilla usage of）Spring DispatcherServlet和Spring Security不需要改变。如果你的应用有其他特性，比如使用其他servlets或filters，那你可能需要添加一些配置到你的Application上下文中，按以下操作替换web.xml的那些元素：

1. 在容器中安装一个Servlet或ServletRegistrationBean类型的@Bean，就好像web.xml中的<servlet/>和<servlet-mapping/>。
2. 同样的添加一个Filter或FilterRegistrationBean类型的@Bean（类似于<filter/>和<filter-mapping/>）。
3. 在XML文件中的ApplicationContext可以通过@Import添加到你的Application中。简单的情况下，大量使用注解配置可以在几行内定义@Bean定义。

一旦war可以使用，我们就通过添加一个main方法到Application来让它可以执行，比如：

	public static void main(String[] args) {
	    SpringApplication.run(Application.class, args);
	}
应用可以划分为多个类别：

* 没有web.xml的Servlet 3.0+应用
* 有web.xml的应用
* 有上下文层次的应用
* 没有上下文层次的应用

所有这些都可以进行适当的转化，但每个可能需要稍微不同的技巧。

Servlet 3.0+的应用转化的相当简单，如果它们已经使用Spring Servlet 3.0+初始化器辅助类。通常所有来自一个存在的WebApplicationInitializer的代码可以移到一个SpringBootServletInitializer中。如果一个存在的应用有多个ApplicationContext（比如，如果它使用AbstractDispatcherServletInitializer），那你可以将所有上下文源放进一个单一的SpringApplication。你遇到的主要难题可能是如果那样不能工作，那你就要维护上下文层次。参考示例entry on building a hierarchy。一个存在的包含web相关特性的父上下文通常需要分解，这样所有的ServletContextAware组件都处于子上下文中。

对于还不是Spring应用的应用来说，上面的指南有助于你把应用转换为一个Spring Boot应用，但你也可以选择其他方式。

##### 9.13.4 部署WAR到Weblogic
想要将Spring Boot应用部署到Weblogic，你需要确保你的servlet初始化器直接实现WebApplicationInitializer（即使你继承的基类已经实现了它）。

一个传统的Weblogic初始化器可能如下所示：

	import org.springframework.boot.autoconfigure.SpringBootApplication;
	import org.springframework.boot.context.web.SpringBootServletInitializer;
	import org.springframework.web.WebApplicationInitializer;

	@SpringBootApplication
	public class MyApplication extends SpringBootServletInitializer implements WebApplicationInitializer {

	}
如果使用logback，你需要告诉Weblogic你倾向使用的打包版本而不是服务器预装的版本。你可以通过添加一个具有如下内容的WEB-INF/weblogic.xml实现该操作：

	<?xml version="1.0" encoding="UTF-8"?>
	<wls:weblogic-web-app
	    xmlns:wls="http://xmlns.oracle.com/weblogic/weblogic-web-app"
	    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
	        http://java.sun.com/xml/ns/javaee/ejb-jar_3_0.xsd
	        http://xmlns.oracle.com/weblogic/weblogic-web-app
	        http://xmlns.oracle.com/weblogic/weblogic-web-app/1.4/weblogic-web-app.xsd">
	    <wls:container-descriptor>
	        <wls:prefer-application-packages>
	            <wls:package-name>org.slf4j</wls:package-name>
	        </wls:prefer-application-packages>
	    </wls:container-descriptor>
	</wls:weblogic-web-app>



转载自:[https://www.gitbook.com/book/qbgbook/spring-boot-reference-guide-zh/details](https://www.gitbook.com/book/qbgbook/spring-boot-reference-guide-zh/details)

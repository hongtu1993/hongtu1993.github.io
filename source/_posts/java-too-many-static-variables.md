---
title: java too many static variables
author: 毛宇鹏
date: 2018-12-13 14:07:04
subtitle:
showTitle: java 静态变量太多的优化方法
description: 如果系统定义了大量的静态常量, 但又不希望其占用太多堆内存,要怎么处理? 我们将会巧妙使用java的内部类来解决这个问题
tags:
categories:
    - java
---

```bash
// 需要用时就Constant.A.A1   Constant.B.B2
public class Constant {
    public class A{
        public static final String A1= "A1";
        public static final String A2= "A2";
    }

    public class B{
        public static final String B1= "B1";
        public static final String B2= "B2";
    }
}
```

---
layout:     post
title:      "关于mongoDB对时区的处理"
subtitle:   "mongoDB对时间的处理ISODate与我们时区相差8小时"
date:       2016-05-02
author:     "caojiele"
tags:
    - mongoDB
    - ISODate
    - Java
---

在mongoDB数据库中，时间的保存是ISODate类型，orm关系映射为java.util.Date类型，其保存的时间与我们会有8小时的区别（保存的时间比我们早了8个小时）。

原数据为：
`Person [id=11188, name=doctorwho, age=888888,birth=2016-01-01 13:55:00]`
 
 mongoDB数据库中为：
```mongoDB
{ 
    "_id" : "11188", 
    "_class" : "com.doctor.domain.Person", 
    "name" : "doctorwho", 
    "age" : NumberInt(888888), 
    "birth" : ISODate("2016-01-01T05:55:00.000+0000")
}
```
  
 那我们用时间查询数据的时候，看下java 驱动如何做的（部分日志）：
 
```java
package com.alibaba.dubbo.demo;
public interface DemoService {
    String sayHello(String name);
}
```

time query:

* 01-02 22:12:37.195 main  DEBUG org.springframework.data.mongodb.core.MongoTemplate - find using query: { "birth" : { "$date" : "2016-01-01T05:55:00.000Z"}} fields: null for class: class com.doctor.domain.Person in collection: person

* 01-02 22:12:37.196 main  DEBUG org.springframework.data.mongodb.core.MongoDbUtils - Getting Mongo Database name=[sdcuike]
Person [id=11188, name=doctorwho, age=888888,birth=2016-01-01 13:55:00]

{ "birth" : { "$date" : "2016-01-01T05:55:00.000Z"}}查询语句按我们的相差时间查询，返回的数据确实是我们需要的，即使数据库中我们看到的iso date相差8个小时。其实java 驱动帮我们做了转换。


com.mongodb.util.JSONSerializers.LegacyDateSerializer代码：

```java

 ```

所以在这里`GregorianCalendar` ，做了时区转换。

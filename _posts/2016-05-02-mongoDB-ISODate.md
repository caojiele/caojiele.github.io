---
layout:     post
title:      "关于mongoDB对时区的处理"
subtitle:   "mongoDB对时间的处理ISODate与我们时区相差8小时"
date:       2016-05-02
author:     "caojiele"
header-img: "img/in-post/2016.05/02/post-bg-miui6.jpg"
tags:
    - 数据库
    - mongoDB
    - Java
---

在mongoDB数据库中，时间的保存是ISODate类型，orm关系映射为java.util.Date类型，其保存的时间与我们会有8小时的区别（保存的时间比我们早了8个小时）。

原数据为：
```Bash
Person [id=11188, name=doctorwho, age=888888, birth=2016-01-01 13:55:00]
```

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
package com.doctor.springdoc;
 
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Date;
import java.util.List;
 
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;
import org.springframework.data.mongodb.core.query.Update;
 
import com.doctor.domain.Person;
import com.mongodb.WriteResult;
 
/**
 * JSONSerializers L205-216有关mongoDB对时间的处理ISODate与我们时区相差8小时（做个时区转换）
 * 
 * @author sdcuike
 *
 * @time 2015年12月27日 下午10:54:16
 */
public class SavingUpdatingRemovingDocuments {
 
    /**
     * @param args
     */
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("classpath:/mongoDBConfig/spring-mongoDB.xml");
        MongoTemplate mongoTemplate = context.getBean(MongoTemplate.class);
 
        Person person = new Person("doctorwho", 28888, "11188");
 
        LocalDateTime localDateTime = LocalDateTime.of(2016, 1, 1, 13, 55);
        ZonedDateTime zonedDateTime = localDateTime.atZone(ZoneId.of("Asia/Shanghai"));
        person.setBirth(Date.from(zonedDateTime.toInstant()));
 
        System.out.println(person);
        if (mongoTemplate.findById(person.getId(), Person.class) == null) {
            mongoTemplate.insert(person);
        }
 
        Person findById = mongoTemplate.findById(person.getId(), Person.class);
        System.out.println(findById);
 
        List<Person> find = mongoTemplate.find(Query.query(Criteria.where("name").is("doctorwho").and("age").is(28888)), Person.class);
        find.forEach(System.out::println);
 
        WriteResult updateMulti = mongoTemplate.updateMulti(Query.query(Criteria.where("age").is(28888)), Update.update("age", 888888), Person.class);
        System.out.println(updateMulti.getN());
 
        System.out.println("time query");
        List<Person> find2 = mongoTemplate.find(Query.query(Criteria.where("birth").is(person.getBirth())), Person.class);
        find2.forEach(System.out::println);
        // JSONSerializers L205-216有关mongoDB对时间的处理ISODate与我们时区相差8小时（做个时区转换）
    }
 
}
```

time query:

* 01-02 22:12:37.195 main  DEBUG org.springframework.data.mongodb.core.MongoTemplate - find using query: { "birth" : { "$date" : "2016-01-01T05:55:00.000Z"}} fields: null for class: class com.doctor.domain.Person in collection: person

* 01-02 22:12:37.196 main  DEBUG org.springframework.data.mongodb.core.MongoDbUtils - Getting Mongo Database name=[sdcuike]
Person [id=11188, name=doctorwho, age=888888,birth=2016-01-01 13:55:00]


{ "birth" : { "$date" : "2016-01-01T05:55:00.000Z"}}查询语句按我们的相差时间查询，返回的数据确实是我们需要的，即使数据库中我们看到的iso date相差8个小时。其实java 驱动帮我们做了转换。


com.mongodb.util.JSONSerializers.LegacyDateSerializer代码：

```java
 private static class LegacyDateSerializer extends CompoundObjectSerializer {
 
        LegacyDateSerializer(ObjectSerializer serializer) {
            super(serializer);
        }
 
        @Override
        public void serialize(Object obj, StringBuilder buf) {
            Date d = (Date) obj;
            SimpleDateFormat format = new SimpleDateFormat(
                    "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'");
            format.setCalendar(new GregorianCalendar(
                    new SimpleTimeZone(0, "GMT")));
            serializer.serialize(
                    new BasicDBObject("$date", format.format(d)),
                    buf);
        }
    }
 ```

所以在这里`GregorianCalendar` ，做了时区转换。

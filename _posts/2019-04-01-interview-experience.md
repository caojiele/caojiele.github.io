---
layout:     post
title:      "面试经验"
subtitle:   "大厂"
date:       2019-04-01
author:     "caojiele"
header-img: "img/in-post/2019.04/01/post-interview-experience.png"
tags:
    - 面试
    - Java
---

这是我今年三月份大厂的主要面试经过，有些还没整理出来，这篇文章会持续更新，请各位持续关注，希望对你有所帮助！

## 平安产险面试（电话面试） 深圳
先通过邮件发了一份线上测评（EQ+IQ), 做完达到要求后才能有后续的面试机会，没有通过`两年之内`不能进平安任何一家公司。

**一面：**
* 自我介绍 2分钟
* 看我工作时间不长，问我为什么频繁跳槽（间接问离职原因）
* 关注过平安哪些架构?(我就说了[军哥](https://github.com/HaojunRen)的pass平台）
* 解释下什么是用户态和内核态以及区别？
* 用过spring boot哪些版本？新版本相对于旧版本有哪些改变？
* web.xml中DispatcherServlet的作用？
* 讲下web.xml中Filter类（过滤器）
* 使用spring boot以后，与之前系统的配置方式区别方面?(spring boot 和 spring MVC 使用和配置上的区别？
* 好像还有个reactivity什么的,当时记不清了。

**二面：**
整理中

## 飞猪面试（电话面试） 杭州
这个是内推，当然内推的人和我一面的面试官都是同一个人，所以 嘿嘿嘿 你懂得...

**一面：**
* 自我介绍
* 介绍一下你这边最熟悉的项目？在开发过程中印象最深刻地方？
* springboot 2.0.0和springboot 1.5.6的区别？
* 有没有看过springboot的源码？（很尴尬，没有研究过）
* springboot中遇到的一些坑及解决方法？
* 有没有看过spring的源码？（很尴尬，了解过）
* 你现在对Dubbo了解得怎么样？
* JDK1.9的新特性？（我说：没有用过1.9，感觉1.9不是很稳定,只用过1.8）那说一下 1.8有哪些新特性？
* JDK有哪些实现代理方法？JDK动态代理和CGlib动态代理有什么区别？
* 介绍下OOM?开发过程中遇到过哪些OOM,怎样解决的？
* 介绍下Java内存模型？
* 你这边有什么问题？

**二面：**
整理中

## 上汽大通（现场面试） 上海
一套J2EE+Oracle的笔试 大概有五六张纸 我依稀记得几道题

* main方法中是否可以调用非静态方法
可以，一种方法将main方法写成静态方法，另一种将当前类实例化再调用它的非静态方法 例如：
```java
public class Test {
private int a;
public int getnumber() {
setnumber(8);
return this.a;
}
public int setnumber (int a) {
return this.a=a;
}
public static void main(String args[]){

}
}
```
改为：
```java
public class Test {
    private int a;
 
    public int getnumber() {
        setnumber(8);
        return this.a;
    }
 
    public int setnumber(int a) {
        return this.a = a;
    }
 
    public static void main(String args[]) {
        Test t = new Test();
//      t.setnumber(10);
        int a = t.getnumber();
        System.out.println(a);
    }
}
```
* 解释下AOP和IOC的工作机制？
AOP思想的实现一般都是基于代理模式 ，在JAVA中一般采用JDK动态代理模式，但是我们都知道，JDK动态代理模式只能代理接口而不能代理类。因此，Spring AOP 会这样子来进行切换，因为Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理。

Spring IOC的初始化过程： 


* servlet的生命周期

  javax.servlet.Servlet接口中的init()、service()和destroy()方法来表示，主要包括四个阶段：
  * 加载和实例化
  * 初始化
  * 请求处理
  * 服务终止

* String、StringBuffer和StringBuilder三者区别？
* synchronized的可重入怎么实现？
* RuntimeException和Exception的区别？
* wait()和sleep()的区别？
* 有三个线程t1、t2、t3。确保三个线程t1执行完后t2执行，t2执行完成后t3执行？

* &和&&的区别？
**电路问题总结：**
对于：&   -- >  不管怎样，都会执行"&"符号左右两边的程序

对于：&& -- >  只有当符号"&&"左边程序为真(true)后，才会执行符号"&&"右边的程序。

**运算规则：**

对于：&  -- >  只要左右两边有一个为false，则为false；只有全部都为true的时候，结果为true

对于：&& -- > 只要符号左边为false，则结果为false；当左边为true，同时右边也为true，则结果为true

* sql语句select、group by、order by、where 先后顺序？

写的顺序：select ... from... where.... group by... having... order by..

执行顺序：from... where...group by... having.... select ... order by...

* 解释Java内存模型？

* JDBC如何连接数据库？

两位技术负责人+部长（周）简单聊了一下，自己的项目和经验，遇到过哪些问题？怎么解决的？怎么设计数据库模型？

## 浩鲸科技（电话面试） 杭州

**一面（技术面）:**
* 自我介绍
* 谈一下自己最熟悉的项目中的业务框架？
（登录+权限VIP服务绑定）
* 是怎样提交给前端接口的？
* token使用的时候过期失效怎么解决？
* 登录这块如何实现高可用？什么是高可用？
* 你实际java开发多长时间？

当问我这个问题的时候，我就知道前面答得并不是很好，所以面试官后面问的都是基础题。
* 抽象类和接口有什么区别？
* 用过哪些集合？list和set的区别？
* 用过哪些设计模式？
* 你这边还有什么问题？

因为这个项目是和杭州阿里系的大佬们一起开发盒马鲜生这款产品，所以着重问了下开发产品情况和团队架构。
* 你现在的薪资和期望薪资？

照实际的说，大厂一般都会查银行流水。

**二面（终面）**
整理中

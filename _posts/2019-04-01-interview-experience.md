---
layout:     post
title:      "面试经验总结"
subtitle:   "Java开发 大厂面试"
date:       2019-04-01
author:     "caojiele"
header-img: "img/in-post/2019.04/01/post-interview-experience.png"
tags:
    - 面试
    - Java
---

这是我今年从三月份开始，主要的大厂面试经过，有些企业面试的还没来得及整理，可能有些没有带答案就发出来了，还请各位先思考如果是你怎么回答面试官？这篇文章会持续更新，请各位持续关注，希望对你有所帮助！

## 面试清单
- [平安产险](#平安产险)
- [飞猪](#飞猪)
- [上汽大通](#上汽大通)
- [浩鲸科技](#浩鲸科技)
- [杏仁医生](#杏仁医生)
- [兴盛优先](#兴盛优先)
- [御泥坊](#御泥坊)
- [拓维信息](#拓维信息)
- [陆金所](#陆金所)
- [蜜獾信息](#蜜獾信息)
- [丰巢科技](#丰巢科技)


## 平安产险
先通过邮件发了一份线上测评（EQ+IQ), 做完达到要求后才能有后续的面试机会，没有通过`两年之内`不能进平安任何一家公司。

### **一面**

#### **自我介绍**

#### **看我工作时间不长，问我为什么频繁跳槽（间接问离职原因）**

#### **关注过平安哪些架构？**
  我就说了[军哥](https://github.com/HaojunRen)的pass平台

#### **解释下什么是用户态和内核态？两者有什么区别？**

  **内核态**：当一个任务（进程）执行系统调用而陷入内核代码中执行时，我们就称进程处于内核运行态（或简称为内核态）。其他的都属于**用户态**。
  
  用户程序运行在用户态,操作系统运行在内核态（操作系统内核运行在内核态，而服务器运行在用户态）。用户态不能干扰内核态.所以CPU指令就有两种,特权指令和非特权指令.不同的状态对应不同的指令。特权指令：只能由操作系统内核部分使用，不允许用户直接使用的指令。
  如：I/O指令、置终端屏蔽指令、清内存、建存储保护、设置时钟指令（这几种记好，属于内核态）。非特权指令：所有程序均可直接使用。 
  
  **所以：**
  
  系统态（核心态、特态、管态）：执行全部指令。 
  
  用户态（常态、目态）：执行非特权指令。
  
  [用户态和内核态的理解和区别](https://blog.csdn.net/qq_39823627/article/details/78736650)

#### **用过Spring boot哪些版本？新版本相对于旧版本有哪些改变？**
  [https://github.com/spring-projects/spring-boot/wiki](https://github.com/spring-projects/spring-boot/wiki)
  
  [Spring Boot 2.x 与 1.x 的区别，以及如何做版本迁移](https://zhuanlan.zhihu.com/p/63596771)

#### **web.xml中DispatcherServlet的作用？**

  [Spring MVC中的DispatcherServlet作用](https://www.cnblogs.com/shilin000/p/4759015.html)

  [DispatcherServlet过程详解](https://blog.csdn.net/lhn1234321/article/details/83868724)

#### **讲下web.xml中Filter类（过滤器）**

  [web.xml中的配置，servlet，filter，listener的作用和原理](https://blog.csdn.net/h2604396739/article/details/84899251)

#### **使用Spring boot以后，与之前系统的配置方式区别方面？(Spring boot 和 Spring MVC 使用和配置上的区别？）**

  [SpringBoot - 注册Servlet、Filter和Listener(代码和注解两种方式)](https://blog.csdn.net/J080624/article/details/80758614)

  [spring boot与spring mvc的区别是什么？](https://www.zhihu.com/question/64671972/answer/223383505)
   
#### **好像还有个reactivity什么的,当时记不清了。** 
你们如果面试碰到了相关经典题目。欢迎补充！

### **二面**
整理中


## 飞猪
首先这个面试机会是来自于内推，当然内推的人和我一面的面试官都是同一个人，所以 嘿嘿嘿 你懂得...

### **一面**

#### **自我介绍**

#### **介绍一下你这边最熟悉的项目？在开发过程中印象最深刻地方？**

#### **Springboot 2.0.0和Springboot 1.5.6的区别？**
 
  [https://github.com/spring-projects/spring-boot/wiki](https://github.com/spring-projects/spring-boot/wiki)
  
  [Spring Boot 2.x 与 1.x 的区别，以及如何做版本迁移](https://zhuanlan.zhihu.com/p/63596771)

#### **有没有看过Springboot的源码？（很尴尬，没有研究过）**

  [https://github.com/spring-projects/spring-boot](https://github.com/spring-projects/spring-boot)

#### **Springboot中遇到的一些坑及解决方法？**
 
  [Springboot与shiro整合遇到的坑](https://zhuanlan.zhihu.com/p/29161098)
  
  [Spring Boot 从1.0 升级到 2.0 所踩的坑](https://zhuanlan.zhihu.com/p/42678472)

#### **有没有看过Spring的源码？（很尴尬，了解过）**

  [https://github.com/spring/spring](https://github.com/spring/spring)

#### **你现在对Dubbo了解得怎么样？（作为这个项目的贡献者，没有深入阅读源码和实践真的是汗颜）**

   [https://github.com/apache/incubator-dubbo](https://github.com/apache/incubator-dubbo)
   
   [30 道 Dubbo 面试题及答案](https://segmentfault.com/a/1190000018438985)

#### **JDK 1.9 的新特性？（我说：没有用过1.9，感觉1.9不是很稳定,只用过1.8）那说一下 1.8 有哪些新特性？**

  [jdk8, jdk8u, jdk9, jdk10的侧重和区别是什么？](https://www.zhihu.com/question/60786248/answer/180169329)

  [JDK 9新特性汇总](https://zhuanlan.zhihu.com/p/29589033)
  
  [JDK1.8新特性（持续更新）](https://zhuanlan.zhihu.com/p/62601317)
  
#### **JDK有哪些实现代理方法？JDK动态代理和CGlib动态代理有什么区别？**

  [深入理解静态代理与JDK动态代理](https://zhuanlan.zhihu.com/p/60922671)
  
  [JDK动态代理与CGLib动态代理相关问题](https://zhuanlan.zhihu.com/p/48736954)
  
#### **介绍下OOM?开发过程中遇到过哪些OOM,怎样解决的？**

  OutOfMemoryError，当JVM因为没有足够的内存来为对象分配空间并且垃圾回收器也已经没有空间可回收时，就会抛出这个error（注：非exception，因为这个问题已经严重到不足以被应用处理）。
  
  因为OutOfMemoryError是可以catch的。catch之后吞掉的话程序还能试着继续运行。例如说以前见过的一个案例是：一个Java服务器端应用，有段代码没写对导致有一个线程在疯狂创建大数组对象——直到OOM。这个线程注册的uncaught exception handler捕获到了这个异常，记录了日志，然后就把这个异常吞掉了。这样还能继续正常跑下去是因为：只是一个创建很大的数组对象的请求失败了而已，而出错的那个方法由于异常处理已经被退出了，程序的其它部分并没有受影响。
  
  [JVM 发生 OOM 的 8 种原因、及解决办法](https://zhuanlan.zhihu.com/p/63752449)

#### **介绍下Java内存模型？**

[Java内存模型（JMM）总结](https://zhuanlan.zhihu.com/p/29881777)

#### **你这边还有什么问题？**

### **二面**
整理中


## 上汽大通
一套J2EE+Oracle的笔试 大概有五六张纸 我只依稀记得几道题

### 现场面试

#### **main方法中是否可以调用非静态方法**

可以，一种方法将main方法写成静态方法，另一种将当前类实例化再调用它的非静态方法，例如：

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
#### **解释下AOP和IOC的工作机制？**

AOP思想的实现一般都是基于代理模式 ，在JAVA中一般采用JDK动态代理模式，但是我们都知道，JDK动态代理模式只能代理接口而不能代理类。因此，Spring AOP 会这样子来进行切换，因为Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理。

Spring IOC的初始化过程： 

XML ------> Resource ------> BeanDefinition ------> BeanFactory

[如何理解Spring中的IOC和AOP](https://zhuanlan.zhihu.com/p/58006579)

#### **servlet的生命周期**

  javax.servlet.Servlet接口中的init()、service()和destroy()方法来表示，主要包括四个阶段：
  * 加载和实例化
  * 初始化
  * 请求处理
  * 服务终止

#### **String、StringBuffer和StringBuilder三者区别？**

  [JAVA中String与StringBuffer，StringBuilder的区别](http://blog.chinaunix.net/uid-20767210-id-1849811.html)
  
  [StringBuffer 和 StringBuilder 的区别是什么？](https://zhuanlan.zhihu.com/p/22298080)
  
#### **怎么实现synchronized的可重入？**

  synchronized是可重入的，对同一个执行线程，它在获得了锁之后，在调用其他需要同样锁的代码时，可以直接调用。

  可重入是通过记录锁的持有线程和持有数量来实现的，当调用synchronized保护的代码时，检查对象是否已被锁，如果是，再检查是否被当前线程锁定，如果是，增加持有数量，如果不是被当前线程锁定，才加入等待队列，当释放锁时，减少持有数量，当数量为0时才释放整个锁。

  [synchronized 关键字](https://snailclimb.top/JavaGuide/#/./java/Multithread/JavaConcurrencyAdvancedCommonInterviewQuestions?id=_1-synchronized-关键字)

#### **RuntimeException和Exception的区别？**

  [java基础学习(12)RuntimeException和Exception](https://zhuanlan.zhihu.com/p/47258269)
  
#### **wait()和sleep()的区别？**

  [sleep( ) 和 wait( ) 的这 5 个区别，你知道几个？](https://zhuanlan.zhihu.com/p/45666264)
  
#### **有三个线程t1、t2、t3。确保三个线程t1执行完后t2执行，t2执行完成后t3执行？**
  用 Thread 类的 join 方法。
  ```java
private static void threadJoinOneByOne() throws InterruptedException {
        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        // start() 仅是通知线程启动
        t1.start();
        // join() 控制线程必须执行完成
        t1.join();

        t2.start();
        t2.join();

        t3.start();
        t3.join();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}
```
**CountDownLatch**也可以实现

**调整优先级**并不能保证控制线程执行顺序

#### **&和&&的区别？**

**电路问题总结：**

&：不管怎样，都会执行"&"符号左右两边的程序

&&：只有当符号"&&"左边程序为真(true)后，才会执行符号"&&"右边的程序。

**运算规则：**

&：只要左右两边有一个为false，则为false；只有全部都为true的时候，结果为true

&&：只要符号左边为false，则结果为false；当左边为true，同时右边也为true，则结果为true

#### **sql语句`select`、`group by`、`order by`、`where`先后顺序？**

写的顺序：select ... from... where.... group by... having... order by..

执行顺序：from... where...group by... having.... select ... order by...

#### **解释Java内存模型？**

[Java内存模型（JMM）总结](https://zhuanlan.zhihu.com/p/29881777)
  
#### **JDBC如何连接数据库？**
  [JDBC【介绍JDBC、使用JDBC连接数据库、简单的工具类】](https://zhuanlan.zhihu.com/p/33828916)

两位技术负责人+部长（周）简单聊了一下，自己的项目和经验，遇到过哪些问题？怎么解决的？怎么设计数据库模型？

## 浩鲸科技（电话面试） 杭州

### **一面**

#### **自我介绍**

#### **谈一下自己最熟悉的项目中的业务框架？**
（登录+权限VIP服务绑定）

#### **开发过程中后端如何提交给前端接口？**

#### **如何解决前后端token过期问题？**

  每隔一段时间在后端请求中都将token传送过去，获取新的token值，并返回前端放入cookies中并记录cookie的存储失控,达到更新cookie中token的效果;而长时间不做操作的话我们就可以让他的token失效退出系统了。
  
  [如何解决前后端token过期问题](https://blog.csdn.net/qq_31679735/article/details/79590850)
  
#### **如何实现在登录中高可用？什么是高可用？**
  用户信息存redis；加节点，加机器，多部署实例。

  [什么是高可用](https://zhuanlan.zhihu.com/p/43723276)

#### **你实际java开发多长时间？**

  当问我这个问题的时候，我就知道前面答得并不是很好，所以面试官后面问的都是基础题。
  
#### **抽象类和接口有什么区别？**

  [接口和抽象类有什么区别？](https://www.zhihu.com/question/20149818/answer/142270191)

#### **用过哪些集合？list和set的区别？**
  
  [深入理解Java中的List、Set与Map集合](https://zhuanlan.zhihu.com/p/34518772)

#### **用过哪些设计模式？**

  [如何在代码中应用设计模式](https://zhuanlan.zhihu.com/p/63601369)
  
#### **你这边还有什么问题？**

  因为这个项目是和杭州阿里系的大佬们一起开发盒马鲜生这款产品，所以着重问了下开发产品情况和团队架构。
  
#### **你现在的薪资和期望薪资？**

  照实际的说，大厂一般都会查银行流水。

### **二面**
整理中


## 杏仁医生

### **一面**

#### **自我介绍**

#### **mysql 常用存储引擎有哪些？分别有什么特点和区别？**

  [MySQL常用存储引擎](https://www.cnblogs.com/lvjianwei/p/9880993.html)

#### **谈一谈MySQL的四种事务隔离级别，有哪些区别？**

  [MySQL的四种事务隔离级别](https://www.cnblogs.com/huanongying/p/7021555.html)

#### **说一下非公平锁？平时用到的是非公平锁多一点还是公平锁多一点？**

  非公平锁的优点是可以减少唤起线程的开销，整体的吞吐效率高，因为线程有几率不阻塞直接获得锁，CPU不必唤醒所有线程。缺点是处于等待队列中的线程可能会饿死，或者等很久才会获得锁。

#### **谈一下volatile关键字你是怎么理解的？能否保证原子性？（比较synchronized关键字）**

  volatile关键字是线程同步的轻量级实现，所以volatile性能肯定比synchronized关键字要好。但是volatile关键字只能用于变量，而synchronized关键字可以修饰方法以及代码块。synchronized关键字在JavaSE1.6之后进行了优化，主要包括为了减少获得锁和释放锁带来的性能消耗而引入的偏向锁和轻量级锁以及其它各种优化，执行效率有了显著提升，实际开发中使 用 synchronized 关键字的场景还是更多一些。
  
  多线程访问volatile关键字不会发生阻塞，而synchronized关键字可能会发生阻塞。
  
  volatile关键字能保证数据的可见性，但不能保证数据的原子性。synchronized关键字两者都能保证。
  
  volatile关键字主要用于解决变量在多个线程之间的可见性，而 synchronized关键字解决的是多个线程之间访问资源的同步性。

#### **谈一下乐观锁和悲观锁？**

  [面试必备之乐观锁与悲观锁](https://snailclimb.top/JavaGuide/#/./essential-content-for-interview/面试必备之乐观锁与悲观锁)
  
  [面试官：什么是乐观锁请举例 程序员：瑟瑟发抖 不懂啊](https://www.toutiao.com/a6674394835207586311/?timestamp=1559090888&app=news_article&group_id=6674394835207586311&req_id=20190529084808010019054222417A028)

#### **谈一下守护线程？用到过哪种？**
  
  [java 多线程 守护线程](https://segmentfault.com/a/1190000018964390)

#### **ArrayList和LinkedList的区别？**

  [Java中ArrayList和LinkedList区别](https://www.cnblogs.com/huzi007/p/5550440.html)

#### **简单介绍下java中常见的引用类型**

  [java基本类型与引用类型](https://blog.csdn.net/chengbinbbs/article/details/78973453#%E4%B8%80%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  
## 兴盛优先
  
说下面试前奏，我和这个公司互相鸽了一次，第一次我是因为那次在地铁里，信号不好怕影响面试效果，就提前说明了；结果第二次本来约的是晚上8：00，结果9：15分打电话过来面试，*** ，我还在洗衣服。面试官说只要20分钟，如果不方便可以下次约，好像这个面试官是已经下班了，在家里跟我打得电话，我觉得都不容易，还是同意面了。

说来也奇怪，竟然没让我自我介绍，直接上来就跟我聊参与的开源项目 Dubbo,问我为这个项目贡献了哪一块？我轻描淡写的描述了主要负责 Dubbo的哪些生态，和如何管理控制版本的发布等等。因为我主要负责官网的迭代和维护，而Apache项目之间的沟通都是英文交流，老外喜欢用邮件列表的形式来讨论，不会像国内的开源项目，任务认领的方式是在社交软件上进行沟通，老外根本就不用。顺便问了下我英语怎么样？我讲完后，顺便介绍了下我自己。接下来正式进入面试环节。
  
### **一面**
  
#### **谈一谈 Dubbo 序列化协议**

Dubbo 支持 [Hessian](https://zhuanlan.zhihu.com/p/44787200)、[Java 二进制序列化](https://www.zhihu.com/question/47794528/answer/672095170)、json、SOAP 文本序列化多种序列化协议。但是 **Hessian** 是其默认的序列化协议。

#### **谈一下 Dubbo 的整体架构中的网络传输层（Transport）？**

抽象 mina 和 netty 为统一接口，以 Message 为中心，扩展接口为Channel、Transporter、Client、Server和Codec

 [30 道 Dubbo 面试题及答案](https://segmentfault.com/a/1190000018438985)

#### **说一下你最熟悉的项目中，遇到的印象最深刻的问题？是怎么解决的？**

 [Springboot与shiro整合遇到的坑](https://zhuanlan.zhihu.com/p/29161098)
  
#### **说一下在HashMap中遇到的hash冲突是如何解决的？**

[HashMap？面试？我是谁？我在哪](https://zhuanlan.zhihu.com/p/62854712)

原理：HashMap基于哈希表实现的，通过put和get方法存储和获取对象。当调用put方法时，通过键对象的hashCode找到在数组中的位置来存储值对象。当获取对象时的时候，先通过键对象的hashCode找到数组中的位置，然后通过键对象的equals()方法找到正确的值对象。

HashMap使用LinkedList来解决碰撞冲突，当两个对象的hashCode相等时它们在数组的位置相同就会发生碰撞冲突，这个时候对象将会存储在LinkedList的下一个节点中。获取对象的时候通过键对象的equals方法遍历LinkedList直到找到正确的值对象。

#### **谈一下List接口有哪些特性？**

 [深入理解Java中的List、Set与Map集合](https://zhuanlan.zhihu.com/p/34518772)
  
#### **说一下ArrayList和LinkedList区别？**

 [Java中ArrayList和LinkedList区别](https://www.cnblogs.com/huzi007/p/5550440.html)
  
#### **foreach循环里进行元素的remove/add操作，这样合理吗？为什么？**

不合理

[为什么阿里巴巴禁止在 foreach 循环里进行元素的 remove/add 操作](https://juejin.im/entry/5c7c7cae518825620677eebb)

#### **当有线程 T1、T2 以及 T3，如何实现 T1 -> T2 -> T3 的执行顺序？以上问题请至少提供另外一种实现？**
  
  用 Thread 类的 join 方法。
  ```java
private static void threadJoinOneByOne() throws InterruptedException {
        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        // start() 仅是通知线程启动
        t1.start();
        // join() 控制线程必须执行完成
        t1.join();

        t2.start();
        t2.join();

        t3.start();
        t3.join();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}
```
CountDownLatch也可以实现

调整优先级并不能保证控制线程执行顺序
  
#### **好像还有一个问题？是一个专有技术名词的解释？我真的没听过......**


## 御泥坊

这个也是一个朋友内推，工资要砍半，细节我就不说了，直接上干货。

#### **说一下你最熟悉的项目中，遇到的印象最深刻的问题？是怎么解决的？**

 [Springboot与shiro整合遇到的坑](https://zhuanlan.zhihu.com/p/29161098)

#### **说一下TCP/IP 协议**

 [HTTP协议—— 简单认识TCP/IP协议](https://www.cnblogs.com/roverliang/p/5176456.html)

#### **如何让Redis与Mysql数据保持同步？**

[如何保持mysql和redis中数据的一致性？](https://www.zhihu.com/question/319817091/answer/653985863)

#### **如何查询Hashmap里面的元素？(增删改查）**

[【面向对象版】HashMap（增删改查）](https://www.cnblogs.com/liupengpengg/p/6101091.html)

#### **说一下Hashmap 扩容机制？第一次扩容到达的阈值是多少？**

JDK 1.7: [深入理解HashMap的扩容机制](https://www.cnblogs.com/yanzige/p/8392142.html)

JDK 1.8: [jdk1.8 HashMap工作原理和扩容机制(源码解析)](https://blog.csdn.net/u010890358/article/details/80496144)

默认大小为16，负载因子0.75，阈值12


## 拓维信息
这个是Boss直聘找的，本来是另一个HR先跟我聊得，后面他出差了，来了个小姐姐找我。

### **一面**

#### **说一下Spring boot(工作机制，和spring mvc对比优缺点)**

 [这10道springboot常见面试题你需要了解下](https://zhuanlan.zhihu.com/p/58402413)

#### **说一下Spring MVC框架**

  [Spring MVC框架](https://snailclimb.top/JavaGuide/#/./system-design/framework/spring/SpringMVC-Principle?id=%E5%85%88%E6%9D%A5%E7%9C%8B%E4%B8%80%E4%B8%8B%E4%BB%80%E4%B9%88%E6%98%AF-mvc-%E6%A8%A1%E5%BC%8F)

#### **工作中有没有遇到过Mysql优化，请谈一谈**

 [巧用这19条MySQL优化，效率至少提高3倍](https://zhuanlan.zhihu.com/p/60249139)

 [最全 MySQL 优化方法，从此优化不再难](https://zhuanlan.zhihu.com/p/59818056)
 
#### **Mysql一般什么情况查询容易出现索引失效？怎么解决？**

 关联查询
 
 [Mysql之索引失效](https://blog.csdn.net/student__software/article/details/82078786)
 
 [MySQL避免索引失效](https://blog.csdn.net/zsx157326/article/details/79406491)
 
#### **说一下在工作项目中如何运用Redis的？**

 [Redis](https://snailclimb.top/JavaGuide/#/./database/Redis/Redis)

#### **工作中使用Java多态多吗？请简单说一下**

 [浅谈java多态](https://zhuanlan.zhihu.com/p/50190390)
 
 [浅谈Java的多态](https://zhuanlan.zhihu.com/p/29088148)

#### **工作中用过哪些接口？其中List有哪些类？谈一下它们的区别？**

 [工作3年出去面试Java，被鄙视spring的接口有哪些都不清楚](https://www.toutiao.com/a6694111343538078222/?timestamp=1559054464&app=news_article&group_id=6694111343538078222&req_id=20190528224104010152032099253E81B)
 
 [深入理解Java中的List、Set与Map集合](https://zhuanlan.zhihu.com/p/34518772)
 
#### **有使用过Spring Cloud吗？有了解过微服务吗？**

#### **对前端技术有了解吗？**

#### **你这边有什么问题？**


## 陆金所

### **一面**

#### **看我工作时间不长，问我为什么频繁跳槽（间接问离职原因）**

#### **说一下Java类加载机制？**

  [Java类加载机制](https://zhuanlan.zhihu.com/p/25228545)
  
#### **说一下GC中 G1 G2 的算法**

  [G1 收集器原理理解与分析](https://zhuanlan.zhihu.com/p/52841787)

#### **为啥你们公司在使用Mysql,还要使用MongDB?**

  [我为什么放弃MySQL？选择了MongoDB](https://zhuanlan.zhihu.com/p/52810103)
  
#### **说一下 B+树 的理解？**

  [平衡二叉树、B树、B+树、B*树 理解其中一种你就都明白了](https://zhuanlan.zhihu.com/p/27700617)
  
#### **你对索引有了解吗？说一下A ='a',B='b', AB='ab'?**(这个题说实话没听清面试官的意思，应该是问的是否会造成索引失效)。


## 蜜獾信息

### **一面**

#### **说一下最近做过的项目**

#### **你使用过哪些JDK版本？**

#### **用过哪些集合包？**

  ArrayList、LinkedList、Vector、Stack、HashSet、TreeSet、HashMap、TreeMap
  
  [深入理解Java中的List、Set与Map集合](https://zhuanlan.zhihu.com/p/34518772)

#### **说一下ArrayList、LinkedList、HashMap 底层数据结构**

  [Arraylist 与 LinkedList 区别?](https://snailclimb.top/JavaGuide/#/./java/collection/Java%E9%9B%86%E5%90%88%E6%A1%86%E6%9E%B6%E5%B8%B8%E8%A7%81%E9%9D%A2%E8%AF%95%E9%A2%98?id=arraylist-%E4%B8%8E-linkedlist-%E5%8C%BA%E5%88%AB)

  [一篇文章搞定ArrayList和LinkedList所有面试问题](https://zhuanlan.zhihu.com/p/45967570)

  [HashMap底层实现原理（上）](https://zhuanlan.zhihu.com/p/28501879)
  
  [HashMap底层实现原理（下）](https://zhuanlan.zhihu.com/p/28587782)

#### **Arraylist 是有序还是无序？**
有序

#### **有哪些方式可以实现多线程？**

  [Java多线程实现的四种方式](https://zhuanlan.zhihu.com/p/47401636)
  
#### **用过哪些并发包（我反问面试官是不是JUC，为何他说不是？）**

  [java并发包、线程池、锁](https://zhuanlan.zhihu.com/p/43618142)
  
#### **说一下sleep( ) 和 wait( )的区别？**

  [sleep( ) 和 wait( ) 的这 5 个区别，你知道几个？](https://zhuanlan.zhihu.com/p/45666264)

#### **开发过程中遇到过哪些异常？/Exception 与 error的区别？/说一下error层次结构？**

  [Java异常处理](https://zhuanlan.zhihu.com/p/37072375)
  
#### **用过哪些数据库？/说一下Mysql 四种事务隔离级别/哪种级别最高？为什么？**

  [真正理解Mysql的四种事务隔离级别](https://www.jianshu.com/p/75187e19faf2)
  
#### **用过索引吧？在使用索引需要注意什么？（如何避免索引失效？）**

  [如何理解并正确使用MySql索引](https://zhuanlan.zhihu.com/p/27835355)
  
  [Mysql索引简明教程](https://zhuanlan.zhihu.com/p/40820574)
  
  [Mysql之索引失效](https://blog.csdn.net/student__software/article/details/82078786)
 
  [MySQL避免索引失效](https://blog.csdn.net/zsx157326/article/details/79406491)

#### **说一下Spring MVC框架**

 [Spring MVC框架](https://snailclimb.top/JavaGuide/#/./system-design/framework/spring/SpringMVC-Principle?id=%E5%85%88%E6%9D%A5%E7%9C%8B%E4%B8%80%E4%B8%8B%E4%BB%80%E4%B9%88%E6%98%AF-mvc-%E6%A8%A1%E5%BC%8F)
 
#### **http 和 https 的区别？**

`http`就是我们说的超文本传输协议，这个协议它是用一种明文的方式发送我们的内容，没有任何的加密。比如说我们访问一个网站，我们可能需要在这个网站输入密码，登录账号之类的操作，那我们的账号和密码就会发送到网站的服务器上面。但要是有人在中途截取了我们的信息，那我们的一些比较重要的信息可能就暴露了，所以为了解决`http`在传输过程中不加密的问题，之后就增加了一个SSL协议，这个协议简单说就是一个提供数据安全和完整性的协议，也就是负责网络连接的加密。

比如我们访问一个`https`的网站，那我们的电脑就会先和服务器建立一个安全的连接通道，然后服务器会先发送一份网站的证书信息到我们电脑，就相当于是告诉我们电脑，你访问的服务器没有问题。确认了信息之后，我们服务器就会生成一个加锁的箱子，但是这把锁有两把不一样的钥匙，一把是给我们电脑的，另一把是服务器自己的。然后服务器就会把没有上锁的箱子和钥匙发给我们电脑，我们把信息放在箱子里面之后，用钥匙锁上，然后发给服务器，服务器再用自己的钥匙打开箱子，来保证信息的安全。在这个过程中，即使箱子被别人拦截了，因为没有服务器的钥匙，以目前的技术来讲，还是很难打开箱子的。所以现在的一些大的网站，尤其是购物网站、或者是需要我们登录的网站，基本上都是`https`的。

  [http 和 https 有何区别？如何灵活使用？](https://www.zhihu.com/question/19577317/answer/103499193)

#### **一般数据都是以什么形式传给前端？**
json格式

  [前后端数据交互之前端传值到后台](https://blog.csdn.net/henouren/article/details/78282406)

#### **你这边还有什么问题？**

## 丰巢科技

#### **自我介绍**
看到我说的和简历上的没差别，就没让我继续说了

#### **你平时是怎么学习技术的？**

#### **有中间件开发经验吗？**

#### **如何搭建Nacos/dubbo平台？**

#### **说一下Spring MVC框架**

 [Spring MVC框架](https://snailclimb.top/JavaGuide/#/./system-design/framework/spring/SpringMVC-Principle?id=%E5%85%88%E6%9D%A5%E7%9C%8B%E4%B8%80%E4%B8%8B%E4%BB%80%E4%B9%88%E6%98%AF-mvc-%E6%A8%A1%E5%BC%8F)
 
#### **Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？**

第一种是使用<resultMap>标签，逐一定义列名和对象属性名之间的映射关系。第二种是使用sql列的别名功能，将列别名书写为对象属性名，比如T_NAME AS NAME，对象属性名一般是name，小写，但是列名不区分大小写，Mybatis会忽略列名大小写，智能找到与之对应对象属性名，你甚至可以写成T_NAME AS NaMe，Mybatis一样可以正常工作。
有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。

[十道常见的mybatis面试题](https://zhuanlan.zhihu.com/p/61432692)

#### **谈一谈公平锁和非公平锁？**

[最全Java锁详解：独享锁/共享锁+公平锁/非公平锁+乐观锁/悲观锁](https://zhuanlan.zhihu.com/p/54551800)

[两程序员玩“锁”，一人抢救无效身亡](https://zhuanlan.zhihu.com/p/34510121)

#### **简单聊下线程池？**

[线程池你真不来了解一下吗？](https://zhuanlan.zhihu.com/p/36475103)

[当面试官问线程池时，你应该知道些什么？](https://zhuanlan.zhihu.com/p/62132884)

#### **简单说一下Java内存模型（JMM)**

[Java内存模型（JMM）总结](https://zhuanlan.zhihu.com/p/29881777)

#### **工作中有没有Mysql优化的经验，请谈一谈**

 [巧用这19条MySQL优化，效率至少提高3倍](https://zhuanlan.zhihu.com/p/60249139)

 [最全 MySQL 优化方法，从此优化不再难](https://zhuanlan.zhihu.com/p/59818056)

#### **谈一下索引数据结构**

[数据库索引数据结构总结](https://zhuanlan.zhihu.com/p/47046781)

#### **简述 B+Tree**

[二叉树学习笔记之B树、B+树、B*树](https://yq.aliyun.com/articles/38345)

#### **谈一谈单链表和双链表的区别？**

**单链表**：单链表只有一个指向下一节点的指针，也就是只能next。

**双链表**：双链表除了有一个指向下一节点的指针外，还有一个指向前一结点的指针，可以通过prev快速找到前一结点。一般我们都构造双向循环链表。

[数据结构与算法-链表(上)](https://zhuanlan.zhihu.com/p/52878334)

#### **谈谈 synchronized 和 ReentrantLock 的区别**

[谈谈 synchronized 和 ReentrantLock 的区别](https://snailclimb.top/JavaGuide/#/./essential-content-for-interview/PreparingForInterview/美团面试常见问题总结?id=_3-谈谈-synchronized-和-reentrantlock-的区别)

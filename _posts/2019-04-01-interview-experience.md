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

## 平安产险面试（电话面试） 深圳
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

## 飞猪面试（电话面试） 杭州
首先这个面试机会是来自于内推，当然内推的人和我一面的面试官都是同一个人，所以 嘿嘿嘿 你懂得...

### **一面**

#### **自我介绍**

#### **介绍一下你这边最熟悉的项目？在开发过程中印象最深刻地方？**

#### **Springboot 2.0.0和Springboot 1.5.6的区别？**
 
  [https://github.com/spring-projects/spring-boot/wiki](https://github.com/spring-projects/spring-boot/wiki)

#### **有没有看过Springboot的源码？（很尴尬，没有研究过）**

  [https://github.com/spring-projects/spring-boot](https://github.com/spring-projects/spring-boot)

#### **Springboot中遇到的一些坑及解决方法？**
 
  [Springboot与shiro整合遇到的坑](https://zhuanlan.zhihu.com/p/29161098)

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
  
  [JVM 发生 OOM 的 8 种原因、及解决办法](https://zhuanlan.zhihu.com/p/63752449)
  
  因为OutOfMemoryError是可以catch的。catch之后吞掉的话程序还能试着继续运行。例如说以前见过的一个案例是：一个Java服务器端应用，有段代码没写对导致有一个线程在疯狂创建大数组对象——直到OOM。这个线程注册的uncaught exception handler捕获到了这个异常，记录了日志，然后就把这个异常吞掉了。这样还能继续正常跑下去是因为：只是一个创建很大的数组对象的请求失败了而已，而出错的那个方法由于异常处理已经被退出了，程序的其它部分并没有受影响。

#### **介绍下Java内存模型？**

  在 JDK1.2 之前，Java的内存模型实现总是从主存（即共享内存）读取变量，是不需要进行特别的注意的。而在当前的 Java 内存模型下，线程可以把变量保存本地内存比如机器的寄存器）中，而不是直接在主存中进行读写。这就可能造成一个线程在主存中修改了一个变量的值，而另外一个线程还继续使用它在寄存器中的变量值的拷贝，造成数据的不一致。
  
  要解决这个问题，就需要把变量声明为volatile，这就指示 JVM，这个变量是不稳定的，每次使用它都到主存中进行读取。
  
  说白了，volatile关键字的主要作用就是保证变量的可见性然后还有一个作用是防止指令重排序。

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

  https://snailclimb.top/JavaGuide/#/./java/Multithread/JavaConcurrencyAdvancedCommonInterviewQuestions?id=_1-synchronized-关键字

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
而调整优先级并不能保证控制线程执行顺序

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

  见飞猪面试
  
#### **JDBC如何连接数据库？**
  [JDBC【介绍JDBC、使用JDBC连接数据库、简单的工具类】](https://zhuanlan.zhihu.com/p/33828916)

两位技术负责人+部长（周）简单聊了一下，自己的项目和经验，遇到过哪些问题？怎么解决的？怎么设计数据库模型？

## 浩鲸科技（电话面试） 杭州

### **一面**

#### **自我介绍**

#### **谈一下自己最熟悉的项目中的业务框架？**
（登录+权限VIP服务绑定）

#### **是怎样提交给前端接口的？**

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


## 上海爱海斯信息技术有限公司（杏仁医生）

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

#### **谈一下守护线程？用到过哪种？**
  
  [java 多线程 守护线程](https://segmentfault.com/a/1190000018964390)

#### **ArrayList和LinkedList的区别？**

  [Java中ArrayList和LinkedList区别](https://www.cnblogs.com/huzi007/p/5550440.html)

#### **简单介绍下java中常见的引用类型**

  [java基本类型与引用类型](https://blog.csdn.net/chengbinbbs/article/details/78973453#%E4%B8%80%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  
## 湖南兴盛优先电子商务有限公司
  
说下面试前奏，我和这个公司互相鸽了一次，第一次我是因为那次在地铁里，信号不好怕影响面试效果，就提前说明了；结果第二次本来约的是晚上8：00，结果9：15分打电话过来面试，fuck，我还在洗衣服。面试官说只要20分钟，如果不方便可以下次约，好像这个面试官是已经下班了，在家里跟我打得电话，我觉得都不容易，还是同意面了。

说来也奇怪，竟然没让我自我介绍，直接上来就跟我聊参与的开源项目 Dubbo,问我为这个项目贡献了哪一块？我轻描淡写的描述了主要负责 Dubbo的哪些生态，和如何管理控制版本的发布等等。因为我主要负责官网的迭代和维护，而Apache项目之间的沟通都是英文交流，老外喜欢用邮件列表的形式来讨论，不会像国内的开源项目，任务认领的方式是在社交软件上进行沟通，老外根本就不用。顺便问了下我英语怎么样？我讲完后，顺便介绍了下我自己。接下来正式进入面试环节。
  
### **一面**
  
#### **谈一谈 Dubbo 序列化**
  
#### **谈一下 Dubbo 的整体架构中的网络传输层（Transport）？**

 [30 道 Dubbo 面试题及答案](https://segmentfault.com/a/1190000018438985)

#### **说一下你最熟悉的项目中，遇到的印象最深刻的问题？是怎么解决的？**

 [Springboot与shiro整合遇到的坑](https://zhuanlan.zhihu.com/p/29161098)
  
#### **说一下在HashMap中遇到的hash冲突是如何解决的？**
  
#### **谈一下List接口有哪些特性？**

 [深入理解Java中的List、Set与Map集合](https://zhuanlan.zhihu.com/p/34518772)
  
#### **说一下ArrayList和LinkedList区别？**

 [Java中ArrayList和LinkedList区别](https://www.cnblogs.com/huzi007/p/5550440.html)
  
#### **foreach循环里进行元素的remove/add操作，这样合理吗？**
  
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
而调整优先级并不能保证控制线程执行顺序
  
#### **好像还有一个问题？是一个专有技术名词的解释？我真的没听过......**

---
layout:     post
title:      "Spring IOC 容器源码分析"
subtitle:   "异步化改造,三大中心改造,服务治理增强"
date:       2019-03-28
author:     "caojiele"
header-img: "img/in-post/2019.03/28/post-spring-ioc.jpg"
tags:
    - Spring
    - IOC
    - Java
---

Spring 最重要的概念是 IOC 和 AOP，本篇文章其实就是要带领大家来分析下 Spring 的 IOC 容器。既然大家平时都要用到 Spring，怎么可以不好好了解 Spring 呢？阅读本文并不能让你成为 Spring 专家，不过一定有助于大家理解 Spring 的很多概念，帮助大家排查应用中和 Spring 相关的一些问题。

本文采用的源码版本是 4.3.11.RELEASE，算是 5.0.x 前比较新的版本了。为了降低难度，本文所说的所有的内容都是基于 xml 的配置的方式，实际使用已经很少人这么做了，至少不是纯 xml 配置，不过从理解源码的角度来看用这种方式来说无疑是最合适的。

阅读建议：读者至少需要知道怎么配置 Spring，了解 Spring 中的各种概念，少部分内容我还假设读者使用过 SpringMVC。本文要说的 IOC 总体来说有两处地方最重要，一个是创建 Bean 容器，一个是初始化 Bean，如果读者觉得一次性看完本文压力有点大，那么可以按这个思路分两次消化。读者不一定对 Spring 容器的源码感兴趣，也许附录部分介绍的知识对读者有些许作用。

希望通过本文可以让读者不惧怕阅读 Spring 源码，也希望大家能反馈表述错误或不合理的地方。

**目录**

## 引言

先看下最基本的启动 Spring 容器的例子：

以上代码就可以利用配置文件来启动一个 Spring 容器了，请使用 maven 的小伙伴直接在 dependencies 中加上以下依赖即可，个人比较反对那些不知道要添加什么依赖，然后把 Spring 的所有相关的东西都加进来的方式。

> spring-context 会自动将 spring-core、spring-beans、spring-aop、spring-expression 这几个基础 jar 包带进来。

多说一句，很多开发者入门就直接接触的 SpringMVC，对 Spring 其实不是很了解，Spring 是渐进式的工具，并不具有很强的侵入性，它的模块也划分得很合理，即使你的应用不是 web 应用，或者之前完全没有使用到 Spring，而你就想用 Spring 的依赖注入这个功能，其实完全是可以的，它的引入不会对其他的组件产生冲突。

废话说完，我们继续。`ApplicationContext context = new ClassPathXmlApplicationContext(...)` 其实很好理解，从名字上就可以猜出一二，就是在 ClassPath 中寻找 xml 配置文件，根据 xml 文件内容来构建 ApplicationContext。当然，除了 ClassPathXmlApplicationContext 以外，我们也还有其他构建 ApplicationContext 的方案可供选择，我们先来看看大体的继承结构是怎么样的：

![1](http://upload-images.jianshu.io/upload_images/6039661-8d78cf47750ada18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 读者可以大致看一下类名，源码分析的时候不至于找不着看哪个类，因为 Spring 为了适应各种使用场景，提供的各个接口都可能有很多的实现类。对于我们来说，就是揪着一个完整的分支看完。
> 
> 当然，读本文的时候读者也不必太担心，每个代码块分析的时候，我都会告诉读者我们在说哪个类第几行。

我们可以看到，ClassPathXmlApplicationContext 兜兜转转了好久才到 ApplicationContext 接口，同样的，我们也可以使用绿颜色的 **FileSystemXmlApplicationContext** 和 **AnnotationConfigApplicationContext** 这两个类。

**FileSystemXmlApplicationContext** 的构造函数需要一个 xml 配置文件在系统中的路径，其他和 ClassPathXmlApplicationContext 基本上一样。

**AnnotationConfigApplicationContext** 是基于注解来使用的，它不需要配置文件，采用 java 配置类和各种注解来配置，是比较简单的方式，也是大势所趋吧。

不过本文旨在帮助大家理解整个构建流程，所以决定使用 ClassPathXmlApplicationContext 进行分析。

我们先来一个简单的例子来看看怎么实例化 ApplicationContext。

首先，定义一个接口：

定义接口实现类：

接下来，我们在 **resources** 目录新建一个配置文件，文件名随意，通常叫 application.xml 或 application-xxx.xml 就可以了：

这样，我们就可以跑起来了：

以上例子很简单，不过也够引出本文的主题了，就是怎么样通过配置文件来启动 Spring 的 ApplicationContext？也就是我们今天要分析的 IOC 的核心了。ApplicationContext 启动过程中，会负责创建实例 Bean，往各个 Bean 中注入依赖等。

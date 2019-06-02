---
layout:     post
title:      "初识 Nacos(上）"
subtitle:   "学习《Spring Cloud 服务发现新选择》"
date:       2018-09-21
author:     "caojiele"
header-img: "img/in-post/2018.09/21/post-alibaba-nacos-discovery1.png"
tags:
    - Spring Cloud
    - Nacos
    - Java
---

> 本文来自于我的简书：[初识 Nacos(上） 学习《Spring Cloud 服务发现新选择》](https://www.jianshu.com/p/b374a7b10486)，转载请保留链接 ;)

最近在从零接触Alibaba 开源项目Nacos,学习的是[小马哥(mercyblitz)](https://github.com/mercyblitz)的技术周报，之前看了后忘记总结，导致也没有什么印象。所以现在决定学习一章，写一篇学习感悟，并且持续更新下去。首先这一章节主要讲得是服务发现(Service Discovery)，作为 Spring Cloud 最核心功能特性之一，受到业界的广泛关注。
![文章主题](https://raw.githubusercontent.com/caojiele/caojiele.github.io/master/img/in-post/2018.09/21/post-theme.png)

## Spring Cloud 整体架构

在现行的 Spring Cloud 服务发现技术体系中，以 Spring Cloud Eureka 为典型代表，它作为官方推荐解决方案，被业 界广泛运用，然而其设计缺陷也非常之明显。还有Spring Cloud Zookeeper和Spring Cloud Consul。那么先介绍这三种的特点吧。
![整体架构](https://raw.githubusercontent.com/caojiele/caojiele.github.io/master/img/in-post/2018.09/21/post-architecture.png)

### Spring Cloud Eureka 特点
#### 优点：
* Spring Cloud 背书 - 推荐服务发现方案
* CAP 理论 - AP模型，数据最终一致
* 简单易用 - 开箱即用，控制台管理

#### 缺点：
* 内存限制 - 客户端上报完整注册信息，造成服务端内存浪费
* 单一调度更新 - 客户端简单轮训更新，增加服务器压力
* 集群伸缩性限制 - 广播式复制模型，增加服务器压力

### Spring Cloud Zookeeper 特点
#### 优点：
* 成熟协调系统 - Dubbo、Spring Cloud等适配方案
* CAP理论 - CP模型，ZAB算法，强数据一致性

#### 缺点：
* 维护成本 - 客户端、Session状态、网络故障
* 伸缩性限制 - 内存、GC、连接

### Spring Cloud Consul 特点
#### 优点：
* 通用方案 - 适用于 Service Mesh、 Java 生态
* CAP理论 - AP 模型，Raft+Gossip 算法，数据最终一致

#### 缺点：
* 可靠性无法保证 - 未经过大规模验证
* 非 Java 生态 - 维护和问题排查困难

综上所述，让我得出了Spring Cloud服务发现方案对比结果:
![方案对比结果](https://raw.githubusercontent.com/caojiele/caojiele.github.io/master/img/in-post/2018.09/21/post-compare.png)

那么这三种服务发现的基本模式是怎样的呢？现在来谈谈Spring cloud 服务器发现模式。
* 首先都是服务器启动 - 启动注册中心
* 然后增加客户端依赖 - `sping-cloud-start-*`
* 最后就是客户端注册 - 记得在`XXApplication.java`文件中添加`@EnableDiscoveryClient`，注解开启服务注册与发现功能。

以下我以Eureka发现模式为例：
* 首先去[Spring Initializr](https://start.spring.io)快速创建Eureka服务端和客户端应用程序，然后导入自己的IDE。当然你如果嫌麻烦，也可以直接导入已经写好的[工程](https://github.com/mercyblitz/tech-weekly/tree/master/2018.09.21%E3%80%8C%E5%B0%8F%E9%A9%AC%E5%93%A5%E6%8A%80%E6%9C%AF%E5%91%A8%E6%8A%A5%E3%80%8D-%20%E7%AC%AC%E4%B8%80%E6%9C%9F%E3%80%8ASpring%20Cloud%20%E6%9C%8D%E5%8A%A1%E5%8F%91%E7%8E%B0%E6%96%B0%E9%80%89%E6%8B%A9%20-%20Alibaba%20Nacos%20Discovery%E3%80%8B/%E4%BB%A3%E7%A0%81)。
* 然后在`resources-application.properties`中分别配置好两者的端口号，像客户端这块还需要写好应用名称、以及Eureka 服务器地址。
* 最后我们就直接可以run`XXApplication.java`了，像我的服务端端口是`12345`，就访问[localhost:12345](localhost:12345)。页面跳转如下图所示，恭喜你的Eureka服务已经起来了。
* Eureka-client亦如此，成功run起来后，在之前的服务端页面，也就是[localhost:12345](localhost:12345)，刷新下会在`Instances currently registered with Eureka`出现`EUREKA-CLIENT`的状态信息。

spring-cloud-alibaba-nacos-discovery 作为 Spring Cloud Alibaba 服务发现的核心模块，其架构基础与 Spring Cloud 现行方案相同，均构建在 Spring Cloud Commons 抽象。因此，它在 Spring Cloud 服务发现的使用上，开发人员将不会心存任何的违和感。

## Alibaba Nacos 生态介绍
从功能特性而言，spring-cloud-alibaba-nacos-discovery 仅是 Nacos 在 Spring Cloud 服务发现的解决方案，Nacos 在 Spring Cloud 中还支持分布式配置的特性。与开源产品不同的是，Nacos 曾经历过中国特色的超大流量考验，以及巨型规模的集群实施，无论从经验积累还是技术沉淀，现行 Spring Cloud 解决方案 都是无法比拟的。然而这并非说明它完美无缺，在内部的评估和讨论中，也发现其中差距和文化差异。为了解决这些问题，讨论将从整体架构和设计思考两个方面，介绍 Nacos 与 Spring 技术栈整合情况，以及与其他开源方案的适配思考，整体上，降低 Nacos 使用门槛，使迁移成本接近为零，达到“一次开发，到处运行”的目的。
那么接下来我们通过Github上，Spring Cloud Alibaba项目中官方给出的指导文档来配置启动 Nacos吧。

### 下载注册中心

1. 首先需要获取 Nacos Server，支持直接下载和源码构建两种方式。

	1. 直接下载：[Nacos Server 下载页](https://github.com/alibaba/nacos/releases) 
	2. 源码构建：进入 Nacos [Github 项目页面](https://github.com/alibaba/nacos)，将代码 git clone 到本地自行编译打包，[参考此文档](https://nacos.io/zh-cn/docs/quick-start.html)。**推荐使用源码构建方式以获取最新版本**

### 启动注册中心

2. 启动 Server，进入解压后文件夹或编译打包好的文件夹，找到如下相对文件夹 nacos/bin，并对照操作系统实际情况之下如下命令。
	
	1. Linux/Unix/Mac 操作系统，执行命令 `sh startup.sh -m standalone`
	1. Windows 操作系统，执行命令 `cmd startup.cmd`

### 增加第三方依赖

3. 首先，修改 pom.xml 文件，引入 Nacos Discovery Starter。
```mongoDB
	    <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
```
### 外部化配置	

4. 在应用的 /src/main/resources/application.properties 配置文件中配置 Nacos Server 地址
```mongoDB	
		spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
```
### 激活服务发现	

5. 使用 @EnableDiscoveryClient 注解开启服务注册与发现功能（`SpringApplication.run`)
```mongoDB		
		@SpringBootApplication
		@EnableDiscoveryClient
		public class ProviderApplication {

			public static void main(String[] args) {
				SpringApplication.run(Application.class, args);
			}

			@RestController
			class EchoController {
				@RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
				public String echo(@PathVariable String string) {
						return string;
				}
			}
		}
```

### 应用启动

6. 增加配置，在 nacos-discovery-provider-example 项目的 /src/main/resources/application.properties 中添加基本配置信息
```mongoDB	
		spring.application.name=service-provider
		server.port=18082
```
		
7. 启动应用，支持 IDE 直接启动和编译打包后启动。

	1. IDE直接启动：找到 nacos-discovery-provider-example 项目的主类 `ProviderApplication`，执行 main 方法启动应用。
	2. 打包编译后启动：在 nacos-discovery-provider-example 项目中执行 `mvn clean package` 将工程编译打包，然后执行 `java -jar nacos-discovery-provider-example.jar`启动应用。

### 验证

#### 检验服务发现
在浏览器输入此地址[http://127.0.0.1:8848/nacos/v1/ns/instances?serviceName=service-provider](http://127.0.0.1:8848/nacos/v1/ns/instances?serviceName=service-provider) 并点击跳转，可以看到服务节点已经成功注册到 Nacos Server。

![查询服务](https://cdn.nlark.com/lark/0/2018/png/54319/1536986288092-5cf96af9-9a26-466b-85f6-39ad1d92dfdc.png)

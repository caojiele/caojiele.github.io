---
layout:     post
title:      "开篇-分布式系统中的那些开源软件"
subtitle:   "讨论一个大型话题：分布式系统所能采用的主流软件"
date:       2019-04-09
author:     "caojiele"
header-img: "img/in-post/2019.04/09/post-bg-software-distributed-system.jpg"
tags:
    - 分布式
    - Java
    - 慕课网手记
---

> 本文来自于我的[慕课网手记](https://www.imooc.com/u/4024769)：[开篇-分布式系统中的那些开源软件](https://www.imooc.com/article/284696)，转载请保留链接 ;)


![微服务框架历史演进](https://cdn.nlark.com/yuque/0/2019/png/338441/1566474998506-b5c65f28-53a2-48ea-a49d-e912cdc49075.png)

我们来讨论一个大型话题，把分布式系统所能采用的开源或者商业软件，方方面面都来讨论一下。这里做个记录，也算是我加入慕课网认证作者的一个里程碑，今后的文章也是会和这些软件相关的，毕竟单体的项目已经不复返，分布式的项目已经成为了主流。不管你看到这个大纲可能有的熟悉，还是有的不了解，没关系，我们今后会一个个掰开的学习掌握它们，（熟悉的就要更加熟悉，不会的就要学会并掌握它。）当然，这篇文章不能代表所有分布式所用到的技术，也欢迎各位在后面评论中留言补充。

![微服务框架的常见特性](https://pic4.zhimg.com/80/v2-c370436f1ddce659b60d35595d4445c7_hd.jpg)

**基础框架**

Spring Cloud，Dubbo，Motan，Sofa



**分布式注册中心**

Eureka（Netflix），Consul，Nacos，Etcd，Zookeeper



**分布式监控中心**

CAT，SBA，Prometheus，Grafana



**分布式配置中心**

Apollo，Nacos，DisConf，Spring Cloud Config



**分布式网关**

F5，Ngnix+（打通Consul），ESB，Kong，zuul,  gateway



**分布式事务**

Seata，dts，tcc-transaction，hmily，ByteTCC，myth，EasyTransaction，tx-lcn



**分布式日志系统**

ELK(Kibana，ElasticSearch，Logstash)，Kafka，Flume，Splunk



**分布式定时任务调度和管理**

Elastic Job，XXL Job



**分布式限流熔断降级**

Sentinel，Redis，Guava



**分布式服务权限控制系统**

OAuth，JWT，单点登录，Hystrix，shiro



**分布式监控中心**

CAT，SBA，Prometheus，Grafana，Graphite，Statsd，Solarwinds，Zabbix，Centreon，appDynamics，new relic，Kaeger



**分布式服务和系统诊断**

Arthas



**分布式调用链**

CAT，SkyWalking+RocketBolt，Zipkin，DynaTrace



**分布式流程和服务编排**

Coroutine，Akka，Kilim，Flowable，Axon



**分布式锁**

Redisson，Redis，Zookeeper



**分布式压测平台**

JMeter，LoadRunner



**分布式全局主键系统**

Redis，Zookeeper，Twitter Snowflake



**分布式自动化测试**

Postman、Jenkins



**分布式自动化API文档**

Swagger



**分布式分库分表中间件**

**多数据源**

Sharding Sphere，MyCat



**分布式消息队列中间件**

RocketMQ，Kafka，ActiveMQ，Tibco



**分布式缓存**

Redis、MongoDB



**分布式数据库分析诊断系统**

慢SQL，听云



**分布式自动化数据库脚本升级**

Flyway



**异构系统**

Spring Cloud Sidecar，Service Mesh，istio，Sofa mesh



**异构网关**



**运维发布**

DevOps，CICD和Pipeline，容器(Docker)化，K8S，Jenkins，蓝鲸，TriAquae，Choerodon（猪齿鱼）

![Spring cloud 中间件生态](https://cdn.nlark.com/yuque/0/2019/png/338441/1566474998581-67fb061e-bec1-43bb-9337-09bac790c75b.png)
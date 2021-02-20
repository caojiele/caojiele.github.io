---
layout:     post
title:      "三诺云底层技术分享"
subtitle:   "Sino cloud underlying technology sharing"
header-img: "img/in-post/2020.12/31/sino-cloud.png"
date:       2020-12-31
author:     "caojiele"
tags:
    - 三诺云
    - 后端
    - 技术分享
---

# GIT多源提交代码 `xxx` 为 Git Remotes Name

+ git push -u `xxx` master

# Maven私库设置

> 请将 [Maven Setting](doc/settings.xml "Setting") 复制到本地私库缓存根目录下，默认在`{userhome}/.m2`下

# 环境依赖

> * 【必选】JDK: 1.8
> * 【必选】Maven: 3.3+
> * 【必选】MySql: 5.7+
> * 【必选】Redis: 4.0+
> * 【必选】Nacos: 1.1.3+
> * 【可选】Sentinel: 1.5.0+

# 插件依赖

> * 【必选】Lombok Plugin
> * 【可选】MybatisX Plugin

# JVM启动参数，为了避免容器无限使用资源，请务必进行设置

> * 【必选】 `-XX:MetaspaceSize=128m`            （元空间默认大小）
> * 【必选】 `-XX:MaxMetaspaceSize=128m`         （元空间最大大小）
> * 【必选】 `-XX:ReservedCodeCacheSize=50m`      (限制CacheCode最大大小)
> * 【必选】 `-Xmx256m`                          （堆最大大小）
> * 【必选】 `-Xms128m`                          （堆默认大小）
> * 【必选】 `-Xmn32m`                           （新生代大小）
> * 【必选】 `-Xss256k`                          （棧最大深度大小）
> * 【可选】 `-XX:SurvivorRatio=6`               （新生代分区比例 6:4）
> * 【可选】 `-XX:+UseConcMarkSweepGC`           （指定使用的垃圾收集器，这里使用CMS收集器）
> * 【可选】 `-Dnacos=xxxxx`                      (设置nacos服务地址,默认使用指定的开发)
> * 【可选】 `-Dnamespace=xxxxx`                  (设置nacos名空间)
> * 【可选】 `-Dsentinel=xxxxx`                   (设置sentinel服务地址)
> * 【可选】 `-Dseata=xxxxx`                      (设置seata服务地址)
> * 【可选】 `-Dzipkin=xxxxx`                     (设置zipkin服务地址)
> * 【可选】 `-Delk=xxxxx`                        (设置elk服务地址)
> * 【可选】 `--mpw.key=xxxx`                     (设置MP解密密钥，用于DB密码解密)

# Sino-Boot 模块介绍 `2.6.0`

> ###### `sino-boot`工程已集成常用组件和核心运行机制，_请勿擅自在业务层拓展重复逻辑_
>
>  *[x] 【总装】**sino-bom** 集中版本配置，用于boot工程所有内外部构件库依赖的版本声明
>  *[x] 【内核】**sino-core-auto 工程自动化，编译时根据代码自动生成`spi`声明文件或`spring.factories`**
>  *[x] 【内核】**sino-core-boot** 核心包总装，覆盖核心组件，默认最小核心依赖
>  *[x] 【内核】**sino-core-cloud** 分布式协议设定、接口版本、RPC、熔断
>  *[x] 【内核】**sino-core-common** 公共约定、工具包
>  *[x] 【内核】**sino-core-context** 链路追逐上下文自定义管理
>  *[x] 【内核】**sino-core-db** 数据库连接池默认配置
>  *[x] 【内核】**sino-core-dubbo** dubbo和feign双模服务注册
>  *[x] 【内核】**sino-core-launch** 服务启动自定义封装、服务常量
>  *[x] 【内核】**sino-core-log4j2** LOG日志启动封装
>  *[x] 【内核】**sino-core-oss** OSS对象存储抽象定义
>  *[x] 【内核】**sino-core-secure** 权限认证模块抽象封装
>  *[x] 【内核】**sino-core-sms** 短信模块抽象定义
>  *[x] 【内核】**sino-core-gateway** 网关模块实现
>  *[x] 【框架】**sino-platform** 平台业务工程框架
>  *[x] 【插件】**sino-plugin-actuate** 暴露端点,请求拦截设置
>  *[x] 【插件】**sino-plugin-api-crypto** API请求加密签名支撑
>  *[x] 【插件】**sino-plugin-auth** 安全模块基础对象声明和安全工具包实现
>  *[x] 【插件】**sino-plugin-cache** 缓存抽象定义
>  *[x] 【插件】**sino-plugin-datascope** 数据权限封装
>  *[x] 【插件】**sino-plugin-develop** 代码在线生成封装
>  *[x] 【插件】**sino-plugin-ehcache** ehcache缓存封装
>  *[x] 【插件】**sino-plugin-excel** excel导入、导出组件封装
>  *[x] 【插件】**sino-plugin-http** httpclient组件封装，用于SDK底层调用
>  *[x] 【插件】**sino-plugin-ldap** LDAP同步插件封装
>  *[x] 【插件】**sino-plugin-log** log日志封装
>  *[x] 【插件】**sino-plugin-mongo** mongo拓展
>  *[x] 【插件】**sino-plugin-mybatis** mybatis拓展
>  *[x] 【插件】**sino-plugin-oss-aliyun** 阿里云OSS封装
>  *[x] 【插件】**sino-plugin-oss-all** OSS存储桶操作模型定义
>  *[x] 【插件】**sino-plugin-oss-minio** Minio存储封装
>  *[x] 【插件】**sino-plugin-oss-tencent** 腾讯云OSS封装
>  *[x] 【插件】**sino-plugin-redis** redis拓展
>  *[x] 【插件】**sino-plugin-ribbon** 负载均衡策略拓展，用于多人协作开发和服务的灰度发布
>  *[x] 【插件】**sino-plugin-rocket** rocketMQ拓展
>  *[x] 【插件】**sino-plugin-sms-aliyun** 阿里云短信封装
>  *[x] 【插件】**sino-plugin-sms-all** 短信操作模型定义
>  *[x] 【插件】**sino-plugin-sms-tencent** 腾讯短信封装
>  *[x] 【插件】**sino-plugin-sms-cloopen** 容联云短信封装
>  *[x] 【插件】**sino-plugin-swagger** API文档拓展
>  *[x] 【插件】**sino-plugin-tenant** 多租户模型封装
>  *[x] 【插件】**sino-plugin-trace** 链路追踪组件拓展
>  *[x] 【插件】**sino-plugin-transaction** 分布式事务拓展

# Nacos配置说明

> 请参考 [Nacos Config](/doc/doc/nacos/*.yaml "Nacos Config") 配置模版


# 判断当前环境类型

> - CommonUtil.getEnv(); 获取环境代码
> - CommonUtil.isProd(); 判断是否正式环境
> - CommonUtil.isTest(); 判断是否测试环境
> - CommonUtil.isDev();  判断是否开发环境
> - CommonUtil.call(Callable callable, String... env);  设定指定环境被执行


# 常规操作

- ### 带id和parentId列表自动合并成树形Json:

> ForestNodeMerger.merge(baseMapper.tree());

- ### 获取当前用户；

> - 1、Principal account = SecureUtil.getUser(); //通过AuthUtil工具包获取，常用于serverice层；
> - 2、public R<List<OrgVO>> tree(String tenantId, Principal sinoUser){} //在controller方法中直接设置参数接收


- ### Func常规操作类

> 参考 [Func](/doc/util/Func.text "Func")

- ### Auth工具类

> 参考 [AuthUtil](/doc/util/AuthUtil.md "AuthUtil")

- ### Condition分页工具

> 参考 [Condition](/doc/util/Condition.md "Condition") 

- ### Cache缓存工具

> 参考 [CacheUtil](/doc/util/CacheUtil.md "CacheUtil") 


- ### 通用字段

> - `account_id`    : 账户id
> - `user_id`       : 用户档案id
> - `tenant_id`     : 租户id
> - `mch_id`        : 商户ID
> - `client_id`     : 客户端id
> - `app_id`        : 应用id
> - `org_id`        : 机构id
> - `role_id`       : 角色id
> - `post_id`       : 岗位id
> - `device_id`     : 设备ID
> - `device_sn`     : 设备SN
> - `parent_id`     : 上级id
> - `indicator_id`  : 指标id
> - `indicator_record_id`     : 检测记录id
> - `patient_id`    : 患者id
> - `surveyor_id`   : 检测员id
> - `ancestors`     : 祖级id树
> - `reflect_id`    : 关联对象
> - `openid`        : openid
> - `unionid`       : unionid

- ### 保留字段

>   - `id`                  ：主键字段
>   - `create_account       ：创建账户
>   - `create_org           ：创建机构
>   - `create_time          ：创建时间
>   - `update_account       ：更新账户
>   - `update_time          ：更新时间
>   - `status               ：业务状态
>   - `is_deleted           ：是否删除
>   - `version              ：乐观锁
>   - `tenant_id            ：租户号

- ### Entity 基类

> - `LiteEnity`:
>   - 继承关系：所有表必须遵守第四范式，拥有自己的主键
>   - 字段集合：`id`
>   - 业务场景：常用于关系表和基础配置表
>
> - `BaseEntity`:
>   - 继承关系：继承自LiteEntiy
>   - 字段集合：`id`、`createAccount`、`createOrg`、`createTime`、`updateAccount`、`updateTime`、`status`、`isDeleted`
>   - 业务场景：用于常规业务表，需要进行权限隔离和基础操作日志
>
> - `OnlyDateEntity`:继承自LiteEntity，
>   - 继承关系：继承自LiteEntiy
>   - 字段集合：`id`、`createTime`、`updateTime`
>   - 业务场景：用于关系表，并需要记录关系变更的时间
>
> - `VersionEntity`：
>   - 继承关系：继承自BaseEntity
>   - 字段集合：`id`、`createAccount`、`createOrg`、`createTime`、`updateAccount`、`updateTime`、`status`、`isDeleted`、`version`
>   - 业务场景：用于资源互抢型的业务表，避免多用户操作出现脏数据

> - `TenantEntity`：
>   - 继承关系：继承自BaseEntity
>   - 字段集合：`id`、`createAccount`、`createOrg`、`createTime`、`updateAccount`、`updateTime`、`status`、`isDeleted`、`tenantId`
>   - 业务场景：用于需要对租户进行数据隔离的业务表，各租户间相互不干扰

> - `TenantVersionEntity`：
>   - 继承关系：继承自BaseEntity
>   - 字段集合：`id`、`createAccount`、`createOrg`、`createTime`、`updateAccount`、`updateTime`、`status`、`isDeleted`、`version`、`tenantId`
>   - 业务场景：用于租户内存在资源互抢型的业务场景



# 开启Seata分布式事务

* 1、在提供方和调用方服务的`pom.xml`文件中增加分布式事务依赖

> 代码样例：

```xml
    <dependency>
        <groupId>com.sino.boot</groupId>
        <artifactId>sino-plugin-transaction</artifactId>
    </dependency>
```

* 2、在提供方和调用方服务的启动类切换注解 `@SeataCloudApplication`,服务调用方和提供方都要开启

> 代码样例：

```java
@EnableSinoFeign
//@SpringCloudApplication
@SeataCloudApplication
public class SeataOrderApplication {

	public static void main(String[] args) {
		SinoApplication.run(LauncherConstant.APPLICATION_SEATA_ORDER_NAME, SeataOrderApplication.class, args);
	}

}
```

* 3、服务提供方的服务层方法增加`@Transactional`事务注解，并指名拦截异常类型

> 代码样例：

```java
@Service
public class StorageServiceImpl extends ServiceImpl<StorageMapper, Storage> implements IStorageService {

	@Override
	@Transactional(rollbackFor = Exception.class)
	public int deduct(String commodityCode, int count) {
		Storage storage = baseMapper.selectOne(Wrappers.<Storage>query().lambda().eq(Storage::getCommodityCode, commodityCode));
		if (storage.getCount() < count) {
			throw new RuntimeException("超过库存数，扣除失败！");
		}
		storage.setCount(storage.getCount() - count);
		return baseMapper.updateById(storage);
	}

}
```

* 4、服务调用方方法增加全局`@GlobalTransactional`全局异常声明注解

> 代码样例：

```java
@Service
@AllArgsConstructor
public class OrderServiceImpl extends ServiceImpl<OrderMapper, Order> implements IOrderService {

	private IStorageClient storageClient;

	@Override
	@GlobalTransactional
	@Transactional(rollbackFor = Exception.class)
	public boolean createOrder(String userId, String commodityCode, Integer count) {
		int maxCount = 100;
		BigDecimal orderMoney = new BigDecimal(count).multiply(new BigDecimal(5));
		Order order = new Order()
			.setUserId(userId)
			.setCommodityCode(commodityCode)
			.setCount(count)
			.setMoney(orderMoney);
		int cnt1 = baseMapper.insert(order);
		int cnt2 = storageClient.deduct(commodityCode, count);
		if (cnt2 < 0) {
			throw new ServiceException("创建订单失败");
		} else if (count > maxCount) {
			throw new ServiceException("超过订单最大值，创建订单失败");
		}
		return cnt1 > 0 && cnt2 > 0;
	}

}
```

#redis分布式锁基于`redisson`的实现

+ 1、@RedisLock 注解，用于声明当前方法启用分布式锁
+ 2、参数列表：
  + `value`：锁的 key 必须：请保持唯一性
  + `param`：分布式锁参数，可选，支持 spring el # 读取方法参数和 @ 读取 spring bean
  + `waitTime`：等待锁超时时间，默认30
  + `leaseTime`：自动解锁时间，自动解锁时间一定得大于方法执行时间，否则会导致锁提前释放，默认100
  + `timeUnit`：时间单温，默认为秒
  + `type`：默认公平锁 (`LockType.REENTRANT` 重入锁) (`LockType.FAIR` 公平锁)

# 关于日志采集

+ 1、`@ApiLog`注解，用户采集指定的方法执行耗时
+ 2、系统前后台都自动采集错误日志统一推送到`Sino-Log`进行采集
+ 3、`ApiLogPublisher.publishEvent()` 手动采集API日志事件
+ 4、`UsualLogPublisher.publishEvent()` 手动采集常规日志事件
+ 5、`ErrorLogPublisher.publishEvent()` 手动采集常规日志事件

# 关于请求限流的控制

+ 1、@RateLimiter 注解，用于声明当前方法参与限流策略
+ 2、参数列表：
  + `value`：限流的 key 支持，必须：请保持唯一性
  + `param`：限流的参数，可选，支持 spring el # 读取方法参数和 @ 读取 spring bean
  + `max`：支持的最大请求
  + `ttl`：持续时间
  + `timeUnit`：时间单位

> 代码样例：

```java
@Service
@Validated
@AllArgsConstructor
public class XXXServiceImpl extends ServiceImpl<XXXMapper, XXX> implements IXXXService {
    /**
     * 限流控制样例
     */
    @RateLimiter(value = "triggerIntegralEvent", max = 2, ttl = 3L, timeUnit = TimeUnit.SECONDS, param = "#equityEvent.eventKey+':'+#equityEvent.userId")
    public R triggerIntegralEvent(@RequestBody IntegralEvent equityEvent) {
       //todo something
    }
}
```

# 关于异步响应请求开启

>对于同一客户端存在多次并非获取某个相同请求时，容易出现请求响应紊乱情况，启用异步响应请求可以解决这类问题，如字典加载、图片响应等

+ 1、在对应启动类增加@EnableAsync注解，表明当前服务开启异步响应机制
+ 2、将Controller层的方法返回改成异步回调的方式返回，如Callable<R<T>>
+ 3、方法的执行体用异步回调匿名类包装一下即可

> 开启异步请求机制示例

```java
@EnableAsync
@EnableSinoFeign
@SpringCloudApplication
public class XXXApplication {

    public static void main(String[] args) {
        SinoApplication.run(ModuleInfo.APPLICATION_NAME, XXXApplication.class, args);
    }

}
```

> 申明限流规则示例

```java
@RestController
@AllArgsConstructor
@RequestMapping("/dict")
@Api(value = "字典", tags = "字典")
public class DictController extends BaseController {
    /**
    * 详情
    */
    @GetMapping("/detail")
    @ApiOperationSupport(order = 1)
    @ApiOperation(value = "详情", notes = "传入dict")
    public Callable<R<DictVO>> detail(Dict dict) {
        return new Callable<R<DictVO>>() {
            @Override
            public R<DictVO> call() throws Exception {
                Dict detail = dictService.getOne(Condition.getQueryWrapper(dict));
                return R.data(DictWrapper.build().entityVO(detail));
            }
        };
    }

    /**
     * 获取字典树形结构
     *
     * @return
     */
    @GetMapping("/tree")
    @ApiOperationSupport(order = 3)
    @ApiOperation(value = "树形结构", notes = "树形结构")
    public Callable<R<List<DictVO>>> tree() {
        return () -> {
            List<DictVO> tree = dictService.tree();
            return R.data(tree);
        };
    }
}
```

# HttpRequest工具包

```xml
    <dependency>
        <groupId>com.sino.boot</groupId>
        <artifactId>sino-plugin-http</artifactId>
        <version>${boot.version}</version>
    </dependency>
```

# 启用加密通讯

> - 在Ctroller类或方法上增加`@ApiCrypto`即可
> - 后台和前端分别配置aes和des对应的密钥
> - 前后台默认都增加了对加密和非加密请求的兼容

# 动态权限体系

## **功能权限**

> 支持模块、菜单、按钮级别的授权，界面入口级限制

## **接口权限**

> - 支持根据角色设定接口调用权限，针对敏感类的接口，是只能有固定的一些角色才能调用，非指定角色是不能调用，动态调整角色可调用接口
> - 注解定义，`value`可用于`Spring EL`表达式，主要用于`RestController`层的`public`方法上

 ```java
/**
 * 权限注解 用于检查权限 规定访问权限
 *
 * @example @ApiAuth("#userVO.id<10")
 * @example @ApiAuth("hasRole(#test, #test1)")
 * @example @ApiAuth("hasPermission(#test) and @ApiAuth.hasPermission(#test)")
 * @author sinocare.com
 */
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface ApiAuth {

	/**
	 * 启用 Spring el
	 */
	String value();

}
 ```

> - `com.sino.boot.core.common.constant.RoleConstant` 已经定义常规的角色判断
>   - `RoleConstant.HAS_ROLE_ADMINISTRATOR`:超级管理员权限
>   - `RoleConstant.HAS_ROLE_ADMIN`:管理员权限
>   - `RoleConstant.HAS_ROLE_USER`:普通用户
>   - `RoleConstant.DENY_ALL`:只有超管才能访问
>   - `RoleConstant.PERMISSION_ALL`:对所有请求进行接口权限校验,常用于Controller类层，声明所有接口都需要权限判断
> - `com.sino.boot.core.secure.auth.AuthFun`:权限判断主类，可以进行拓展，用于特定的权限场景
>
> > 注：注解指定级别最高，直接规定了某些重要的敏感接口只能由固定的角色才能访问。但同时带来但问题是不够灵活，适用于不能被篡改，只能由管理员调用但接口配置。

## **数据权限**

> 动态的配置数据可访问的范围,动态数据权限部分只扫描了包含`Page`、`List`的`mapper`方法,如需扩大范围可以进入`nacos`配置`sino.data-scope.mapper-key`

```java
/**
 * 数据权限定义
 *
 * @author sinocare.com
 */
@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface DataAuth {

	/**
	 * 资源编号
	 */
	String code() default "";

	/**
	 * 数据权限对应字段
	 */
	String column() default DataScopeConstant.DEFAULT_COLUMN;

	/**
	 * 数据权限规则
	 */
	DataScopeEnum type() default DataScopeEnum.ALL;

	/**
	 * 可见字段
	 */
	String field() default "*";

	/**
	 * 数据权限规则值域
	 */
	String value() default "";

}

//=================================================================================

/**
 * 数据权限类型
 *
 * @author lengleng, Chill
 */
@Getter
@AllArgsConstructor
public enum DataScopeEnum {
	/**
	 * 全部数据
	 */
	ALL(1, "全部"),

	/**
	 * 本人可见
	 */
	OWN(2, "本人可见"),

	/**
	 * 所在机构可见
	 */
	OWN_ORG(3, "所在机构可见"),

	/**
	 * 所在机构及子级可见
	 */
	OWN_ORG_CHILD(4, "所在机构及子级可见"),

	/**
	 * 自定义
	 */
	CUSTOM(5, "自定义");
}
```

> - ###纯手工-纯注解配置
>
> > 如果是纯注解配置，相当于是离线配置,无需通过数据库；只需要关注column、type、value这三个字段。
> >
> > - 注解使用在Mapper类的方法上
> > - 查看本部门：`@DataAuth(type=DataScopeEnum.OWN_ORG)` 默认`column`=`create_org`
> > - 查看本人：`@DataAuth(column="create_account",type=DataScopeEnum.OWN)`
> > - 自定义范围：`@DataAuth(type=DataScopeEnum.CUSTOM,value="where scope.create_account=${accountId} or scope.create_org in (${orgId})")`
> > - 在`value`这个配置的sql里我使用里占位符`${userId}`，除此之外我们还可以用更多的参数，比如`${orgId}`、`${roleId}`、`${tenantId}`、`${account}`、`${userName}`等等,具体参考`com.sino.boot.core.secure。Principal`的可拓展字段
>
> - ###全自动-可视化动态配置
>
> > 不解释，自己看
> > ![](screenhots/Screenshot_20200612095251.png)
> > 权限类名：要做权限拦截的mapper文件中的fun全称
>
> - ###半自动-注解半自动配置
>
> > - 通过注解定义基础控制：
> > - 通过可视化配置灵活类控制
> > - 在角色授权时根据角色确定权限范围

# oauth协议：登录认证、获取凭证

- 参数设定:
  - `sino.token.state`:token是否有状态
  - `sino.token.single`:是否只可同时在线一人
  - `sino.token.sign-key`:token签名

- 密码模式：`http://host/sino-auth/oauth/token`
  - 请求头
    - `Authorization`: Basic c3dvcmQ6c3dvcmRfc2VjcmV0 （"c3dvcmQ6c3dvcmRfc2VjcmV0"为clientId:clientSecret串转换为的base64编码）
    - `Tenant-Id`:000000
  - 表单：
    - `grant_type`：password
    - `scope`：all
    - `username`：admin
    - `password`：admin

- 刷新token：`http://host/sino-auth/oauth/token`
  - 请求头：
    - `Authorization` ： Basic c3dvcmQ6c3dvcmRfc2VjcmV0 （"c3dvcmQ6c3dvcmRfc2VjcmV0"为clientId:clientSecret串转换为的base64编码）
  - 表单：
    - `grant_type`：refresh_token
    - `scope`：all
    - `refresh_token`: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0ZXN0IjoidGVzdCIsInVzZXJfbmFtZSI6ImFkbWluIiwic2NvcGUiOlsiYWxsIl0sImV4cCI6MTU1MzE2MTA5NSwiYXV0aG9yaXRpZXMiOlsiUk9MRV9VU0VSIl0sImp0aSI6IjE0YmMyYjAyLTgxY2UtNDFiNC04ZTI3LTA5YWE0ZmU4ZWMwYyIsImNsaWVudF9pZCI6ImJsYWRlIn0.jTmioQDq-fSNNn7YCwl3wP0JE-etSWtzLDe545mDbP4

- 授权码模式：`http://host/sino-auth/oauth/authorize`
  - 请求头：
    - `Authorization` ： Basic c3dvcmQ6c3dvcmRfc2VjcmV0 （"c3dvcmQ6c3dvcmRfc2VjcmV0"为clientId:clientSecret串转换为的base64编码,需要和t_sys_client表的对应字段相匹配）
  - 表单：
    - `grant_type`：authorization_code
    - `scope`：all
    - `code`：VhYNLR
    - `redirect_uri`： http://www.example.com

- 获取用户信息：`http://host/sino-auth/oauth/account-info`

# 网关动态代理

> 请参考`doc/nacos/sino-gateway-*.json` 配置示例

# 字段自动脱敏处理

> - `@SensitiveSerialize(SensitiveType.XXXXX)` 脱敏字段注解
> - `SensitiveType`:脱敏类型
>   - `CHINESE_NAME`:[中文姓名] 只显示第一个汉字，其他隐藏为2个星号<例子：李**>
>   - `ID_CARD`:[身份证号] 显示最后四位，其他隐藏。共计18位或者15位。<例子：*************5762>
>   - `FIXED_PHONE`:[固定电话] 后四位，其他隐藏<例子：****1234>
>   - `MOBILE_PHONE`:[手机号码] 前三位，后四位，其他隐藏<例子:138******1234>
>   - `ADDRESS`:[地址] 只显示到地区，不显示详细地址；我们要对个人信息增强保护<例子：北京市海淀区****>
>   - `EMAIL`:[电子邮箱] 邮箱前缀仅显示第一个字母，前缀其他隐藏，用星号代替，@及后面的地址显示<例子:g**@163.com>
>   - `BANK_CARD`:[银行卡号] 前六位，后四位，其他用星号隐藏每位1个星号<例子:6222600**********1234>
>   - `CNAPS_CODE`:[公司开户银行联号] 公司开户银行联行号,显示前两位，其他用星号隐藏，每位1个星号<例子:12********>

示例：

```java
@Data
public class UserVO {
    
    private String useId;
    
    @ApiModelProperty(value = "用户账号")
    private String account;
    
    @SensitiveSerialize(SensitiveType.CHINESE_NAME)
    @ApiModelProperty(value = "用户姓名")
    private String useName;
    
    @SensitiveSerialize(SensitiveType.MOBILE_PHONE)
    @ApiModelProperty(value = "用户手机号")
    private String mobile;
}
```

# JackJson常用注解使用

- @JsonInclude((JsonInclude.Include.XXXX)) 作用在类，用于声明本类转换json时的默认动作
  - `ALWAYS` : 包含所有属性，默认为ALWAYS
  - `NON_NULL` : 包含不为NUll的属性
  - `NON_ABSENT` : 包含NON_NULL，即为null的时候不序列化
  - `NON_EMPTY` : 包含NON_NULL，NON_ABSENT之后还包含如果字段为空也不序列化
  - `NON_DEFAULT` : 如果该字段为默认值的话就不序列化
  - `CUSTOM` : 自定义规则
  - `USE_DEFAULT` : 使用默认值的情况下就序列化
- @JsonIgnore 作用域属性或方法上，忽略指定字段
- @JsonIgnoreProperties 作用在类上，批量设置需要忽略的字段，@JsonIgnoreProperties(value = {"createTime","updateTime"})
- @JsonIgnoreType 标注在类上，当其他类有该类作为属性时，该属性将被忽略
- @JsonProperty 可以指定某个属性和json映射的名称。例如我们有个json字符串为{“userName”:”user_name”}或者直接在熟悉上设置@JsonProperty("user_name")
- @JsonPropertyOrder 指定属性在 json 字符串中的顺序
- @JsonSetter 标注于 setter 方法上，类似 @JsonProperty ，也可以解决 json 键名称和 java pojo 字段名称不匹配的问题

# 枚举定义规范-主要方便数据库中的枚举类字段在代码中增强可读性

示例：

```java
@Getter
@AllArgsConstructor
public enum PlanEnum {

	/**
	 * 代码生成
	 */
	BUILD("build", 1),

	/**
	 * 代码压缩
	 */
	ZIP("zip", 2),
	;

	final String label;

    /*枚举值声明*/
	@EnumValue
    /*jackjson序列化处理*/
	@JsonValue
	final int value;

}
```

# MYSQL-DB配置加密

YML 配置：

```yaml
// 加密配置 mpw: 开头紧接加密内容（ 非数据库配置专用 YML 中其它配置也是可以使用的 ）
spring:
  datasource:
    url: mpw:qRhvCwF4GOqjessEB3G+a5okP+uXXr96wcucn2Pev6Bf1oEMZ1gVpPPhdDmjQqoM
    password: mpw:Hzy5iliJbwDHhjLs1L0j6w==
    username: mpw:Xb+EgsyuYRXw7U7sBJjBpA==
```

密钥加密：

```java
class PWD{
    public static void main(String[] args){
          // 生成 16 位随机 AES 密钥
          String randomKey = AES.generateRandomKey();
          // 随机密钥加密
          String pwd = AES.encrypt(data, randomKey);
    }
}
```

如何使用：

```shell script
    // Jar 启动参数（ idea 设置 Program arguments , 服务器可以设置为启动环境变量 ）
    java -jar sino-auth.jar --mpw.key=d1104d7c3b616f0b
```

# 多数据源使用

1、引入dynamic-datasource-spring-boot-starter。

```xml
<dependency>
  <groupId>com.baomidou</groupId>
  <artifactId>dynamic-datasource-spring-boot-starter</artifactId>
  <version>${version}</version>
</dependency>
```

2、配置数据源。

```yaml
spring:
  datasource:
    dynamic:
      primary: master #设置默认的数据源或者数据源组,默认值即为master
      strict: false #设置严格模式,默认false不启动. 启动后在未匹配到指定数据源时候回抛出异常,不启动会使用默认数据源.
      datasource:
        master:
          url: jdbc:mysql://xx.xx.xx.xx:3306/dynamic
          username: root
          password: 123456
          driver-class-name: com.mysql.jdbc.Driver
        slave_1:
          url: jdbc:mysql://xx.xx.xx.xx:3307/dynamic
          username: root
          password: 123456
          driver-class-name: com.mysql.jdbc.Driver
        slave_2:
          url: ENC(xxxxx) # 内置加密,使用请查看详细文档
          username: ENC(xxxxx)
          password: ENC(xxxxx)
          driver-class-name: com.mysql.jdbc.Driver
          schema: db/schema.sql # 配置则生效,自动初始化表结构
          data: db/data.sql # 配置则生效,自动初始化数据
          continue-on-error: true # 默认true,初始化失败是否继续
          separator: ";" # sql默认分号分隔符
```

| 多主多从    | 纯粹多库（记得设置primary） | 混合配置    |
| ----------- | --------------------------- | ----------- |
| spring:     | spring:                     | spring:     |
| datasource: | datasource:                 | datasource: |
| dynamic:    | dynamic:                    | dynamic:    |
| datasource: | datasource:                 | datasource: |
| master_1:   | mysql:                      | master:     |
| master_2:   | oracle:                     | slave_1:    |
| slave_1:    | sqlserver:                  | slave_2:    |
| slave_2:    | postgresql:                 | oracle_1:   |
| slave_3:    | h2:                         | oracle_2:   |

3、使用 @DS 切换数据源。
`@DS` 可以注解在方法上和类上，同时存在方法注解优先于类上注解。
强烈建议只注解在service实现上。

| 注解          | 结果                                     |
| ------------- | ---------------------------------------- |
| 没有@DS       | 默认数据源                               |
| @DS("dsName") | dsName可以为组名也可以为具体某个库的名称 |

```java
    @Service
    @DS("slave")
    public class UserServiceImpl implements UserService {
    
      @Autowired
      private JdbcTemplate jdbcTemplate;
    
      public List<Map<String, Object>> selectAll() {
        return  jdbcTemplate.queryForList("select * from account");
      }
      
      @Override
      @DS("slave_1")
      public List<Map<String, Object>> selectByCondition() {
        return  jdbcTemplate.queryForList("select * from account where age >10");
      }
    }
```

# 动态表名设置

> `sino.mybatis-plus.dynamic-tables`参数可以设置需要按一定规则自动分表策略
>
> - table-name：原始表名
> - dynamic-rule：动态规则
>   - `tenantId`：按租户号进行分表
>   - `userId`：按用户进行分表
>   - `orgId`：按机构进行分表
>   - `YYYY`：按年份进行分表
>   - `YYYYMM`：按年月进行分表
>   - `YYYYMMDD`：按年月日进行分表

```yaml
sino:
    mybatis-plus:
        #动态表名规则配置,dynamic-rule:[tenantId|userId|orgId|YYYY|YYYYMM|YYYYMMDD]
        dynamic-tables:
            -   table-name: t_sys_account
                dynamic-rule: tenantId
```

# Rocket MQ 使用

> - @EnableRocket : 运用在Application启动类上，用于标注本服务启动MQ配置
> - @RocketListeners : 运用在类上，则这个类会被转换成为一个 DefaultMqPushConsumer
> - @RocketMQListener : 运用在消费端的方法上，用来处理同一topic中不同的tag类型的消息
> - 一个监听类定义一个group，确保一个topic将消息投递到，然后不同监听的tag分别消费自己想要的消息

```java
/**
* 生产并发送MQ消息到队列
*/
public class NoticeSend{
    
    public void send(){
        SendResult result = MessageEvent.data(IndicatorModuleInfo.MQTopic.INDICATOR_DETECTION_MQ, IndicatorModuleInfo.MQTag.A2, MQDelay.s0, notice).push();
    }
}

/**
* 监听并消费MQ队列
*/
@Slf4j
@RocketListeners(topic = RocketConstant.MQ_NOTICE_TOPIC, consumerGroup = "GID_NOTICE_GROUP")
public class NoticeListener {

    @Autowired
    private IMessageService messageService;

    @RocketMQListener(messageClass = NoticeEvent.class, tag = RocketConstant.MQ_NOTICE_EVENT_TAG)
    public R sendEvent(NoticeEvent noticeEvent) {
        String key = noticeEvent.getMessageTemplate().getKey();
        if (key.equals(DictNoticeEvent.FRIEND_BLOOD_GLUCOSE_NOTICE.getKey())) {
            return messageService.sendRelationshipMsg(noticeEvent);
        }
        return messageService.sendMessage(noticeEvent);
    }
}

```

#Excel 导入导出&常用操作工具

```java
//读取excel的所有sheet数据
//ExcelUtil.read(MultipartFile excel, Class<T> clazz);

//读取excel的指定sheet数据
//ExcelUtil.read(MultipartFile excel, int sheetNo, Class<T> clazz);

//读取excel的指定sheet数据
//ExcelUtil.read(MultipartFile excel, int sheetNo, int headRowNumber, Class<T> clazz);

//读取并导入数据
//ExcelUtil.save(MultipartFile excel, ExcelImporter<T> importer, Class<T> clazz);

//导出excel
//ExcelUtil.export(HttpServletResponse response, List<T> dataList, Class<T> clazz);

//导出excel
//ExcelUtil.export(HttpServletResponse response, String fileName, String sheetName, List<T> dataList, Class<T> clazz);

//获取构建类
//ExcelUtil.getReaderBuilder(MultipartFile excel, ReadListener<T> readListener, Class<T> clazz);
```

> - 定义一个按照Excel字段的类
> - 定义一个继承ExcelImporter的导入类
> - 在对应的Controller层实现导入、导出、下载模板等

```java
/**
 * 行政区划数据导入类
 *
 * @author sinocare.com
 */
@RequiredArgsConstructor
public class RegionImporter implements ExcelImporter<RegionExcel> {

	private final IRegionService service;
	private final Boolean isCovered;

	@Override
	public void save(List<RegionExcel> data) {
		service.importRegion(data, isCovered);
	}
}

/**
* Controller操作
*/
public class RegionController{
    /**
	 * 导入行政区划数据
	 */
	@PostMapping("import-region")
	@ApiOperationSupport(order = 10)
	@ApiOperation(value = "导入行政区划", notes = "传入excel")
	public R importRegion(MultipartFile file, Integer isCovered) {
		RegionImporter regionImporter = new RegionImporter(regionService, isCovered == 1);
		ExcelUtil.save(file, regionImporter, RegionExcel.class);
		return R.success("操作成功");
	}

	/**
	 * 导出行政区划数据
	 */
	@GetMapping("export-region")
	@ApiOperationSupport(order = 11)
	@ApiOperation(value = "导出行政区划", notes = "传入user")
	public void exportRegion(@ApiIgnore @RequestParam Map<String, Object> region, HttpServletResponse response) {
		QueryWrapper<Region> queryWrapper = Condition.getQueryWrapper(region, Region.class);
		List<RegionExcel> list = regionService.exportRegion(queryWrapper);
		ExcelUtil.export(response, "行政区划数据" + DateUtil.time(), "行政区划数据表", list, RegionExcel.class);
	}

	/**
	 * 导出模板
	 */
	@GetMapping("export-template")
	@ApiOperationSupport(order = 12)
	@ApiOperation(value = "导出模板")
	public void exportUser(HttpServletResponse response) {
		List<RegionExcel> list = new ArrayList<>();
		ExcelUtil.export(response, "行政区划模板", "行政区划表", list, RegionExcel.class);
	}
}
```

# ModuleInfo 定义,所有服务颗粒的主要暴露的模块信息

```java
/**
 * 演示-模块信息
 */
@Deprecated
public interface ModuleInfo extends IModuleInfo {

	//feign默认请求根路径
	String FeignPrefix = "/demo";
	//服务颗粒名称
	String ModuleName = "sino-demo";

	//==============================================
	//    错误代码
	//==============================================
	@Getter
	@AllArgsConstructor
	enum ResultCode implements IResultCode {
		OK(200),
		Fail(500);

		Integer value;
	}

	//==============================================
	//    缓存组定义
	//==============================================
	@AllArgsConstructor
	@Getter
	enum CacheGroup implements ICacheGroup {
		DEMO_GROUP("sino:group");
		String value;
	}


	//==============================================
	//    缓存定义
	//==============================================
	@AllArgsConstructor
	@Getter
	enum CacheKey implements ICacheKey {
		DEMO_CACHE("demo:cache", 0L, Timescale.SECOND);

		String key;
		Long expire;
		Timescale timescale;
	}

	//==============================================
	//    消息主题
	//==============================================
	@AllArgsConstructor
	@Getter
	enum MQTopic implements IMQTopic {
		DEMO_MQ("DEMO_TOPIC", "DEMO_GROUP");

		String topic;
		String group;
	}
}
```

# ServiceException 用于定义业务异常，用于service层主动抛出异常，并声明异常代码

```java
public class XXXXXController{
    public void exportXXXXX(HttpServletResponse response) {
        if (response == null ) {
            throw new ServiceException(AccountModuleInfo.ResultCode.Demo);
        } else {
            throw new ServiceException("自定义错误内容");
        }
    }
}
```

# 常见问题集合

> - **ServiceImpl被强制提示需要实现IService中的所有方法?**
>   答:  1、Mapper、Service、ServiceImpl中定义的Entity泛型是否一致；
>        2、LiteEntity用IService,BaseEntity用BaseService

[]: AuthUtil.md
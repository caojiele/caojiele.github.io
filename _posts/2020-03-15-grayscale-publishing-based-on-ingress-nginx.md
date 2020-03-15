---
layout:     post
title:      "基于Ingress-Nginx 实现灰度发布"
subtitle:   "Grayscale publishing based on ingress-nginx"
header-img: "img/in-post/2020.03/15/ingress-nginx.png"
date:       2020-03-15
author:     "caojiele"
tags:
    - KubeSphere
    - Ingress-Nginx
    - 灰度发布
---

  灰度发布，是指在黑与白之间，能够平滑过渡的一种发布方式。通俗来说，即让产品的迭代能够按照不同的灰度策略对新版本进行线上环境的测试，灰度发布可以保证整体系统的稳定，在初始灰度的时候就可以对新版本进行测试、发现和调整问题，以保证其影响度。

  而KubeSphere在实现灰度发布中提供两种方式，一种是在 Bookinfo 微服务的灰度发布示例中，KubeSphere 基于 Istio 对 Bookinfo 微服务示例应用实现灰度发布。另一种则是使用应用路由 (Ingress) 和项目网关 (Ingress Controller) 实现灰度发布。

  在 [Ingress-Nginx (0.21.0 版本)](https://github.com/kubernetes/ingress-nginx/releases/tag/nginx-0.21.0) 中，引入了一个新的 Canary 功能，可用于为网关入口配置多个后端服务，还可以使用指定的 annotation 来控制多个后端服务之间的流量分配。 KubeSphere 在 [2.0.2 的版本](https://kubesphere.com.cn/docs/docs/v2.0/zh-CN/release/release-v202/) 中，升级了项目网关 (Ingress Controller) 版本至 0.24.1，支持基于 [Ingress-Nginx](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#canary) 的灰度发布。


  > 说明： 本文用到的示例 yaml 源文件及代码已在KubeSphere企业空间中`demo-workspace`实现，后期版本控制发布可以在其基础上拓展实现。

  ### Ingress-Nginx Annotation 简介

  KubeSphere 基于 Nginx Ingress Controller 实现了项目的网关，作为项目对外的流量入口和项目中各个服务的反向代理。而 Ingress-Nginx 支持配置 Ingress Annotations 来实现不同场景下的灰度发布和测试，可以满足金丝雀发布、蓝绿部署与 A/B 测试等业务场景。

  > Nginx Annotations 支持以下 4 种 Canary 规则：
  >
  > * `nginx.ingress.kubernetes.io/canary-by-header`：基于 Request Header 的流量切分，适用于灰度发布以及 A/B 测试。当 Request Header 设置为 always 时，请求将会被一直发送到 Canary 版本；当 Request Header 设置为 never 时，请求不会被发送到 Canary 入口；对于任何其他 Header 值，将忽略 Header，并通过优先级将请求与其他金丝雀规则进行优先级的比较。
  > * `nginx.ingress.kubernetes.io/canary-by-header-value`：要匹配的 Request Header 的值，用于通知 Ingress 将请求路由到 Canary Ingress 中指定的服务。当 Request Header 设置为此值时，它将被路由到 Canary 入口。该规则允许用户自定义 Request Header 的值，必须与上一个 annotation (即：canary-by-header) 一起使用。
  > * `nginx.ingress.kubernetes.io/canary-weight`：基于服务权重的流量切分，适用于蓝绿部署，权重范围 0 - 100 按百分比将请求路由到 Canary Ingress 中指定的服务。权重为 0 意味着该金丝雀规则不会向 Canary 入口的服务发送任何请求，权重为 100 意味着所有请求都将被发送到 Canary 入口。
  > * `nginx.ingress.kubernetes.io/canary-by-cookie`：基于 cookie 的流量切分，适用于灰度发布与 A/B 测试。用于通知 Ingress 将请求路由到 Canary Ingress 中指定的服务的cookie。当 cookie 值设置为 always 时，它将被路由到 Canary 入口；当 cookie 值设置为 never 时，请求不会被发送到 Canary 入口；对于任何其他值，将忽略 cookie 并将请求与其他金丝雀规则进行优先级的比较。

  **注意：金丝雀规则按优先顺序进行如下排序：**

  `canary-by-header - > canary-by-cookie - > canary-weight`

  把以上的四个 annotation 规则可以总体划分为以下两类：

  * 基于权重的 Canary 规则

  ![基于权重的 Canary 规则](https://cdn.nlark.com/yuque/0/2020/png/338441/1584205753569-f5c7ae30-f2ed-4f55-bb89-400c56baee4b.png)

  * 基于用户请求的 Canary 规则

  ![基于用户请求的 Canary 规则](https://cdn.nlark.com/yuque/0/2020/png/338441/1584205759640-fe16c10c-7b9b-442d-9f8d-50a07b74a381.png)

  ### 前提条件

  * 使用 project-admin 登陆创建 ingress-demo 项目
  * 使用 admin 用户登陆，在KubeSphere 右下角的工具箱打开 web kubectl

  #### 第一步：创建项目和 Production 版本的应用

  1.1. 在 KubeSphere 中创建一个企业空间 (workspace) 和项目 (namespace) ，可参考 多租户管理快速入门。如下已创建了一个示例项目。

  ![web kubectl](https://cdn.nlark.com/yuque/0/2020/png/338441/1584261132071-97378210-cd73-4d6a-8e99-fd67bc2347ab.png)

  1.2. 本文为了快速创建应用，使用集群的 admin 账号登录，在项目中创建工作负载和服务时可通过 `编辑 yaml` 的方式，或使用 KubeSphere 右下角的工具箱打开 `web kubectl` 并使用以下命令和 yaml 文件创建一个 Production 版本的应用并暴露给集群外访问。如下创建 Production 版本的 `deployment` 和 `service`。

  ![web kubectl](https://cdn.nlark.com/yuque/0/2020/png/338441/1584261294616-1905eb51-26cc-47b2-835b-5ee0e981076a.png)


  ```shell
  $ kubectl apply -f production.yaml -n ingress-demo
  deployment.extensions/production created
  service/production created
  ````

  其中用到的 yaml 文件如下：

  **production.yaml**

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: production
    labels:
      app: production
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: production
    template:
      metadata:
        labels:
          app: production
      spec:
        containers:
        - name: production
          image: mirrorgooglecontainers/echoserver:1.10
          ports:
          - containerPort: 8080
          env:
            - name: NODE_NAME
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            - name: POD_IP
              valueFrom:
                fieldRef:
                  fieldPath: status.podIP
  
  ---
  
  apiVersion: v1
  kind: Service
  metadata:
    name: production
    labels:
      app: production
  spec:
    ports:
    - port: 80
      targetPort: 8080
      protocol: TCP
      name: http
    selector:
      app: production
  ```

  1.3. 创建 Production 版本的应用路由 (Ingress)。

  ```
  $ kubectl apply -f production.ingress -n ingress-demo
  ingress.extensions/production created
  ```

  其中用到的 yaml 文件如下：

  **production.ingress**

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: production
    annotations:
      kubernetes.io/ingress.class: nginx
  spec:
    rules:
    - host: kubesphere.io
      http:
        paths:
        - backend:
            serviceName: production
            servicePort: 80
  ```

  #### 第二步：访问 Production 版本的应用

  2.1. 此时，在 KubeSphere UI 的企业空间 demo-workspace 下，可以看到 ingress-demo 项目下的所有资源。

  **Deployment** 

  ![工作负载](https://cdn.nlark.com/yuque/0/2020/png/338441/1584261462950-1f37d9ba-5aa0-4f7b-8138-6fa54d3e1d07.png)

  **Service** 

  ![服务](https://cdn.nlark.com/yuque/0/2020/png/338441/1584261935002-b85d6221-aed8-4f68-a112-a72a128a2c4e.png)

  **Route (Ingress)**

  ![应用路由](https://cdn.nlark.com/yuque/0/2020/png/338441/1584262062301-0ef64e76-3013-47d3-a1c6-aebc62448cd3.png)

  2.2. 访问 Production 版本的应用需确保当前项目已开启了网关，在外网访问下打开网关，类型为 NodePort。

  ![外网访问](https://cdn.nlark.com/yuque/0/2020/png/338441/1584262402139-b3fab14b-e3cd-428b-a4f1-fc3476adcaa9.png)


  2.3. 如下访问 Production 版本的应用，注意以下命令需要在 SSH 客户端中执行。

  ```
  $ curl --resolve kubesphere.io:31740:192.168.100.210 kubesphere.io:31740
  # 注意，加上 --resolve 参数则无需在本地配置 /etc/hosts 中的 IP 与域名映射，否则需要预先在本地配置域名映射，其中 192.168.100.210 是项目内的网关地址。
  
  	
  Hostname: production-7946d7969c-pf8gq
  
  Pod Information:
          node name:      k8snode1
          pod name:       production-7946d7969c-pf8gq
          pod namespace:  ingress-demo
          pod IP: 10.101.249.5
  
  Server values:
          server_version=nginx: 1.13.3 - lua: 10008
  
  Request Information:
          client_address=10.101.249.7
          method=GET
          real path=/
          query=
          request_version=1.1
          request_scheme=http
          request_uri=http://kubesphere.io:8080/
  
  Request Headers:
          accept=*/*
          host=kubesphere.io:31740
          user-agent=curl/7.66.0
          x-forwarded-for=10.101.16.128
          x-forwarded-host=kubesphere.io:31740
          x-forwarded-port=80
          x-forwarded-proto=http
          x-original-uri=/
          x-real-ip=10.101.16.128
          x-request-id=2da8fdbddfa5cfeda25e1ae1c5189b35
          x-scheme=http
  
  Request Body:
          -no body in request-	
  ```

  #### 第三步：创建 Canary 版本

  参考将上述 Production 版本的 `production.yaml` 文件，再创建一个 Canary 版本的应用，包括一个 Canary 版本的 `deployment` 和 `service` (为方便快速演示，仅需将 `production.yaml` 的 deployment 和 service 中的关键字 `production` 直接替换为 `canary`，实际场景中可能涉及业务代码变更)。

  #### 第四步：Ingress-Nginx Annotation 规则

  基于权重 (Weight)

  基于权重的流量切分的典型应用场景就是`蓝绿部署`，可通过将权重设置为 0 或 100 来实现。例如，可将 Green 版本设置为主要部分，并将 Blue 版本的入口配置为 Canary。最初，将权重设置为 0，因此不会将流量代理到 Blue 版本。一旦新版本测试和验证都成功后，即可将 Blue 版本的权重设置为 100，即所有流量从 Green 版本转向 Blue。

  4.1. 使用以下 `canary.ingress` 的 yaml 文件再创建一个基于权重的 Canary 版本的应用路由 (Ingress)。

  > 注意：要开启灰度发布机制，首先需设置 `nginx.ingress.kubernetes.io/canary: "true"` 启用 Canary，以下 Ingress 示例的 Canary 版本使用了基于权重进行流量切分的 annotation 规则，将分配 30% 的流量请求发送至 Canary 版本。

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: canary
    annotations:
      kubernetes.io/ingress.class: nginx
      nginx.ingress.kubernetes.io/canary: "true"
      nginx.ingress.kubernetes.io/canary-weight: "30"
  spec:
    rules:
    - host: kubesphere.io
      http:
        paths:
        - backend:
            serviceName: canary
            servicePort: 80
  ```

  ![应用路由](https://cdn.nlark.com/yuque/0/2020/png/338441/1584262062301-0ef64e76-3013-47d3-a1c6-aebc62448cd3.png)

  4.2. 访问应用的域名（在 SSH 中执行以下命令）。

  > 说明：应用的 Canary 版本基于权重 (30%) 进行流量切分后，访问到 Canary 版本的概率接近 30%，流量比例可能会有小范围的浮动。

  ```
  $ for i in $(seq 1 10); do curl -s --resolve kubesphere.io:31740:192.168.100.210 kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![Weight](https://cdn.nlark.com/yuque/0/2020/png/338441/1584265721603-453160b1-652e-4099-beaf-a74a893e0d2d.png)

  ### 基于 Request Header

  4.3. 基于 Request Header 进行流量切分的典型应用场景即`灰度发布或 A/B 测试场景`。参考以下截图，在 KubeSphere 给 Canary 版本的应用路由 (Ingress) 新增一条 annotation `nginx.ingress.kubernetes.io/canary-by-header: canary` (这里的 annotation 的 value 可以是任意值)，使当前的 Ingress 实现基于 Request Header 进行流量切分。

  > 说明：金丝雀规则按优先顺序 `canary-by-header - > canary-by-cookie - > canary-weight` 进行如下排序，因此以下情况将忽略原有 canary-weight 的规则。

  ![Request Header](https://cdn.nlark.com/yuque/0/2020/png/338441/1584265853031-2e8a83ef-f964-483b-9bd1-844dd57afb2f.png)

  4.4. 在请求中加入不同的 Header 值，再次访问应用的域名。

  > 说明：
  > 举两个例子，如开篇提到的当 Request Header 设置为 `never` 或 `always` 时，请求将`不会`或`一直`被发送到 Canary 版本；

  > 对于任何其他 Header 值，将忽略 Header，并通过优先级将请求与其他 Canary 规则进行优先级的比较（如下第二次请求已将`基于 30% 权重`作为第一优先级）。

  ```
  $ for i in $(seq 1 10); do curl -s -H "canary: never" --resolve kubesphere.io:31740:192.168.100.210 kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![never](https://cdn.nlark.com/yuque/0/2020/png/338441/1584266669549-8da0cf3e-23d0-4558-81c8-e1ae64f34fe7.png)

  ```
  $ for i in $(seq 1 10); do curl -s -H "canary: always" --resolve kubesphere.io:31740:192.168.100.210 kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![always](https://cdn.nlark.com/yuque/0/2020/png/338441/1584266719484-b261a890-da02-4ee6-81a0-728a46612146.png)

  ```
  $ for i in $(seq 1 10); do curl -s -H "canary: other-value" --resolve kubesphere.io:31740:192.168.100.210  kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![other-value](https://cdn.nlark.com/yuque/0/2020/png/338441/1584266785569-d9f2e88e-a240-4116-848e-1a788caf22ff.png)

  4.5. 此时可以在上一个 annotation (即 canary-by-header）的基础上添加一条 `nginx.ingress.kubernetes.io/canary-by-header-value: user-value` 。用于通知 Ingress 将请求路由到 Canary Ingress 中指定的服务。

  ![canary-by-header](https://cdn.nlark.com/yuque/0/2020/png/338441/1584266895332-0514996c-d14f-4b3d-8c97-07a8c05ff6c6.png)

  4.6. 如下访问应用的域名，当 Request Header 满足此值时，所有请求被路由到 Canary 版本（该规则允许用户自定义 Request Header 的值）。

  ```
  $ for i in $(seq 1 10); do curl -s -H "canary: user-value" --resolve kubesphere.io:31740:192.168.100.210 kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![user-value](https://cdn.nlark.com/yuque/0/2020/png/338441/1584267028189-fcddd042-3756-4227-bdb3-4e1792c422bd.png)

  4.7. 如果改成`other-value`，则匹配的原则不是`user-value`值，所以会匹配到第三优先级Ingress规则（weight），即权重规则。

  ```
  $ for i in $(seq 1 10); do curl -s -H "canary: other-value" --resolve kubesphere.io:31740:192.168.100.210  kubesphere.io:31740 | grep "Hostname"; done
  ```

  ![other-value](https://cdn.nlark.com/yuque/0/2020/png/338441/1584266785569-d9f2e88e-a240-4116-848e-1a788caf22ff.png)

  ### 基于 Cookie

  4.7. 与基于 Request Header 的 annotation 用法规则类似。例如在 `A/B 测试场景` 下，需要让地域为北京的用户访问 Canary 版本。那么当 cookie 的 annotation 设置为 `nginx.ingress.kubernetes.io/canary-by-cookie: "users_from_Beijing"`，此时后台可对登录的用户请求进行检查，如果该用户访问源来自北京则设置 cookie `users_from_Beijing` 的值为 `always`，这样就可以确保北京的用户仅访问 Canary 版本。

  ### 总结

  灰度发布可以保证整体系统的稳定，在初始灰度的时候就可以对新版本进行测试、发现和调整问题，以保证其影响度。本文通过多个示例演示和说明了基于 KubeSphere 使用应用路由 (Ingress) 和项目网关 (Ingress Controller) 实现灰度发布，并详细介绍了 Ingress-Nginx 的四种 Annotation，在未使用 Istio 的情况下，也能借助 Ingress-Nginx 轻松实现灰度发布。

  ### 参考

  * [NGINX Ingress Controller - Annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#canary)
  * [canary deployment with ingress-nginx](https://www.elvinefendi.com/2018/11/25/canary-deployment-with-ingress-nginx.html)
  * [Canary Deployments on Kubernetes without Service Mesh](https://kubesphere.com.cn/docs/v2.1/zh-CN/quick-start/ingress-canary/)


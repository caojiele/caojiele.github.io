---
layout:     post
title:      "如何在私网环境实现异地SSH远程管理"
subtitle:   "The private network environment to realize long-distance SSH remote management"
date:       2018-03-30
author:     "caojiele"
header-img: "img/in-post/2018.03/30/post-ssh-remote-management.png"
tags:
    - Linux
    - SSH
    - VPN
---

> 本文来自于我的简书：[如何在私网环境实现异地SSH远程管理](https://www.jianshu.com/p/9f46ae1a1fcc)，转载请保留链接 ;)

由于不少中小型公司的宽带网络是没有固定IP的私网环境，同时还由于预算有限，因此通过传统方式很难建立VPN（`Virtual Private Network`），对于IT运维人员而言异地SSH远程管理、维护就成了相当头疼的问题。 

不过面对此类问题，终于找到了解决方案。在使用花生壳中的蒲公英异地组网后，就可以轻松实现异地SSH远程管理，而且支持纯软件组网，即使在没有预算的情况下同样可以解决难题。

### 1. Linux中安装并配置蒲公英

#### 1-1. 预先准备

服务器系统：`Centos 7.2`

所需软件：Linux版蒲公英VPN

下载地址：http://pgy.oray.com/download/

蒲公英Linux版除了拥有支持Centos、Redhat的安装包外，官网还提供了Ubuntu安装包。我们可以预先下载完成上传至服务器，也可直接进行下载。

![image](http://upload-images.jianshu.io/upload_images/6039661-1098da0577d488e0?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

首先，我先将已经将蒲公英安装包预先上传至了服务器（路径：`/home/jlcao/oray/PgyVPN_CentOS_2.0.1_x86_64.rpm`）。理论上，只要是蒲公英官方支持的Linux发行版，就不必再安装环境，一键安装即可（32位需下载32位安装包，64位需下载64位安装包）。

![image](http://upload-images.jianshu.io/upload_images/6039661-374b3705e200763f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我通过内网的一台Windows主机，使用Xshell5软件远程登录服务器，登录后使用su root命令获取了管理员权限，否则软件无法安装。

#### 1-2. 安装软件

通过cd命令进入存放蒲公英安装软件的目录，输入rpm命令进行安装；

`cd /home/jlcao/oray`

`rpm -ivh PgyVPN_CentOS_2.0.1_x86_64.rpm`

![image](http://upload-images.jianshu.io/upload_images/6039661-dbf4f59b4637f888?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

刚刚已经装过了，所以package已经存在。

#### 1-3. 设置软件

安装成功后，任意路径下输入“PgyVistor”命令即可调出交互界面，按照界面指示输入Oray账号或VPN ID进行登录，可以选择打开自动登录。如果没有账号可以在Oray官网（www.oray.com）注册即可。

![image](http://upload-images.jianshu.io/upload_images/6039661-3f399ee0c362ec22?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

账号密码登陆一次后，直接记忆保存，下次直接登陆。

登录成功后，输入对应的序号即可进入菜单，由于还未进行组网，因此获取组成员信息后，只能看到一个成员。

![image](http://upload-images.jianshu.io/upload_images/6039661-7038a0dad7ee56c9?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到了这一步，Linux服务器端的设置已经完成。只要让蒲公英在后台运行即可，输入0后返回主界面，再输入9退出界面，让其在后台继续运行。

![image](http://upload-images.jianshu.io/upload_images/6039661-e34527a91fd81e91?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2. 添加成员，实现异地组网

 打开www.oray.com，用刚才注册或是已有的Oray账号登录，进入蒲公英-智能组网一栏创建网络，并点击管理，添加成员。

![image](http://upload-images.jianshu.io/upload_images/6039661-780db91d55fddd1b?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/6039661-90294dbf2ba066b6?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

为了便于异地组网，除了将已有的客户端成员加入外，也可手动添加组网成员；

蒲公英组网成员分为客户端成员与路由器成员；

 路由器成员，则需输入蒲公英路由器的SN码进行添加；

客户端成员，则需设置添加的数量及登录的密码，确认后生成VPN ID，可用于登录蒲公英客户端，这样一来，我们就不需要将Oray账号告诉其他人。

最后，点击完成即可完成异地组网。

![image](http://upload-images.jianshu.io/upload_images/6039661-90c7e6df92b09e1d?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/6039661-699006ab6d630efc?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

值得注意的是，成员列表一栏中可以对所有的已有成员进行管理，可对客户端成员进行绑定手机、修改登录密码及重置的操作。

![image](http://upload-images.jianshu.io/upload_images/6039661-b45ae2cc4daadc35?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/6039661-51ba3875cfb4638f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3. SSH远程管理测试

#### 3-1 桌面端，以Windows为例

安装蒲公英Windows版，通过已有VPN ID或是Oray账号登录。

![image](http://upload-images.jianshu.io/upload_images/6039661-9e8234e794cbd157?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

蒲公英VPN win安装包

![image](http://upload-images.jianshu.io/upload_images/6039661-77c9a8abd1793746?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

登录后可以看到已有成员，右键可以ping主机，测试是否联通。

![image](http://upload-images.jianshu.io/upload_images/6039661-26773b0f42f53041?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在Xshell 5 中键入蒲公英软件成员列表中显示的ip进行登录，现在即使在外网环境也可一样访问到公司里的服务器，进行远程维护。

![image](http://upload-images.jianshu.io/upload_images/6039661-5020b6b5dd1a73c9?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3-2 移动端，以IOS为例

在手机中安装蒲公英软件，同样通过通过已有VPN ID或是Oray账号登录。登录后可以看到已有成员，Linux服务器已在其中。

![image](http://upload-images.jianshu.io/upload_images/6039661-1c099f7c939848ea?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/6039661-28c00d80c3e1d5a1?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用JuiceSSH等软件，键入蒲公英软件成员列表中显示的ip即可进行登录！

![image](http://upload-images.jianshu.io/upload_images/6039661-a78bcff2bd24a6df?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3-3 配合蒲公英路由器

如果在成员中添加有蒲公英路由器，凡是接入蒲公英路由器的主机可以像局域网环境一样直接SSH远程管理成员中的主机。

### 4. 总结：

以上采用蒲公英实现异地组网的方式，可以轻松解决私网环境无法通过SSH远程管理Linux服务器的问题，而且安装、配置过程相当简单，就算没有专业知识也能搞定。值得一提的是，蒲公英还拥有手机端管理App，即使出门在外也可对蒲公英VPN进行管理。

不过，上述方式也存在一定的局限性，如果纯软件组网，可能无法满足多对多的情况，同时有多台服务器、多个运维需要异地SSH远程管理就可能无法很好的满足；而且蒲公英VPN软件要一直后台运行着并且登陆正常，才能正常工作；免费版本最多只能添加5个客户端（服务器+PC端+移动端就已经占了三个），可以满足个人的工作需求，但是此版本不符合企业级别，需要账号升级。

![image](http://upload-images.jianshu.io/upload_images/6039661-90df7c3ccc9439a7?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这时就要加入蒲公英路由器，通过路由器来异地组网，满足多个运维访问多台服务器的需求。

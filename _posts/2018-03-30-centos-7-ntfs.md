---
layout:     post
title:      "Centos 7 系统如何挂载NTFS格式移动硬盘"
subtitle:   "How to quickly transfer large data"
date:       2018-03-30
author:     "caojiele"
header-img: "img/in-post/2018.03/30/post-bg-unix-linux.jpg"
tags:
    - Centos 7
    - NTFS
    - linux
---

> 本文来自于我的简书：[Centos 7 系统如何挂载NTFS格式移动硬盘](https://www.jianshu.com/p/b7d4f516c8df)，转载请保留链接 ;)

有些时候做大数据量迁移时，为了快速迁移大数据，有可能在Linux服务器上临时挂载NTFS格式的移动硬盘， 一般情况下，linux是识别不了NTFS格式移动硬盘的（需要重编译Linux核心才能，加挂NTFS分区），这时候为了能让Linux服务器能够识别NTFS的移动硬盘，就必须安装ntfs-3g（Third Generation Read/Write NTFS Driver）的包。 

### 什么是`NTFS-3G`?

`NTFS-3G`是一个开源项目，`NTFS-3G`是为Linux,Android, Mac OS X, FreeBSD, NetBSD, OpenSolaris, QNX, Haiku,和其他操作系统提供的一个稳定的，功能齐全，读写NTFS的驱动程序的。它提供了安全处理Windows XP，WindowsServer 2003，Windows 2000，Windows Vista，Windows Server 2008 和Windows 7 操作系统下的NTFS文件系统。

`NTFS-3g`是一个开源软件，它支持在Linux下面读写NTFS格式的分区。它非常的快速，同时也很安全。它支持Windows2000、XP、2003和Vista，并且支持所有的符合POSIX标准的磁盘操作。 `NTFS-3g`的目的是为了持续的发展，各硬件平台和操作系统的用户需要可靠的互通与支持ntfs的驱动，`NTFS-3g`可以提供可信任的、功能丰富的高性能解决方案。经过了12年多的发展，`NTFS-3g`已经逐渐稳定；

### 安装ntfs-3g步骤：

1. 编译安装fuse模块（支持库，若编辑环境已配置过，可跳过此步骤）

* 下载 `fuse-2.7.0.tar.gz`  拷贝到linux系统上

* `tar –zxvf fuse-2.7.0.tar.gz`

* `cd fuse-2.7.0`

* `./configure`

* `make`

* `make install`

* `lsmod`

* `modprobe fuse`

2. 安装`ntfs-3g`软件

* 下载`ntfs-3g`拷贝到linux系统上

* 下载地址：http://www.tuxera.com/community/ntfs-3g-download/ 当前最新的为：`ntfs-3g_ntfsprogs-2017.3.23`

![image](http://upload-images.jianshu.io/upload_images/6039661-ed3050fa7084e2fd?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* `tar –zxvf ntfs-3g_ntfsprogs-2017.3.23.gz`

* `cd ntfs-3g_ntfsprogs-2017.3.23`

* `./configure`

* `make`

* `make install`

3. 配置挂载`NTFS`格式的移动硬盘

3.1 首先得到`NTFS`分区的信息

* `fdisk -l`（查看linux下挂载分区情况，找到移动硬盘分区）

![image](http://upload-images.jianshu.io/upload_images/6039661-16e3707c096b7adf?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ps:如果出现乱码（中文编码问题），如何解决？

两行命令搞定：`#export LC_ALL=zh_CN.GBK`

* `export.GBK`

3.2 设置挂载点，用如下命令实现挂载

* `mount -t ntfs-3g`

例如得到的NTFS分区信息为`/dev/sdc1`，挂载点设置在`/mnt/data`下，可以用

* `mount -t ntfs-3g /dev/sdc1 /mnt/data`

或者直接用:

* `ntfs-3g ntfs-3g /dev/sdc1 /mnt/data`

PS:注意英文短横线和空格

3.3 可以查看挂载情况

* `df –lh`

![image](http://upload-images.jianshu.io/upload_images/6039661-9f50435f64190842?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

附：

1.如果想实现开机自动挂载，可以在`/etc/fstab`里面添加如下格式语句

`ntfs-3g silent,umask=0,locale=zh_CN.utf8 0 0`

如：`/dev/sda2 /mnt/data ntfs-3g silent,umask=0,locale=zh_CN.utf8 0 0`

这样可以实现NTFS分区里中文文件名的显示。

2.卸载分区可以用`umount`实现,如：

`umount /mnt/data`

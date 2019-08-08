---
layout:     post
title:      "自动化生成报告程序"
subtitle:   "Let the program help you to generate a report"
date:       2017-11-08
author:     "caojiele"
header-img: "img/in-post/2017.11/08/post-report.png"
header-mask: 0.4
tags:
  - Python
  - 前端
  - 检测报告
---

> 本文来自于我的简书：[自动化生成报告程序](https://www.jianshu.com/p/86d4ef73ca72)，转载请保留链接 ;)

各位看官初看标题可能觉得很高大上，可能联想AI这一块，其实就是一个小Demo。这个程序的产生思想可能要追溯到学生时代，在每个学期的期末是不是都要评定什么个人、班级等荣誉；每个奖状在打印的时候是不是有些基本内容是相同的，只需要把对应的个人信息和奖项名称填进去就行了；但是对于一个硬件设施不好的学校，可能会有许多老师和同学共同完成这个工作（毕竟当时年少无知嘛，老师叫你工作是一种光荣）；这无疑增加工作量，还降低了工作效率。要是有一个自动化的设备在里面输入几个指令就行了，然后设备就自动为你的需求而工作。

最近一个偶然的机会，接触到一家基因科技的公司的一个项目。他们的项目和我之前说的小事例很相似，该项目的主要实现目标是实验室检测得出的数据结果与报告模板结合批量生成报告(pdf)。我在网上搜寻了很多方法，什么模板引擎，什么实验室软件等等；都很麻烦。主要是他们公司想要看初稿，就针对他们公司的一个基因检测套餐模板做一个小demo；当然了，我每天要上班，下班以后给他们弄，不可能在这么短时间自己搞个系统出来，所以一些主流的后端语言我就没有使用（因为有些编程语言不能和报告文件后缀能够完美的匹配）。

我的思路是这样的，前期报告模板已word的形式确认后，用HTML+CSS等技术将报告模板以网页版呈现；报告生成demo在Liunx系统下，使用Python、php等技术，运用pdftk、wkhtml等格式转化软件进行格式上的处理；并采用Jinja2模板引擎和MarkupSafe模块对html自动转义和标记，同时高效的将源码转换成Pyhton字节码，加快模板执行时间；对现有表格数据批量快速导入SQL Server并结合php页面数据文件上传下载等功能对系统开发实现。最终实现了将得出的检测数据与与之对应的报告模板相结合，并生成最后的pdf格式报告。前端的报告模板代码我就不列出来了，下面附上.py代码截图，我还没传到Gitub上，有需要的可以留言，到时候我整理一下，把链接发出来，希望对大家有帮助，相互交流学习。

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1564881471786-c56a68a3-b558-49d6-b97d-22dca015adbc.png)

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1564881474503-322780a5-15d2-4d5a-b949-b5f9c363ec0f.png)

代码部署完了，怎么操作得到后面的报告呢？我在这里以win操作系统简单的写出步骤：

首先，进入报告程序路径  （程序路径，如：cd /home/jlcao/TP53/report）；

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289310105-18cb3818-dc51-4dad-93eb-48aee6c8f725.png)

然后，在当前目录创建report文件夹，该文件夹即为创建的虚拟环境                                    （virtualenv-p<文件夹名>   如：/usr/local/bin/python3.5 report）；

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289314650-7665ada7-dabf-4134-a136-6495142ed617.png)

其次，激活虚拟环境（virtualenv） （source report/bin/activate）；

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289320059-a0fc4d29-3c8f-427b-8668-bd39704e9e6e.png)

 再用pip安装依赖环境，运行requirements.txt  （pip install -r requirements.txt）；

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289328528-52c41177-3dac-4dd4-a3b4-5467d1b3e685.png)

最后，python gen_report.py --result-dir result data/xxx.csv（xxx.csv为data文件夹数据文件） 执行此命令，即可在results文件夹里生成xxx.csv中指定的患者所有报告，报告保存在独立文件夹中。

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289332975-c5ad43d0-8465-45e4-854b-e4339c7e9856.png)

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289337742-61fe2ec5-2392-481b-bda8-10a15e68cfad.png)

![image](https://cdn.nlark.com/yuque/0/2019/png/338441/1563289346397-ea3420b5-75c7-403d-aaaa-3b31c33851c6.png)

其中，创建激活虚拟环境和安装依赖环境只需要开始的一次即可，后面直接将相应的数据上传到服务器，然后按步骤操作即可。

GitHub地址：[https://github.com/caojiele/Automation-report](https://github.com/caojiele/Automation-report)  欢迎star!

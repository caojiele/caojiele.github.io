---
layout:       post
title:       "在Github Pages上部署简历"
subtitle:    'Making Github Pages on your resume'
date:        2018-12-07
author:      "Jlcao"
header-img: "img/in-post/2018.12/07/post-bg-infinity.jpg"
header-mask: 0.3
mathjax:     true
tags:
  - Github Pages
  - 简历
---

> 本文来自于我的简书：[如何在Github Pages上生成部署简历](https://www.jianshu.com/p/d95443bfdf75)，转载请保留链接 ;)

## 背景
每年的金三银四都是人员流动最大，找工作最好的时间段之一。而找工作就不得不需要更新简历，想到自己也会有这么一天，那么就来一起好好写一份简历吧。期间在网上找了不少写简历的资源，比如[轻单-在线简历制作](https://qdan.me/list/VUR-PAX01x8Skk0F)收录了一些在线生成简历的网站，有需要的童鞋可以直接拿走，不用再看这节课啦。

怎么可能！我对自己写的简历模板有信心，放这个出来就是要比比看。比比看性价比，我们这个模版的价格是 0，分母是 0 就意味着性价比无穷大！

写这个模版的初衷是希望同一份简历既能做页面展示，也能直接打印出来给我到处投。（请认真对待每一份简历，不要学习笔者）。
* [一看 star 数就知道一定是最牛的简历](https://github.com/DIYgod/Resume)
* [freepik 上的好看简历](https://www.freepik.com/free-psd/editable-cv-format-download_716578.htm)

我们可以利用 Github 的静态页面托管服务 Github Pages 来帮助我们做页面展示。
![背景图](https://cdn.nlark.com/yuque/0/2019/png/338441/1564810996049-120b22b5-c125-477a-a203-05ca5f65c983.png)

**什么是 Github Pages？**

Github Pages 是 Github 的静态页面托管服务。它设计的初衷是为了用户能够直接通过 Github 仓库来托管用户个人、组织或是项目的专属页面。参考：https://help.github.com/articles/what-is-github-pages/

可以说相当于一个可直接用 git 管理内容的静态服务器，有许多人会用它来托管自己的个人博客（利用 Jekyll、Pelican 这一类静态页面生成工具）或是在这上面发布自己的 HTML5 小游戏。当然这么好的东西也是有限制的。

**Github Pages 的限制：**

* 仓库存储的所有文件不能超过 1 GB。
* 页面的带宽限制是低于每月 100 GB 或是每月 100,000 次请求。
* 每小时最多只能部署 10 个静态网站。

对于发布自己的简历或是部署自己的博客的这一类需求我想是不用担心这些限制的，如果真的不小心超了，Github 那边不会采取什么强制措施，而是会发一份邮件提醒你应该找一个更适合你的托管对象的服务。

### 预备知识

本项目需要的预备知识：
git 的基本使用，如果对 git 完全陌生，推荐学习实验楼的[《Git 实战教程》](https://www.shiyanlou.com/courses/4)，仅需了解最基本的操作即可。

### 项目知识点

本项目完成过程中，我们将学习：在 Github Pages 上部署自己的简历。

### 适合人群

适合对于简历有要求的同学，本项目可以完美的让你对简历进行管理。

### 最终效果

简历页面展示： 

![简历页面展示](https://cdn.nlark.com/yuque/0/2019/png/338441/1564810999043-db6bc15a-3d31-448a-b2e2-b46b75b023bb.png)

保存后的 pdf 版本：

![保存后的 pdf 版本](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811002148-7b2506fd-f658-4211-8586-509ef414c466.png) 

## 步骤

本次实验我们从初始化Git库开始，编辑简历文件，将文件部署在Github Pages上，最后可以将其保存为pdf格式并打印出来。下面我们进入具体的实现阶段。

请尽量按照实验步骤自己操作，请确认文件保存在目录：`/home/shiyanlou/Code` 下。

### 初始化git库

打开终端，进入 Code 目录，创建 CV 文件夹, 并将其作为我们的工作目录。

`$ cd Code`

`$ mkdir CV && cd`

初始化 git 库。

`$ git init`

**用户配置（可选）：**

`$ git config --global user.name "你的用户名"`

`$ git config --global user.email "你的邮箱地址"`

这一步不做也没关系，用户名和邮箱是你提交commit时的签名，在 Github 的仓库页面上会显示这次提交的用户，如果不做设置就会默认为该仓库的拥有者，做了则根据邮箱来匹配用户。

### 编辑简历文件

下载页面模板文件。下载完后解压压缩包，并且直接将其中的文件置于 CV 文件夹下。
```shell
        $ wget http://labfile.oss.aliyuncs.com/courses/624/cv-template.zip

        $ unzip cv-template

        $ mv cv-template/* .

        $ rm -rf cv-template* __MACOSX*（MACOSX前面是两根下划线）
```

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811448498-36fa5902-1ab2-4d03-813b-2b2e88121080.png)

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811452055-f8972291-36a7-48e5-a041-3639fb6cf725.png)

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811454857-41a1de16-f498-457d-9903-f4bbd2c5fa49.png)

用浏览器打开就可以看见模板的样子了。同学们可以根据自己的需求来修改模板的样式。

怎么用浏览器打开？

在linux终端项目目录输入命令 `firefox index.html`；也可以进入文件夹，在图形化界面中右键选择用浏览器打开。

有的童鞋可能已经发现这份模板是可编辑的了，所有的文字栏目都是可以随意编辑的：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811461240-fbabc524-9eea-4e82-9ff5-da58464ac445.png)

点击图片可以通过图片的url地址替换：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811472935-8aca375b-ff6e-4c23-b86d-3e14c1c91995.png)

替换后：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811477372-877c1b57-01d8-496f-8af6-d45b7059338b.png)

不想留就把整个栏目删掉：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811480339-4718170e-ca92-4db7-927f-a780d8eefab0.png)

可增加新的条目：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811484560-4fb9036c-0d7e-491f-a593-3004f9e16a1e.png)

可通过点击编辑进度条：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811488385-156c1dbc-a76d-4b15-8f9e-c3fc11599668.png)

注意敏感信息不要发布在页面上，我们仅在需要打印简历时用到这些信息：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811490978-5881011d-d931-4bdb-a178-dc87513c68dd.png)

**注意简历的内容不要超出背景的高度。**

编辑完自己的简历以后，就把修改后的代码复制下来，替换掉原`index.html`里的代码。

Firefox 下，打开查看器：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811493545-abf50266-a3eb-4ed1-8072-496038153d2b.png)

复制 html 标签的外部 HTML：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811500332-6dcf9a91-d426-4e85-b0ea-ab4d60c93156.png)

然后将 index.html 中的 html 标签的所有内容（包括 html 标签）替换掉即可。

我的本意是发布后的简历页面仍是可编辑的，这方便我日后直接在上面编辑手机等个人信息后保存打印。不喜欢这样子的可以修改`static/js`下的`script.js`文件，操作非常简单，删除该文件下的所有内容，然后加上下面这一句。

```javascript 
        $(document).ready(function($){

            $("*").removeAttr('contenteditable');    
   
        })
```

这一句是为了去掉页面上所有元素的可编辑属性，最后可以在 CSS 文件内再改改样式。

### 部署简历文件

首先需要每位同学都有自己的 Github 账号：[https://github.com/](https://github.com/)

没有就快去注册一个吧。然后新建一个仓库，名字取 cv 或是 resume 皆可，之后先别跟着它给的步骤做。

Github Pages 支持托管的页面分两类，个人/组织页面 与 项目页面，其主要区别就是托管位置的区别。如下表所示（这里略去组织，它跟个人是差不多的）：

| 类型 | 页面域名 & 托管位置 | 页面源文件所在的分支 | |---|---|---|---|---| | 个人主页| username.github.io | master | | 项目主页| username.github.io/projectname | master、gh-pages 、或是在master的doc目录下|

如果想使用个人主页，那么就创建一个名为`username.github.io` （username需要替换为你的用户名）的库，在主分支master上托管你的页面代码。

如果是使用项目主页，那么可以选择将代码托管在master、gh-pages、或者`master`的`doc`目录下，其中gh-pages是默认的页面托管分支，如果想使用master，可在项目页面的设置栏中进行切换。

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564811655654-013ebda8-7ab2-4039-9c28-2fe29bf23649.png)

无论使用哪一种页面操作都是差不多的，这里就用项目页面来做演示了，由于我们所有的代码就只有页面代码而已，那么就直接在master分支上进行托管吧。

先在本地仓库做一次代码提交：

`$ git add .`

`$ git commit -m 'commit my cv'`

在项目页面找到你的仓库地址后输入：

`$ git remote add origin` 你的远程仓库地址

`$ git push -u origin master`

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824574463-5ca2b830-e390-4fc2-a662-978ad4d49692.png)

代码提交到远程仓库后，在项目页面设置 Github Pages 使用的托管源。

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824578664-a7db6d3e-dfaa-47b0-875d-b23307cd62b9.png)

现在你可以访问`https://你的用户名.github.io/resume/`这个地址了，恭喜，简历页面已成功部署在了 Github Pages 上。（参考：[https://caojiele.com/online-resume/](https://caojiele.com/online-resume/)，我这里是用的自己的域名，有域名的可以自己的，并且没有去掉页面上所有元素的可编辑属性）

### 保存简历为pdf格式

笔者考察过多个在线转换 pdf 的网站以及 js 保存 pdf 的方案，效果都不甚理想。最后发现这一步其实可以很简单，你只要打开浏览器的打印选项然后它其实是可以直接帮你保存为 pdf 的！这里还是推荐使用 Chrome ，Firefox 似乎无法删页脚与页眉。

Firefox 下：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824629382-e36d95f0-57cc-4829-891c-2088c4d08681.png)

勾上打印背景图像与颜色，页脚和页眉都设置成空白

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824629225-3b4793ee-afd8-44ed-aafd-5ba4db403b46.png)

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824629422-6baca01b-ef27-4067-aab0-dc2a0de0f189.png)
Chrome 下：

![](https://cdn.nlark.com/yuque/0/2019/png/338441/1564824629637-10a75d47-d4f2-426d-920a-b1684091a04f.png)

因为等到打印 pdf 的时候，那个页边距是可以再调的，所以笔者比较倾向于在保存的时候不保留页边距。

Mark简历生成器操作图：

![Mark简历生成器操作图](https://raw.githubusercontent.com/caojiele/resume/master/img-folder/Dynamic_figure2.gif)

网页链接：[Mark简历模板主页](https://caojiele.com/online-resume/)

项目地址：[online-resume](https://github.com/caojiele/online-resume)

## 总结
本课程主要是给没有接触过 Github Pages 的同学演示一遍它的基本使用，关于其它主题如自定义域名，自定义 404 页面等可在[Customizing GitHub Pages](https://help.github.com/categories/customizing-github-pages/)中找到参考。这里还需要再三提醒一句，千万不要在发布的简历中加上个人身份敏感信息呀！最后再给看到这里的同学一个福利吧：https://www.canva.com/templates/resumes/

## 参考资料
* [GitHub Pages Basics](https://help.github.com/categories/github-pages-basics/)
* [Customizing GitHub Pages](https://help.github.com/categories/customizing-github-pages/)
* [HTML5 Editable Table](https://codepen.io/ashblue/pen/mCtuA)
* [一看 star 数就知道一定是最牛的简历](https://github.com/DIYgod/Resume)
* [freepik 上的好看简历](https://www.freepik.com/free-psd/editable-cv-format-download_716578.htm)
* [写简历注意事项](https://note.youdao.com/share/?id=a097d9dedfc367e44e8a5840bc250a96&type=note#/)
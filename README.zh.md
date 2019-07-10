# Jlcao Blog

### [我的博客传送门 &rarr;](https://caojiele.com)

![blog-desktop](https://cdn.nlark.com/yuque/0/2019/jpeg/338441/1562635447723-4ad1235c-92d9-4552-a87a-5ef4e418b459.jpeg)

## 关于模板(beta)

我的博客仓库——`caojiele.github.io`，是经常修改的，而且还会有人乱提交代码，因此给大家做了一个稳定版的模板。大家可以直接fork模板——`Jlcaoblog-boilerplate`,要改的地方我都说明了。或者可以直接下载zip到本地自己去修改。

```
$ git clone git@github.com:caojiele/Jlcaoblog-boilerplate.git
```

**[在这里预览模板 &rarr;](https://caojiele.com/Jlcaoblog-boilerplate/)**

## 新版本特性

##### New Feature

* 当你fork了我的仓库之后，还要删掉里面关于我的文档是不是感到烦躁呢？**Boilerplate** 模板将帮助你快速开始，方便合并与更新。
* 当你非常急迫的想看一篇文章，而不知道文章具体位置在哪里的时候，请不要急，新特性里面加了全局搜索（在页面左上角），可以搜索到你想看得内容。
* 当你浏览一个页面太久，想回到顶部时，请不要移动鼠标滑轮，每个页面右下角都有返回顶部的小火箭在等着你。
* 当你看完一篇文章，想及时发表自己的观点和意见时，不要着急，每个文章底部都有评论系统，但是要用Github账号登录。
* 当然还有一些比较人性化的小插件，比如：打赏功能、站点访问量统计等等。

## 支持

* 你可以自由的fork。如果你能将主题作者和 github 的地址保留在你的页面底部，我将非常感谢你。
* 如果你喜欢我的这个博客模板，请在`caojiele.github.io`这个repository点个赞——右上角**star**一下。

## 说明文档

* 开始
	* [环境要求](#环境要求)
	* [开始](#开始)
	* [写一篇博文](#写一篇博文)
* 组件
	* [侧边栏](#侧边栏)
	* [关于我](#关于我)
	* [推荐标签](#推荐标签)
	* [好友链接](#好友链接)
	* [演示文档布局](#演示文档布局)
* 评论与分析
	* [评论](#评论)
	* [打赏](#打赏)
	* [网站分析](#网站分析) 
* 高级部分
	* [自定义](#自定义)
	* [返回顶部](#返回顶部)
	* [全局搜索](#全局搜索)
	* [标题底图](#标题底图)
	* [站点访问量统计](#站点访问量统计)
	* [搜索展示标题-头文件](#搜索展示标题-头文件)
* 其它
	* [关于收到页面构建警告](#关于收到页面构建警告)

#### 环境要求

如果你安装了jekyll，那你只需要在命令行输入`jekyll serve`就能在本地浏览器预览主题。你还可以输入`jekyll serve --watch`，这样可以边修改边自动运行修改后的文件。

经 [@BrucZhaoR](https://github.com/BruceZhaoR)的测试，好像两个命令都是可以自动运行修改后的文件的，刷新后可以实时预览。官方文件是建议安装`bundler`，这样你在本地的效果就跟在github上面是一样的。详情请见这里：https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll

#### 开始

你可以通用修改 `_config.yml`文件来轻松的开始搭建自己的博客:

```
# Site settings
title: Jlcao Blog           # 你的博客网站标题
SEOTitle: Jack Blog         # 在后面会详细谈到
description: "Cool Blog"    # 随便说点，描述一下

# SNS settings      
github_username: caojiele   # 你的github账号
weibo_username: caojiele    # 你的微博账号，底部链接会自动更新的。

# Build settings
# paginate: 10              # 一页你准备放几篇文章
```

Jekyll官方网站还有很多的参数可以调，比如设置文章的链接形式...网址在这里：[Jekyll - Official Site](http://jekyllrb.com/) 中文版的在这里：[Jekyll中文](http://jekyllcn.com/).

#### 写一篇博文

要发表的文章一般以markdown的格式放在这里`_posts/`，你只要看看这篇模板里的文章你就立刻明白该如何设置。

yaml 头文件(SEO)长这样:

```
---
layout:     post
title:      "Hello 2019"
subtitle:   "Hello World, Hello Blog"
date:       2019-01-01 00:00:00
author:     "Jlcao"
header-img: "img/post-bg-2019.jpg"
tags:
    - Life
---

```

#### 侧边栏

看右边:
![blog-sidebar](https://cdn.nlark.com/yuque/0/2019/jpeg/338441/1562635518053-b73d5f15-c726-4f91-b7ae-5de3f0150e6f.jpeg)

设置是在 `_config.yml`文件里面的`Sidebar settings`那块。
```
# Sidebar settings
sidebar: true                            #添加侧边栏
sidebar-about-description: "简单的描述一下你自己"
sidebar-avatar: /img/avatar-Jack.jpg     #你的大头贴，请使用绝对地址.
```

侧边栏是响应式布局的，当屏幕尺寸小于992px的时候，侧边栏就会移动到底部。具体请见bootstrap栅格系统 <http://v3.bootcss.com/css/>

#### 关于我

Mini-About-Me 这个模块将在你的头像下面，展示你所有的社交账号。这个也是响应式布局，当屏幕变小时候，会将其移动到页面底部，只不过会稍微有点小变化，具体请看代码。

#### 推荐标签

看到这个网站 [Medium](http://medium.com) 的推荐标签非常的炫酷，所以我将他加了进来。
这个模块现在是独立的，可以呈现在所有页面，包括主页和发表的每一篇文章标题的头上。

```
# Featured Tags
featured-tags: true  
featured-condition-size: 1     # A tag will be featured if the size of it is more than this condition value
```

唯一需要注意的是`featured-condition-size`: 如果一个标签的 SIZE，也就是使用该标签的文章数大于上面设定的条件值，这个标签就会在首页上被推荐。
 
内部有一个条件模板 `{% if tag[1].size > {{site.featured-condition-size}} %}` 是用来做筛选过滤的.

#### 好友链接

好友链接部分。这会在全部页面显示。

设置是在 `_config.yml`文件里面的`Friends`那块，自己加吧。

```
# Friends
friends: [
    {
        title: "Foo Blog",
        href: "http://foo.github.io/"
    },
    {
        title: "Bar Blog",
        href: "http://bar.github.io"
    }
]
```

#### 演示文档布局

HTML5幻灯片的排版：

![blog keynote_1](https://cdn.nlark.com/yuque/0/2019/jpeg/338441/1562643097540-c3d5e2bd-4783-4d0b-958c-e607e8a1aab8.jpeg)

这部分是用于占用html格式的幻灯片的，一般用到的是 Reveal.js, Impress.js, Slides, Prezi 等等.我认为一个现代化的博客怎么能少了放html幻灯的功能呢~

![blog keynote_2](https://cdn.nlark.com/yuque/0/2019/jpeg/338441/1562674493253-02a898fb-9a93-48d5-bd61-9833b864c07d.jpeg)

其主要原理是添加一个 `iframe`，在里面加入外部链接。你可以直接写到头文件里面去，详情请见下面的yaml头文件的写法。

```
---
layout:     keynote
iframe:     "https://caojiele.com/js-module-introduce-myself"
---
```

iframe在不同的设备中，将会自动的调整大小。保留内边距是为了让手机用户可以向下滑动，以及添加更多的内容。

#### 评论

做评论系统之前，调研了几个比较成熟的插件：
* 多说：已经关闭;
* 畅言：需要ICP备案;
* 网易云跟贴：曾被当作“多说”的替代品，可惜官方通报说在2017/08/01关闭;
* disqus：国外比较火的评论系统，但在国内墙了，故也不考虑。
* gitalk：支持 markdown,类似 issue,依托 github,不太可能被和谐;

综上所述，那么只能用gitalk了。

**首先**申请一个Github OAuth Application。
> Github头像下拉菜单 > Settings > 左边Developer settings下的OAuth Application > Register a new application，填写相关信息

**ps**:博客网站的回调地址，一定要填写博客的域名。比如我的是域名是：https://caojiele.com，其中`Homepage URL`&`Authorization callback URL`都填这个域名地址，具体可以参考这篇[文章](https://jacobpan3g.github.io/cn/2017/07/17/gitment-in-jekyll/)。

**然后**将 gitalk 配置的代码,抽离成一个文件 `comments.html`，路径: `_includes/comments`；具体内容如下：
```
<div id="gitalk-container"></div>
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
<script>
var gitalk = new Gitalk({
    id: '{{ page.date }}',
    clientID: '{{ site.gitalk.clientID }}',
    clientSecret: '{{ site.gitalk.clientSecret }}',
    repo: '{{ site.gitalk.repo }}',
    owner: '{{ site.gitalk.owner }}',
    admin: ['{{ site.gitalk.owner }}'], 
	labels: ['Gitalk'],
})
gitalk.render('gitalk-container')
</script> 
```

**接着** 需要在`_layouts`目录下的`post.html`中添加关键代码：
```
<!-- 添加评论系统 -->
<link rel="stylesheet" href="../../../../css/gitalk.css">
<script src="../../../../js/gitalk.min.js"></script>
```

两个脚本文件`gitalk.css`与`gitalk.min.js`都在我项目对应的`css`和`js`文件中，clone下来直接用即可。

然后再在`post.html`加个评论框，因为之前抽离出去一个`comments.html`，所以可以这样写：
```
<!-- gitalk评论框-->
{% if site.gitalk %}
<div class="comment">
{% include comments.html %}
</div>
{% endif %}
```

**最后**添加鉴权代码，在`_config.yml`中添加如下代码：
```
# gitalk settings
gitalk:
   enable: true
   owner: caojiele
   repo: caojiele.github.io
   clientID: ****4566f502c0a73ba
   clientSecret: ****406b08f33cc8118d02eb9332cfb707f13bf0
   admin: caojiele
```
里面的参数和第一步申请的`Github OAuth Application`有关。

#### 打赏

打赏这个功能之前尝试了几种方法，但是都没有直接扫收款码直观，同时也是代码量最少，最简单的方法。

**首先**在`_layouts`目录下的`post.html`中添加关键代码：
```
<!-- 添加打赏 -->
<link href="/css/reward.css?v=6.2.0" rel="stylesheet" type="text/css" />
```
其中`reward.css`在我项目对应的`css`文件中，clone下来直接用即可。

**最后**还是在`_layouts`目录下的`post.html`中添加如下代码：
```
     <!-- 打赏功能 -->
            <div>
                <div style="padding: 10px 0; margin: 20px auto; width: 90%; text-align: center;">
                <div>☛小礼物走一走，来Github关注我☚</div>
                <button id="rewardButton" disable="enable" onclick="var qr = document.getElementById('QR'); if (qr.style.display === 'none') {qr.style.display='block';} else {qr.style.display='none'}">
                    <span>打 赏</span>
                </button>
                <div id="QR" style="display: none;">
                     
                <div id="wechat" style="display: inline-block">
                <img id="wechat_qr" src="/img/payimg/weipayimg.jpg" alt="caojiele 微信支付"/>
                <p>微信支付</p>
                </div>
                <div id="alipay" style="display: inline-block">
                <img id="alipay_qr" src="/img/payimg/alipayimg.jpg" alt="caojiele 支付宝"/>
                <p>支付宝</p>
                </div>                        
             </div>
         </div>         
     </div>
```
**ps**：当然微信和支付宝收款码记得提前上传到项目中。

#### 网站分析

网站分析，现在支持百度统计和Google Analytics。需要去官方网站注册一下，然后将返回的code贴在下面：

```
# Baidu Analytics
ba_track_id: 4cc1f2d8f3067386cc5cdb626a202900

# Google Analytics
ga_track_id: 'UA-49627206-1'            # 你用Google账号去注册一个就会给你一个这样的id
ga_domain: caojiele.com			# 默认的是 auto, 这里我是自定义了的域名，你如果没有自己的域名，需要改成auto。
```

#### 自定义

如果你喜欢折腾，你可以去自定义我的这个模板的 code，[Grunt](gruntjs.com)已经为你准备好了。（感谢 Clean Blog）

JavaScript 的压缩混淆、Less 的编译、Apache 2.0 许可通告的添加与 watch 代码改动，这些任务都揽括其中。简单的在命令行中输入 `grunt` 就可以执行默认任务来帮你构建文件了。如果你想搞一搞 JavaScript 或 Less 的话，`grunt watch` 会帮助到你的。

**如果你可以理解 `_include/` 和 `_layouts/`文件夹下的代码（这里是整个界面布局的地方），你就可以使用 Jekyll 使用的模版引擎 [Liquid](https://github.com/Shopify/liquid/wiki)的语法直接修改/添加代码，来进行更有创意的自定义界面啦！**

#### 返回顶部

**首先**将`rocket.css`、`signature.css`和`toc.css`clone到`css`的目录下。

**然后**在 `include`目录下的`head.html`文件的头部添加下面代码：
```
    <link rel="stylesheet" href="/css/rocket.css">
    <link rel="stylesheet" href="/css/signature.css">
    <link rel="stylesheet" href="/css/toc.css">
```

**最后**将`totop.js`和`toc.js`clone到`js`的目录下，**然后**在`include`目录下的`footer.html`的最后添加下面代码：
```
<a id="rocket" href="#top" class=""></a>
<script type="text/javascript" src="/js/totop.js?v=1.0.0" async=""></script>
<script type="text/javascript" src="/js/toc.js?v=1.0.0" async=""></script>
```

#### 全局搜索

在页面左上角添加搜索功能，请先参考[soptq.me 关于全局搜索功能](https://soptq.me/2019/04/03/implement-search/)，后续我会写该功能实现的文章，请关注我的[博客](https://caojiele.com)。

#### 标题底图

标题底图是可以自己选的，看看几篇示例post你就知道如何设置了。在
  [issue #6 ](https://github.com/Huxpro/huxpro.github.io/issues/6) 中我被问到：怎么样才能让标题底图好看呢？
  
标题底图的选取完全是看个人的审美了，我也帮不了你。每一篇文章可以有不同的底图，你想放什么就放什么，最后宽度要够，大小不要太大，否则加载慢啊。

但是需要注意的是本模板的标题是**白色**的，所以背景色要设置为**灰色**或者**黑色**，总之深色系就对了。当然你还可以自定义修改字体颜色，总之，用github pages就是可以完全的个性定制自己的博客。

#### 站点访问量统计

每个页面底部都有对应的访问量统计，具体参考:[不蒜子](http://ibruce.info/2015/04/04/busuanzi/)。后续请关注我的[博客](https://caojiele.com)。

#### 搜索展示标题-头文件

我的博客标题是 **“Jlcao Blog”** 但是我想要在搜索的时候显示 **“曹杰乐的博客 | Jlcao Blog”** ，这个就需要SEO Title来定义了。

其实这个SEO Title就是定义了<head><title>标题</title></head>这个里面的东西和多说分享的标题，你可以自行修改的。

#### 关于收到页面构建警告

由于jekyll升级到3.0.x，对原来的pygments代码高亮不再支持，现只支持一种-rouge，所以你需要在 `_config.yml`文件中修改`highlighter: rouge`。另外还需要在`_config.yml`文件中加上`gems: [jekyll-paginate]`。

同时，你需要更新你的本地jekyll环境。

使用`jekyll server`的同学需要这样：

1. `gem update jekyll` # 更新jekyll
2. `gem update github-pages` #更新依赖的包

使用`bundle exec jekyll server`的同学在更新jekyll后，需要输入`bundle update`来更新依赖的包。

参考文档：[using jekyll with pages](https://help.github.com/articles/using-jekyll-with-pages/) & [Upgrading from 2.x to 3.x](http://jekyllrb.com/docs/upgrading/2-to-3/)

## 致谢

1. 这个模板是从这里[Huxpro/huxpro.github.io](https://github.com/huxpro/huxpro.github.io/)  fork 的， 感谢作者黄玄！

2. 感谢 Jekyll、Github Pages 和 Bootstrap!

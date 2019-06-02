# Jlcao Blog

### [中文文档](README.zh.md)

### [View Live Jlcao Blog &rarr;](https://caojiele.com)

![blog-desktop](https://caojiele.com/img/root/blog-desktop.jpg)

## Boilerplate (beta)

Want to clone a boilerplate instead of my buzz blog? Here comes this!

```
$ git clone git@github.com:caojiele/Jlcaoblog-boilerplate.git
```

**[View Boilerplate Here &rarr;](https://caojiele.com/Jlcaoblog-boilerplate/)**

## Version

##### New Feature

* When you fork in my project, but also delete the inside feel upset about my documents? **Boilerplate** templates will help you to quickly start, facilitate mergers and update.
* When very urgent you want to see an article, but don't know where the article location, please don't worry, new features added in global search (on the left upper corner of the page), can search to you want to see more content.
* When you visit a page for too long, want to go back to the top, please don't move the mouse wheel, every page at the bottom right corner has returned to the top of the small rockets are waiting for you.
* When you finish reading an article, want to express their own opinions and standpoints in time, don't try so hard, at the bottom of each article has a review system, but with a lot to login.
* Of course there are also some more humanized widgets, such as: reward function, site traffic statistics etc.

## Support

- **Feel free to fork. I'll Appreciate it if you keep the Author & Github link at footer**
- Give it a **Star** if you like, fork or just clone to use ;)
- If any problem or requirement, just open an issue here and I will help you.

## Document

* Get Started
	* [Environment](#environment)
	* [Get Started](#get-started)
	* [Write Posts](#write-posts)
* Components
	* [SideBar](#sidebar)
	* [Mini About Me](#mini-about-me)
	* [Featured Tags](#featured-tags)
	* [Friends](#friends)
	* [Keynote Layout](#keynote-layout)
* Comment & Analysis
	* [Comment](#comment)
	* [Reward](#reward)
	* [Analytics](#analytics) 
* Advanced
	* [Customization](#customization)
	* [Back to top](#back-to-top)
	* [Search](#search)
	* [Header Image](#header-image)
	* [Statistics](#statistics)
	* [SEO Title](#seo-title)
* Other
	* [Page Build Warning](#page-build-warning)

#### Environment

If you have jekyll installed, simply run `jekyll serve` in Command Line
and preview the themes in your browser. You can use `jekyll serve --watch` to watch for changes in the source files as well.

According to the test of [@BrucZhaoR](https://github.com/BruceZhaoR), like two commands can be run automatically modified files, can real-time preview after refresh. Official documents is suggested to install `bundler`, so you in the local effect is the same as in making the above. Please see here: https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll


#### Get Started

You can easily get started by modifying `_config.yml`:

```
# Site settings
title: Jlcao Blog           # title of your website
SEOTitle: Jack Blog         # check out docs for more detail
description: "Cool Blog"    # ...

# SNS settings      
github_username: caojiele   # modify this account to yours
weibo_username: caojiele    # the footer woule be auto-updated.

# Build settings
# paginate: 10              # nums of posts in one page
```

There are more options you can check out in the [Jekyll - Official Site](http://jekyllrb.com/), or you can directly dive into code to find more.

#### Write Posts

Feel free to checkout Markdown files in the `_posts/`, you will quickly realized how to post your articles with magical markdown plus this nice theme.

The **front-matter** of a post looks like that:

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

#### SideBar

![blog-sideba](https://caojiele.com/img/root/blog-sidebar.jpg)

Seeing more information may be necessary for you to display, from V1.1, a clean, gorgeous **SideBar** is added for you, which provide more area for displaying possible modules. You can enable *(it is default enable)* this feature by simply config:

```
# Sidebar settings
sidebar: true                            #add sidebar
sidebar-about-description: "introduce myself"
sidebar-avatar: /img/avatar-Jack.jpg     # use absolute URL.
```

We default support *[Featured Tags](#featured-tags)*, *[Mini About Me](#mini-about-me)* and *[Friends](#friends)* these three modules and you can add your own. The sidebar is naturally responsive and would be push to bottom in a small screen size (`<= 992px`, according to [Bootstarp Grid System](http://getbootstrap.com/css/#grid))  
More details of these three separate modules are talking below.

#### Mini About Me

Mini-About-Me module display all your SNS buttons also your avatar and the description if you set `sidebar-avatar` and `sidebar-about-description` which is very useful and common for a sidebar so it is default with your sidebar.

It is really nice-looking and well-designed. It would be hidden in a small screen seeing the sidebar would be push to bottom and there is already a footer including SNS feature which is similar.

#### Featured Tags

Considering the Featured-Tags feature in [Medium](http://medium.com) is pretty cool, so I add it in my blog theme also.   
This module is independent of sidebar from V1.4, so it can definitely live without enable sidebar, which would be displayed in the bottom when `sidebar` set to false, and it is not only displayed in home page but also every post page bottom.

```
# Featured Tags
featured-tags: true  
featured-condition-size: 1     # A tag will be featured if the size of it is more than this condition value
```

The only one thing need to be paid attention to is the `featured-condition-size`: A tag will be featured if the size of it is more than this condition value.  
Internally, a condition template `{% if tag[1].size > {{site.featured-condition-size}} %}` is used to do the filter.


#### Friends

Friends is a very common feature of a blog seeing the SEO, so I add it in V1.1 release to help that.   
Friends can also live without enable sidebar, also be displayed in the bottom when sidebar unable, and be displayed in every post page bottom.

You can just add your friends information in `_config.yml` with a familiar JSON syntax and everything is done, very easy:

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

#### Keynote Layout

![HTML5幻灯片的排版](https://caojiele.com/img/root/blog-keynote.jpg)

There is a increasing tendency to use Open Web technology to create keynotes, presentations, like Reveal.js, Impress.js, Slides, Prezi etc. I consider a modern blog should have abilities to post these HTML based presentation easily also abilities to play it directly.

Under the hood, a `iframe` is used to include webpage from outer source, so the only things left is to give a url in the **front-matter**:

```
---
layout:     keynote
iframe:     "https://caojiele.com/js-module-7day/"
---
```

The iframe will be automatically resized to adapt different form factors also the device orientation. A padding is left to imply user that there has more content below, also to ensure that there is a area for user to scroll down in mobile device seeing most of the keynote framework prevent the browser default scroll behavior.

#### Comment

Do before commenting system, research several mature plug-ins：
* Duoshuo：closed;
* changyan：Need **ICP** for the record;
* wangyiyuntie：Has been as a substitute for "Duoshuo", but the official reported on August 1, 2017 to close;
* disqus：Foreign comparative review system to the fire, but in the domestic wall, so it does not consider.
* gitalk：Support the markdown, similar issue, based on Github, is unlikely to be closed;

So can only use `gitalk`.

**First**,to apply for a Github OAuth Application。
> Head of Github the drop-down menu > Settings > Developer settings > OAuth Application > Register a new application,fill in the relevant information

**ps**: Blog site callback address, be sure to fill in the domain name of your blog.Such as my domain name is: https://caojiele.com, so `Homepage URL`&`Authorization callback URL` fill in this domain address，Please refer to this [article](https://jacobpan3g.github.io/cn/2017/07/17/gitment-in-jekyll/)。

**Second**, Will `gitalk` configuration code, pulling away into one file `comments.html`, url: `_includes/comments`; as follows:
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

**third**, need in `_layouts` directory `post.html` add key code:
```
<!-- Add comments system -->
<link rel="stylesheet" href="../../../../css/gitalk.css">
<script src="../../../../js/gitalk.min.js"></script>
```

Two script files `gitalk.css` and `gitalk.min.js`in my project corresponding `css` and `js` file, clone down can be used directly.

And then in `post.html` add a comment box, because before pulled out a `comments.html`, so you can write like this:
```
<!-- gitalk comment box-->
{% if site.gitalk %}
<div class="comment">
{% include comments.html %}
</div>
{% endif %}
```

**Finally**, add the authentication code, in `_config.yml` add the following code:
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
The inside of the parameters and the first step in the Application of `Github OAuth Application`.

#### Reward

Exceptional tried several methods before this functionality, but no direct payment code directly, and amount of code the least, the most simple way.

**First**, in `_layouts` directory `post.html` add key code:
```
<!-- add reward -->
<link href="/css/reward.css?v=6.2.0" rel="stylesheet" type="text/css" />
```
so `reward.css` in my project corresponding`css`file, clone down can be used directly.

**Finally**, in `_layouts` directory `post.html` add key code:
```
     <!-- reward function -->
            <div>
                <div style="padding: 10px 0; margin: 20px auto; width: 90%; text-align: center;">
                <div>☛小礼物走一走，来Github关注我☚</div>
                <button id="rewardButton" disable="enable" onclick="var qr = document.getElementById('QR'); if (qr.style.display === 'none') {qr.style.display='block';} else {qr.style.display='none'}">
                    <span>reward</span>
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
**ps**：of course remember WeChat and zhifubao payment code uploaded to the project ahead of time.

#### Analytics

We support Google Analytics and Baidu Tongji officially with a deathly simple config:

```
# Baidu Analytics
ba_track_id: 4cc1f2d8f3067386cc5cdb626a202900

# Google Analytics
ga_track_id: 'UA-49627206-1'            # 你用Google账号去注册一个就会给你一个这样的id
ga_domain: caojiele.com			# 默认的是 auto, 这里我是自定义了的域名，你如果没有自己的域名，需要改成auto。
```

Just checkout the code offered by Google/Baidu, and copy paste here, all the rest is already done for you.

(Google might ask for meta tag "google-site-verification")

#### Customization

如If you wanna do more customization and change code yourself, a [Grunt](gruntjs.com) environment is also included. (Thanks to Clean Blog.)

There are a number of tasks it performs like minification of the JavaScript, compiling of the LESS files, adding banners to keep the Apache 2.0 license intact, and watching for changes. Run the grunt default task by entering `grunt ` into your command line which will build the files. You can use `grunt watch` if you are working on the JavaScript or the LESS.

**Try to understand code in `_include/` and `_layouts/`, then you can modify Jekyll [Liquid](https://github.com/Shopify/liquid/wiki) template directly to do more creative customization.**

#### Back to top
**First**, `rocket.css`、`signature.css` and `toc.css` clone to `css` directory.

**And then**, in `include` directory `head.html` file head to add the following code:
```
    <link rel="stylesheet" href="/css/rocket.css">
    <link rel="stylesheet" href="/css/signature.css">
    <link rel="stylesheet" href="/css/toc.css">
```

**Finally**, `totop.js` and `toc.js`clone to `js` directory, **and then** in `include` directory, the end of the `footer.html` to add the following code:
```
<a id="rocket" href="#top" class=""></a>
<script type="text/javascript" src="/js/totop.js?v=1.0.0" async=""></script>
<script type="text/javascript" src="/js/toc.js?v=1.0.0" async=""></script>
```

#### Search

In the left upper corner of the page to add search functionality, please refer to: [soptq.me-implement search](https://soptq.me/2019/04/03/implement-search/).

#### Header Image

Change header images of any pages or any posts is pretty easy as mentioned above. But, thanks to [issue #6 (in Chinese)](https://github.com/Huxpro/huxpro.github.io/issues/6) asked, **how to make it looks great?**

**Well...it is actually a design issue**, not a coding stuff. It is better that you have basic design knowledge, but not is ok, let me told you how to make it well-designed:

Seeing the title text above image is **white**, the image should be **dark** to emphasize the contract. so we can easily add a **black overlay with fews of opacity**, which is depends on the brightness of the original images you used. you can process it in Photoshop, Sketch etc.

In technical views, it can be done with CSS. However, the opacity of the black overlay is really hard to assigned, **every image has different brightness so the  degree it should be adjusted is different so it is impossible to hard code it.**

#### Statistics

At the bottom of each page has a corresponding traffic statistics, refer to: [ibruce](http://ibruce.info/2015/04/04/busuanzi/).

#### SEO Title

It's possible that you want the two things different. For me, my site-title is **“Jlcao Blog”** but I want the title shows in search engine is **“曹杰乐的博客 | Jlcao Blog”** which is multi-language.

So, the SEO Title is introduced to solve this problem, you can set `SEOTitle` different from `title`, and it would be only used to generate HTML `<title>` and setting DuoShuo Sharing.

#### Page Build Warning

There are many possible reasons to cause a "Page Build Warning" email or similar error.

One of these is that github changes its build environment.

> You are attempting to use the 'pygments' highlighter, which is currently unsupported on GitHub Pages. Your site will use 'rouge' for highlighting instead. To suppress this warning, change the 'highlighter' value to 'rouge' in your '_config.yml'.

So, just edit `_config.yml`, find `highlighter: pygments`, change it to `highlighter: rouge` and the warning will be gone.

For other circumstances, check out existing issues or create a new one!

Reference:[using jekyll with pages](https://help.github.com/articles/using-jekyll-with-pages/) & [Upgrading from 2.x to 3.x](http://jekyllrb.com/docs/upgrading/2-to-3/)

## Thx

1. This template from [Huxpro/huxpro.github.io](https://github.com/huxpro/huxpro.github.io/) of the fork,thanks Huxpro！

2. Thanks Jekyll、Github Pages and Bootstrap!

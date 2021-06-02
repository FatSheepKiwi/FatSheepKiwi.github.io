# 操作手册
<!-- doctoc, installed by run: `npm i doctoc -g`, auto generate table of content by headers # to ###### -->
<!-- When content updates, rerun: doctoc {file_path} to update -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [操作手册](#操作手册)
	- [快速开始](#快速开始)
		- [环境](#环境)
		- [开始博客](#开始博客)
		- [撰写博文](#撰写博文)
	- [页面配置](#页面配置)
		- [基础配置](#基础配置)
		- [侧边栏](#侧边栏)
			- [Featured Tags](#featured-tags)
			- [Mini About Me](#mini-about-me)
			- [Friends](#friends)
		- [高级设置](#高级设置)
	- [Keynote Layout](#keynote-layout)
	- [博客开发](#博客开发)
	- [评论区](#评论区)
	- [流量分析](#流量分析)
		- [SEO Title](#seo-title)
	- [Thanks](#thanks)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 快速开始

### 环境

博客使用的[jekyll](https://jekyllrb.com/)是一个博客静态网页生成工具，依赖于[Ruby](https://www.ruby-lang.org/en/) 和[Bundler](https://bundler.io/)。 MAC OS可以follow [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)来完成基础环境的配置。
> **特别注意**，在MAC OS使用zshell的朋友在配置`$PATH`环境变量的时会没有作用，这是因为zsh使用的是`～/.zshrc`作为配置依据，而不是`～/.profile`。

### 开始博客

1. 安装`Gemfile`中的依赖文件（类比`npm install`）:

```sh
$ bundle install
```

2. 启动项目，项目默认运行在4000端口，`localhost:4000`。也可以在npm的`package.json`中配置快捷命令。

```sh
$ bundle exec jekyll serve  # alternatively, npm start
```

或者

```sh
$ npm start
```

### 撰写博文

要发表的文章一般以Markdown的格式储存在`_posts/`。
每篇文章的元信息以`YAML`格式储存于文章开头的`front-matter`，这些信息可供Jekyll正确的渲染整个博客站点。

一个文章头部YAML信息的例子：

```yml
---
layout:     post
title:      "New post title"
subtitle:   " \"Hello World, Hello Blog\""
date:       2015-01-29 12:00:00
author:     "fat sheep"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Life
    - Meta
---
```

> Tips: `tags` 也可以写为数组的形式 `tags: [Life, Meta]`.

如果每次想写新文章的时候，都需重新填写一遍元信息，这肯定太过繁琐了。这时候就使用到了[Rake](https://github.com/ruby/rake)（ Rake 的意思是 Ruby Make ，它是一个用 ruby 开发的代码构建工具）, 在设定好 Rake 脚本后，它就可以帮助我们简化创建一篇新文章的步骤:

```
rake post title="Hello 2015" subtitle="Hello World, Hello Blog"
```

这段命令行将会自动创建包含了以上元信息的文章并存放在`_posts/`目录下。

## 页面配置

博客的配置项全部储存于根目录下的`_config.yml`:

### 基础配置

```yml
# Site settings
title: Sheep Blog             # title of your website
SEOTitle: Sheep Blog          # check out docs for more detail
description: "Cool Blog"    # ...

# SNS settings      
github_username: foobar     # modify this account to yours
weibo_username: foobar     # the footer woule be auto-updated.

# Build settings
paginate: 10                # nums of posts in one page
```

Jekyll也提供了丰富的可配置项目，可以参考官方网站[Jekyll - Official Site](http://jekyllrb.com/).

### 侧边栏

![](http://huangxuan.me/img/blog-sidebar.jpg)

```yml
# Sidebar settings
sidebar: true   # default true
sidebar-about-description: "your description here"
sidebar-avatar: /img/avatar-hux.jpg     # use absolute URL.
```

> Modules *[Featured Tags](#featured-tags)*, *[Mini About Me](#mini-about-me)* and *[Friends](#friends)* are turned on by default and you can add your own.

侧边栏是响应式布局的，当屏幕尺寸小于992px的时候，侧边栏就会移动到底部。具体请见bootstrap栅格系统[Bootstarp Grid System](http://getbootstrap.com/css/#grid))

#### Featured Tags

**Featured-Tags** 现在非常的普遍，无论是推荐算法还是人工智障分类都离不开的Tag。可以呈现在所有页面，包括主页和发表的每一篇文章标题的页面底部。

```yml
# Featured Tags
featured-tags: true  
featured-condition-size: 1     # A tag will be featured if the size of it is more than this condition value
```

需要注意的一个配置项目是`featured-condition-size`，它设定了能够形成一个Tag所需要的最少文章数量。内部有一个条件模板 `{% if tag[1].size > {{site.featured-condition-size}} %}` 是用来做筛选过滤的。

#### Mini About Me

**Mini-About-Me** 通过设置`sidebar-avatar`和 `sidebar-about-description`变量来展示头像和社交媒体链接。

因为也是响应式布局的缘故，当窗口变小时候，会将其移动到页面底部

#### Friends

**Friends** 友链设置，如果和友链site有双向超链接，可以帮助搜索引擎SEO。

友链以Json形式存储在`_config.yml`文件中

```yml
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

### 高级设置

1. 设置标题格式

```yml
header-style: text 
```

2. 开启Latex支持

```yml
mathjax: true
```

3. 为封面图片增加模糊度

```yml
header-mask: 0.3
```

## Keynote Layout

![](http://huangxuan.me/img/blog-keynote.jpg)

使用html格式的幻灯片的，一般用到的是 Reveal.js, Impress.js, Slides, Prezi 等等。

使用幻灯片格式，只需要在文章头部的**front-matter**中设置layout为`keynote`:

```yml
---
layout:     keynote
iframe:     "http://huangxuan.me/js-module-7day/"
---
```

`iframe`在不同的设备中，将会自动的调整大小。保留内边距是为了让手机用户可以向下滑动，以及添加更多的内容。

## 博客开发

如果想要改变博客的主题，需要使用[Grunt](https://gruntjs.com/)它的配置位于`Gruntfile.js`文件中，提供了压缩Javascript，编译`.less`到`.css`等等功能 

Jekyll相关代码位于`_include/` and `_layouts/`.大部分来自于[Liquid](https://github.com/Shopify/liquid/wiki) 模版。

主题使用的是Jekyll默认的代码高亮，[Rouge](http://rouge.jneen.net/), 它与Pygments相匹配，可以从[jekyll-pygments-themes](http://jwarby.github.io/jekyll-pygments-themes/languages/javascript.html)选择样式来替换`highlight.less`。

## 评论区

目前没有开放的需求。

广泛使用的[Disqus](http://disqus.com)和[gitTalk](https://gitalk.github.io/)都有支持。在注册自己的账号之后，将新注册得到的用户名配置在`_config.yml`即可。

```yml
disqus_username: _your_disqus_short_name_
```

## 流量分析

目前没有开放的需求。

支持[Google Analytics]([http://disqus.com)](https://analytics.google.com/analytics/web/provision/#/provision)和[Baidu Analytics](https://tongji.baidu.com/web/welcome/login)统计。依然是在**获得自己的域名**后，注册自己的Analytics账号，会得到一个Gui Tracking Id，将其配置在`_config.yml`即可。

```yml
# Baidu Analytics
ba_track_id: 4cc1f2d8f3067386cc5cdb626a202900

# Google Analytics
ga_track_id: 'UA-49627206-1'            # Format: UA-xxxxxx-xx
ga_domain: huangxuan.me
```

### SEO Title

SEO优化是一个很玄的问题，作者大佬提供了设置SEO Title的功能，可以设置不同的`SEOTitle`和博客的`title`，这样在搜索引擎中可以更容易的搜索到博客。

## Thanks

1. [Hux Pro](https://github.com/Huxpro/huxpro.github.io)大佬发起的博客项目。
2. [qiubaiying](https://github.com/qiubaiying/qiubaiying.github.io)大佬对于项目事无巨细的讲解，大大降低了入门门槛。

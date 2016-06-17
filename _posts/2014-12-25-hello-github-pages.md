---
layout: post
category: Web
title: Hello GitHub Pages
tagline: 2014-12-25
tags: [site, ruby]
---

以下记录Windows7系统下的本地环境搭建过程

<!--more-->

### 第一步 安装ruby ###
前往[rubyinstaller](http://rubyinstaller.org/downloads/)下载ruby的1.93版本并安装，注意勾选添加到环境变量。

这里补充一下，如果安装ruby的2.00版本，在之后的步骤中会出错，后面会说明。

安装对应版本的DevKit。在cmd中切换到解压的目录中，执行下列命令。

    ruby dk.rb init
    ruby dk.rb install

修改source为'https://ruby.taobao.org'

### 第二步 安装jekyll ###
进入cmd，运行

    gem install bundler

建一个新建文件夹，作为网站目录，比如site

在site目录下建立一个名为Gemfile的文件，由于源的关系，注意第一行内容

    source 'https://ruby.taobao.org'
    gem 'github-pages'

做好了这些，继续在cmd中运行

    bundle install

默认的目录结构就建立了。

PS: 如果之前安装的是ruby的2.00版本，这里会出现"Liquid Exception: cannot load such file -- yajl/2.0/yajl in _posts/2014-05-21-welcome-to-jekyll.markdown"错误，试了网上几种方法都未解决。

### 第三步 完善网站 ###
jekyll有很多教程了，可以一步一步从零开始搭建，也可以在网上的模板进行修改。






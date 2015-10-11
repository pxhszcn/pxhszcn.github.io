---
layout: post
title: "如何使用GitHub Pages来写个人博客"
date: 2015-10-10 10:21:59
author: 彭小虎
header-img: "img/post-bg-miui6.jpg"
tags:
    - Blog
    - GtiHub Pages
---

作为利用GitHub Pages开博的第一篇文章，记录一下整个博客的搭建过程，简单来说分为以下几步：

* 创建项目仓库
* 本地环境搭建
* 本地编辑内容

## 创建项目仓库
参照[GitHub Pages官网][GitHub Pages]，创建一个项目仓库，在这里有两种选择，`User or organization site`和`Project site`。前者创建出来后通过`http://username.github.io/`来访问，而后者通过`http://username.github.com/project_name/`来访问。我们选择前者来建立个人博客，项目仓库创建完成后，利用Git终端将项目同步到本地来，基本就是这个样子：
<pre><code>Tigerkin@SZHDRND0082 MINGW64 /d/Repository/GitHub
$ git clone https://github.com/pxhszcn/pxhszcn.github.io.git
Cloning into 'pxhszcn.github.io'...
remote: Counting objects: 199, done.
remote: Compressing objects: 100% (182/182), done.
remote: Total 199 (delta 9), reused 199 (delta 9), pack-reused 0
Receiving objects: 100% (199/199), 5.76 MiB | 857.00 KiB/s, done.
Resolving deltas: 100% (9/9), done.
Checking connectivity... done.
</code></pre>

## 本地环境搭建
由于编写博客内容都在本地，在发布前一定想先在本地验证下，于是乎搭建一个本地环境变的相当重要。这里简单介绍一下在GitHub Pages上搭建个人博客的原理。众所周知，GitHub是一个十分流行且给力的免费源代码托管空间，他提供的GitHub Pages也同样是免费的服务，其特点是不限流量，可以绑定自己的域名，只能托管静态网页但支持jekyll的静态页面转换引擎。[jekyll][jekyll]是GitHub上的一个开源项目，基于Ruby开发，它实际上也可以看成是一种模板引擎liquid的扩展。它的功能有：

* 它可以将符合jekyll规范的文件转换为静态页面
* 内建专门用于博客网站的对象，可以在模板中引用这些对象：page、site等
* 对liquid进行了扩展，方便构建博客网站

为了能够支持jekyll的本地环境，我们需要先安装Ruby开发环境，首先下载Ruby和RubyDevKit的安装包：

* [rubyinstaller-2.2.3-x64.exe][rubyinstaller]
* [DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe][rubyinstaller]

分别安装在`C:\Ruby22-x64\`以及`C:\RubyDevKit\`文件夹中。接着使用`Start Command Prompt with Ruby`进入`C:\RubyDevKet\`文件夹，运行以下命令：
<pre><code>C:\RubyDevKit>dk.rb init
[INFO] found RubyInstaller v2.2.3 at C:/Ruby22-x64

Initialization complete! Please review and modify the auto-generated
'config.yml' file to ensure it contains the root directories to all
of the installed Rubies you want enhanced by the DevKit.</code></pre>
然后运行命令：
<pre><code>C:\RubyDevKit>dk.rb install
[INFO] Updating convenience notice gem override for 'C:/Ruby22-x64'
[INFO] Installing 'C:/Ruby22-x64/lib/ruby/site_ruby/devkit.rb'</code></pre>
接着进入刚才用Git同步过的目录，安装Bundle：（先更换为国内源，原因你懂的）
<pre><code>D:\Repository\GitHub\pxhszcn.github.io>gem source -a http://ruby.taobao.org/
http://ruby.taobao.org/ added to sources</code></pre>
移除官方源：
<pre><code>D:\Repository\GitHub\pxhszcn.github.io>gem source -r https://rubygems.org/
https://rubygems.org/ removed from sources</code></pre>
安装Bundle：
<pre><code>D:\Repository\GitHub\pxhszcn.github.io>gem install bundle
Fetching: bundler-1.10.6.gem (100%)
Successfully installed bundler-1.10.6
Fetching: bundle-0.0.1.gem (100%)
Successfully installed bundle-0.0.1
Parsing documentation for bundler-1.10.6
Installing ri documentation for bundler-1.10.6
Parsing documentation for bundle-0.0.1
Installing ri documentation for bundle-0.0.1
Done installing documentation for bundler, bundle after 6 seconds
2 gems installed</code></pre>
接着安装各种依赖包，在目录中创建一个`Gemfile`的文件，内容如下：
<pre><code>source 'http://ruby.taobao.org/'
gem 'github-pages'</code></pre>
保存后，运行命令：
<pre><code>D:\Repository\GitHub\pxhszcn.github.io>bundle install</code></pre>
等待安装结束后，前往[jekyll模版][jekyll模版]下载一个喜欢的模版，（本博客采用了[Hux][Hux]的模板，在这里表示感谢），完整拷入当前目录中，再次执行`bundle install`命令安装相关依赖包，然后就可以运行以下命令来启动本地转化服务了：
<pre><code>D:\Repository\GitHub\pxhszcn.github.io>bundle exec jekyll serve
Configuration file: D:/Repository/GitHub/pxhszcn.github.io/_config.yml
            Source: D:/Repository/GitHub/pxhszcn.github.io
       Destination: D:/Repository/GitHub/pxhszcn.github.io/_site
      Generating...
                    done.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'D:/Repository/GitHub/pxhszcn.github.io'
Configuration file: D:/Repository/GitHub/pxhszcn.github.io/_config.yml
    Server address: http://127.0.0.1:4000/blog//
  Server running... press ctrl-c to stop.</code></pre>
至此本地环境就搭建完成了。你可以通过访问`http://127.0.0.1:4000/blog/`在本地查看个人博客。

## 本地编辑内容
这里主要采用Sublime Text编辑器编写Markdown格式的文档。参考[这里][Markdown Preview]安装Sublime Text下的Markdown插件。

[GitHub Pages]: https://pages.github.com/
[GitHub建站攻略]: http://www.pchou.info/web-build/2013/01/03/build-github-blog-page-01.html
[jekyll]: https://github.com/mojombo/jekyll
[rubyinstaller]: http://rubyinstaller.org/downloads/
[jekyll模版]: http://jekyllthemes.org/
[Markdown Preview]: http://www.jianshu.com/p/378338f10263
[Hux]: http://huangxuan.me/

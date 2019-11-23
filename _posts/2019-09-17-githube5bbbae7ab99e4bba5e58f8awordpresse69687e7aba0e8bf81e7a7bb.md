---
id: 288
title: GitHub建站以及WordPress文章迁移
date: 2019-09-17T22:22:01+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=288
permalink: '/2019/09/github%e5%bb%ba%e7%ab%99%e4%bb%a5%e5%8f%8awordpress%e6%96%87%e7%ab%a0%e8%bf%81%e7%a7%bb.html'
categories:
  - WordPress使用技巧
  - 工具
tags:
  - exitwp
  - GitHub
  - Jekyll
  - WordPress
  - 搭建网站
---
<blockquote class="wp-block-quote">
  <p>
    本文主要介绍利用github搭建个人静态网站，以及怎样将WordPress上的文章转移到github上。
  </p>
  
  <cite>目前，GitHub Pages只支持静态博客（html，css，js），不支持服务端（php，physon），利用Jekyll生成静态网页是个人网站不错的选择。对于小型的博客之类的网站，利用GitHub建站还是很好的，而且GitHub支持HTTPS协议，也可以绑定自有域名。</cite>
</blockquote>

一时兴起想要一个备用网站，所以利用GitHub创建了一个备用网站。随着国内对GitHub的开放，GitHub的免费等优点还是很有优势的。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## GitHub搭建网站 {.h2c}

#### 关于[GitHub Pages](https://help.github.com/cn/categories/github-pages-basics)和[Jekyll](//jekyllcn.com/) {.h3c}

GitHub 页面 是一种静态站点托管服务，旨在直接从 GitHub 仓库托管您的个人、组织或项目页面。 您可以使用[Jekyll 主题选择器](https://help.github.com/cn/articles/adding-a-jekyll-theme-to-your-github-pages-site-with-the-jekyll-theme-chooser)在线创建和发布 GitHub 页面 站点。 或者，如果您宁愿在本地工作，可以使用&nbsp;[GitHub Desktop](http://desktop.github.com/)&nbsp;或[命令行](https://help.github.com/cn/articles/adding-an-existing-project-to-github-using-the-command-line)。

Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如&nbsp;[Markdown](http://daringfireball.net/projects/markdown/)）和我们的&nbsp;[Liquid](https://github.com/Shopify/liquid/wiki)&nbsp;渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在&nbsp;[GitHub Page](http://pages.github.com/)&nbsp;上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是**完全免费**的。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

#### 搭建步骤  {.h3c}

<p class="has-medium-font-size h4c">
  <strong>1. 注册GitHub账户</strong>
</p>

访问[](https://github.com)<https://github.com>创建新账号，或者登录已有账户

<p class="has-medium-font-size h4c">
  <strong>2. 创建新仓库</strong>
</p>

登录后，点击右上角的 **+** ，选择 **New repository** 。<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3-1024x292.png" alt="GitHub新建仓库 | 小tid笔记" class="wp-image-293" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3-1024x292.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3-300x86.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3-768x219.png 768w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-3.png 1206w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

项目名为**“账号名.github.io”**，如我的账号名为“Tidra&#8221;，所以我的项目名就填“tidra.github.io”，同时这个也是自己的网站名。默认为 **Public**（公开）不要改，是否创建README文件和协议根据自己需要选择。 <figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-4.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-4.png" alt="新建GitHub仓库 | 小tid笔记" class="wp-image-294" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-4.png 781w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-4-300x252.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-4-768x644.png 768w" sizes="(max-width: 781px) 100vw, 781px" /></a></figure> 

<p class="has-medium-font-size h4c">
  <strong>3. 更改设置</strong>
</p>

创建完仓库后，点击Settings进行设置。<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image.png" alt="GitHub设置 | 小tid笔记" class="wp-image-289" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image.png 1018w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-300x90.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-768x229.png 768w" sizes="(max-width: 1018px) 100vw, 1018px" /></a></figure> 

如果步骤2键的项目名不是“账号名.github.io”，可以在设置里重命名。<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1-1024x296.png" alt="github项目设置 | 小tid笔记" class="wp-image-290" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1-1024x296.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1-300x87.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1-768x222.png 768w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-1.png 1064w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

项目名符合GitHub Pages的规定后，会有下图GitHub Pages的设置选项。Custom domain可以绑定自己的域名，没有域名就直接使用项目名就可以访问自己的网页。建议把实施HTTPS勾选上。<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-5.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-5.png" alt="GitHub Pages设置 | 小tid笔记" class="wp-image-295" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-5.png 797w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-5-300x228.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-5-768x585.png 768w" sizes="(max-width: 797px) 100vw, 797px" /></a></figure> 

<p class="has-medium-font-size h4c">
  <strong>4. 选择或者上传Jekyll主题模板</strong>
</p>

设置页的**Github Pages**选项中有**Choose a theme**快捷选项，可以直接点击进去选择喜欢的主题模板，或者去 <http://jekyllthemes.org/> 选择自己喜欢的主题。去主题网站选择时，可以选择下载到本地然后再上去到自己的GitHub仓库中，也可以进入Homepage，到主题的GitHub项目中Fork该项目。

<p class="has-medium-font-size h4c">
  <strong>注意</strong>
</p>

选择Fork主题时，可以跳过上述步骤2，直接到步骤3设置更改项目名。完成上述步骤后，你就可以用**绑定的域名**或者用 **“用户名.github.io”** 在浏览器打开在GitHub上搭建的网站了。<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6-1024x358.png" alt="github建站fork项目 | 小tid笔记" class="wp-image-296" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6-1024x358.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6-300x105.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6-768x268.png 768w, https://www.tidnotes.ga/wp-content/uploads/2019/09/image-6.png 1030w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## WordPress文章迁移到GitHub {.h2c}

[Jekyll](//jekyllcn.com/)官方提供了各种博客迁移的方法，也包括了WordPress，有兴趣的可以到官网查看。目前我只是利用GitHub作为一个备用网站，不太常用到 Jekyll ，也不安装Jekyll相关组件到电脑上，所以以下提供两种不用安装Jekyll等就可以使用的办法。

#### 方法一 利用WordPress导出的xml转格式 {.h3c}

搭建好的网站，文章是存放在 **_posts** 文件夹中的，文件的格式都是md文件。所以将WordPress上的文章导出后转换为md文件放到GitHub的 **_posts** 文件夹中即可。

<p class="h4c">
  <strong>需要组件</strong>
</p>

  * python 2.x
  * html2text
  * PyYAML（[下载链接](https://tpedutw-my.sharepoint.com/:u:/g/personal/tidra_tp_edu_tw/EcPHTnMpe7JAmx5hFdJ8ICcBvpSgbnyuhk5RpwLzJj8HzA?e=ShYDOl)）
  * Beautiful soup

<p class="h4c">
  <strong>1. 导出WordPress文章</strong>
</p>

在WordPress仪表盘中，选择工具 > 导出，选择你要导出的文章。导出后会得到一个xml文件。

<p class="h4c">
  <strong>2. 下载Exitwp工具</strong>
</p>

将Exitwp（ <https://github.com/thomasf/exitwp> ）全部下载到本地，如果GitHub无法下载可以[点击下载](https://tpedutw-my.sharepoint.com/:u:/g/personal/tidra_tp_edu_tw/EVkYEMdd-JxGnBdfcxkl6UsB21EGFAgDDjumpyyhI6qB_w?e=bbtiFH)。下载后解压到任意地方。

<p class="h4c">
  <strong>3. 转换格式</strong>
</p>

将xml文件放到exitwp-master的wordpress-xml文件夹中，运行exitwp.py。无错误完成后会在根目录下多一个build文件夹，转换后的文件存放在该文件夹的最后一层的_posts文件夹里，将该文件夹的内容上传到GitHub对应的文件夹即可。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

#### 方法二 WordPress插件（推荐） {.h3c}

该方法简单，对于文章保留的完整性较好，对于小白来说十分的简便。

搜索安装 Jekyll-export 插件，无法安装可以本地下载安装（[官方下载地址](https://cn.wordpress.org/plugins/jekyll-exporter/)，[其他下载地址](https://tpedutw-my.sharepoint.com/:u:/g/personal/tidra_tp_edu_tw/EQsNgh1P0W5NsoOQgrECs94BAYlp3lK616IsMKLqpUn4lw?e=yuAFgi)）。

安装后启用，在工具栏里可以找到 Export to Jekyll 选项，点击后会自动下载一个 jekyll-export.zip 压缩包。

解压后将 _posts 文件夹内容上传到GitHub相应文件夹即可。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

#### **关于站点** {.h5c}

站点信息一般存储在 _config.yml 里； 文章一般都放在 **_posts** 文件夹里；需要评论功能，可以使用第三方社交评论插件 [Disqus](https://disqus.com/) 。
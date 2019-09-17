---
id: 204
title: WordPress之Gutenberg（古腾堡）自定义块
date: 2019-08-27T00:00:47+08:00
author: TiD
layout: revision
guid: https://www.tidnotes.ga/2019/08/163-revision-v1.html
permalink: /2019/08/163-revision-v1.html
---
<blockquote class="wp-block-quote">
  <p>
    本文内容主要参考 <a href="https://www.haibakeji.com/archives/author/1">海拔科技</a> 以及 <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a> ，介绍并解读新版WordPress所采用的 <em>Gutenberg 编辑器</em> <em>（ Block Editor/块编辑器 ）</em>如何创建自定义编辑块，包括块的样式以及扩展工具栏等。
  </p>
  
  <cite>本文适用于WordPress 5.22。关于WordPress Gutenberg自定义系列目录如下：<br /></cite>
</blockquote>

# Block介绍 {#wznav_0}

新的编辑器采用Block块的方式插入文章，把内容分成各种块，方便内容的调整和修改，同时也大大的扩展了编辑器的功能。

目前相关的中文内容还是很少，需要了解更多内容可以参考官方介绍:

  * <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/" target="_blank">Gutenberg官方网站</a>
  * <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a>
  * <a rel="noreferrer noopener" href="https://developer.wordpress.org/resource/dashicons/#businessman" target="_blank">WordPress 官方图标</a> 

## 效果截图

<ul class="wp-block-gallery columns-2 is-cropped">
  <li class="blocks-gallery-item">
    <figure><a href="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465542.gif" data-fancybox="images"><img class="wp-image-584 alignnone" src="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465542.gif" alt="" data-id="584" data-link="https://www.haibakeji.com/?attachment_id=584" /></a></figure>
  </li>
  <li class="blocks-gallery-item">
    <figure><a href="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465519.gif" data-fancybox="images"><img class="wp-image-585" src="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465519.gif" alt="" data-id="585" data-link="https://www.haibakeji.com/?attachment_id=585" /></a></figure>
  </li>
</ul>
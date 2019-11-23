---
id: 338
title: WordPress之主题制作
date: 2019-11-08T23:09:39+08:00
author: TiD
layout: post
guid: http://www.tidnotes.ga/?p=338
permalink: /2019/11/wordpress-theme-diy.html
image: /wp-content/uploads/2019/11/网页布局.gif
categories:
  - WordPress使用技巧
tags:
  - WordPress
  - 主题
  - 主题制作
  - 自定义
---
<blockquote class="wp-block-quote">
  <p>
    本文主要介绍WordPress怎样制作自己的主题，同时简单说明以下部分要用到的WordPress函数。
  </p>
  
  <cite>部分文件取自<a href="https://www.ludou.org/create-wordpress-themes-prepare.html">露兜博客</a>， <a href="https://code.tutsplus.com/articles/free-aurelius-website-template--net-11421">tutsplus</a>。本教程的主题制作主要内容根据本人制作过程和理解，尽量简化制作内容和过程，如果有什么问题可以在文末留言。</cite>
</blockquote>

最近一段时间，都在忙各种各样的事情没有时间更新博客，同时也在为本站重新设计了一套自定义的主题。这次就来讲讲制作WordPress主题制作要怎么做。

<!--more-->

## 前言

先说一下，制作WordPress主题首先得具备一点的HTML、CSS和PHP的语言基础。下文主要是我制作主题时，理解的最简单的制作WordPress主题的最简方法，如果需要详细的制作结构、步骤等可以查阅[官方文件](https://developer.wordpress.org/themes/basics/template-hierarchy/)。

文章较长，大家可以根据目录定向查看：

  1. [主题模板介绍](#introduction)
      * [网页设计基本结构](#web-design)
  2. [制作步骤](#step)
      * [index.php](#step-index)
      * [page.php 和 single.php](#step-page)
      * [archive.php](#step-archive)
      * [header.php](#step-header)
      * [sidebar.php](#step-sidebar)
      * [footer.php](#step-footer)
      * [404.php](#step-404)
      * [comments.php](#step-comments)
      * [整合文件下载](#download)
  3. [关于主题的函数](#functions)
  4. [注意](#note)

## 主题模板介绍 {#introduction}

tutsplus无偿提供的html模板[Aurelius](https://code.tutsplus.com/articles/free-aurelius-website-template--net-11421)中，包括：首页（index.html）、存档页（archive.html）、页面（page.html）、文章页（single.html）、联系页（contact.html）、无边栏页（full_width.html）、图片（/images/）、样式表（style.css）、缩略图（screenshot.png）。如果自己没有很好的主题构思的话，可以根据 [Aurelius](https://code.tutsplus.com/articles/free-aurelius-website-template--net-11421) 模板改写欸自己的模板。

在[官方的模板层次结构](https://developer.wordpress.org/themes/basics/template-hierarchy/)中也介绍了各种页面的加载顺序，大家想要了解更详细的内容可以到官方网站中查看相关内容。<figure class="wp-block-image">

<a href="https://developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png" target="_blank" rel="noreferrer noopener"><img src="https://developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png" alt="WordPress主题模板层次结构可视图 | 小TiD笔记" /></a></figure> 

考虑一般的使用情况，WordPress主题结构可以简化为下面几部分：

  1. **index.php（必需）：**可以简单的理解为负责主页和搜索页显示部分。
  2. **style.css（必需）:**主题样式。
  3. **page.php：**负责页面显示部分。
  4. **single.php：**负责文章显示部分。
  5. **archive.php：**负责标签页、作者页、目录页等的显示。
  6. **404.php：**404错误页面。
  7. **comments.php：**评论部分，如果需要评论功能。
  8. **functions.php：**自定义函数、功能等。
  9. **screenshot.png：**主题缩略图。

### 网页设计的基本结构 {#web-design}

一个页面主要分为4部分：头部、正文内容部分、侧边栏、尾部（一般叫页脚）。<figure class="wp-block-image">

<a href="//www.tidnotes.ga/wp-content/uploads/2019/11/网页布局.gif" target="_blank" rel="noreferrer noopener"><img src="//www.tidnotes.ga/wp-content/uploads/2019/11/网页布局.gif" alt="网页结构图 | 小TiD笔记" class="wp-image-341" /></a></figure> 

头部一般为固定内容，如标题、导航栏、展示区等；侧边栏一般也为固定内容，显示文章导航、目录分类等、可能会根据不同页面做不同显示，但不影响主体的结构构成，所以还是认为为固定部分；尾部同样为固定部分，一般显示站点信息、所有者信息、联系方式、站点所有权等内容；正文内容则需要根据不同的页面显示不同的内容。

所以制作一个主题，一般会将相同的内容独立到一个php文件，减少不同文件相同代码的重复使用。根据我划分的部分，可以分别写header.php、sidebar.php、footer.php三部分插入到每一个页面。

## 制作步骤 {#step}

制作步骤一般可以根据下面几部分操作：

  1. **编写静态网页：**包括HTML、CSS。CSS样式表个人觉得在编写静态的时候写好最好，这时候调试、更改都比较方便。
  2. **划分结构：**根据自己设计的主题来划分结构，一般分header.php、sidebar.php、footer.php、正文四部分。
  3. **根据静态网页改写为PHP文件：**将自己写的静态文件一部分一部分慢慢改写为php文件就行了。
  4. **打包上传主题：**将所有改写好的文件和文件夹放在一个文件夹下，**文件夹名就是你主题显示的名字**，将文件夹上传到 **wp-content/themes/** 下就可以在 **后台→外观→主题** 看到自己制作的主题了。

### index.php部分 {#step-index}

主页部分一般就是显示文章列表，所以除了引入header.php、sidebar.php、footer.php，基本就剩文章列表内容，可以用循环写列表的每一个内容。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php get_header(); ?&gt;
&lt;!-- 文章列表 --&gt;
&lt;div class="article-list"&gt;
    &lt;!-- 循环读取文章 --&gt;
    &lt;?php if (have_posts()) : while (have_posts()) : the_post(); ?&gt;
            &lt;div class="post"&gt;
                &lt;!-- 标题 --&gt;
                &lt;h3 class="title"&gt;&lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h3&gt;
                &lt;!-- 标签、日期等 --&gt;
                &lt;p class="sub"&gt;&lt;?php the_tags('标签：', ', ', ''); ?&gt; • &lt;?php the_time('Y年n月j日') ?&gt; • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?&gt;&lt;?php edit_post_link('编辑', ' • ', ''); ?&gt;&lt;/p&gt;
                &lt;!-- 图片 --&gt;
                &lt;?php $large_image_url = wp_get_attachment_image_src(get_post_thumbnail_id($post-&gt;ID), 'large');
                        if ($large_image_url[0] != "") : ?&gt;
                    &lt;img class="thumb" alt="&lt;?php the_title(); ?&gt;" src="&lt;?php echo $large_image_url[0]; ?&gt;" /&gt;
                &lt;?php endif; ?&gt;
                &lt;!-- 文章简述 --&gt;
                &lt;?php the_excerpt(); ?&gt;
            &lt;/div&gt;
        &lt;?php endwhile; ?&gt;

    &lt;?php else : ?&gt;
        &lt;h3 class="title"&gt;&lt;a href="#" rel="bookmark"&gt;未找到&lt;/a&gt;&lt;/h3&gt;
        &lt;p&gt;没有找到任何文章！&lt;/p&gt;
    &lt;?php endif; ?&gt;
&lt;/div&gt;
&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### page.php 和 single.php {#step-page}

页面和文章页差不多，主要是引入标题、正文内容和评论部分，文章页一般会在标题下加入标签、时间等信息。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;!-- 标签等 --&gt;
&lt;p class="sub"&gt;&lt;?php the_tags('标签：', ', ', ''); ?&gt; • &lt;?php the_time('Y年n月j日') ?&gt; • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?&gt;&lt;?php edit_post_link('编辑', ' • ', ''); ?&gt;&lt;/p&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php get_header(); ?&gt;
&lt;!-- 页面内容 --&gt;
&lt;?php if (have_posts()) : the_post();
    update_post_caches($posts); ?&gt;
    &lt;!-- 标题 --&gt;
    &lt;h2 class="title"&gt;&lt;?php the_title(); ?&gt;&lt;/h2&gt;
    &lt;div class="article"&gt;
        &lt;!-- 正文 --&gt;
        &lt;?php the_content(); ?&gt;
        &lt;!-- 评论 --&gt;
        &lt;?php comments_template(); ?&gt;
    &lt;/div&gt;
&lt;?php else : ?&gt;
    &lt;div class="errorbox"&gt;
        没有找到你想要的页面！
    &lt;/div&gt;
&lt;?php endif; ?&gt;
&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### archive.php {#step-archive}

标签分类页和主页显示差不多，这里只是多了一个排序选项框，和排序所需要的代码。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php get_header(); ?&gt;
&lt;!-- 页面 --&gt;
&lt;!-- 文章列表 --&gt;
&lt;div class="article-list"&gt;
    &lt;div class="sorting"&gt;
        &lt;div class="sort-by"&gt;
            &lt;h4&gt;排序&lt;/h4&gt;
            &lt;ul&gt;
                &lt;li&gt;&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'rand')) echo 'class="current"'; ?&gt; href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' =&gt; 'rand'))); ?&gt;"&gt;随机阅读&lt;/a&gt;&lt;/li&gt;
                &lt;li&gt;&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'commented')) echo 'class="current"'; ?&gt; href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' =&gt; 'commented'))); ?&gt;"&gt;评论最多&lt;/a&gt;&lt;/li&gt;
                &lt;li&gt;&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'alpha')) echo 'class="current"'; ?&gt; href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' =&gt; 'alpha'))); ?&gt;"&gt;标题排序&lt;/a&gt;&lt;/li&gt;
            &lt;/ul&gt;
        &lt;/div&gt;
        &lt;h4&gt;浏览&lt;?php
                // If this is a category archive
                if (is_category()) {
                    printf('分类&lt;/h4&gt;
			&lt;h2&gt;' . single_cat_title('', false) . '&lt;/h2&gt;');
                    if (category_description()) echo '&lt;p&gt;' . category_description() . '&lt;/p&gt;';
                    // If this is a tag archive
                } elseif (is_tag()) {
                    printf('标签&lt;/h4&gt;
			&lt;h2&gt;' . single_tag_title('', false) . '&lt;/h2&gt;');
                    if (tag_description()) echo '&lt;p&gt;' . tag_description() . '&lt;/p&gt;';
                    // If this is a daily archive
                } elseif (is_day()) {
                    printf('日期存档&lt;/h4&gt;
			&lt;h2&gt;' . get_the_time('Y年n月j日') . '&lt;/h2&gt;');
                    // If this is a monthly archive
                } elseif (is_month()) {
                    printf('月份存档&lt;/h4&gt;
				&lt;h2&gt;' . get_the_time('Y年n月') . '&lt;/h2&gt;');
                    // If this is a yearly archive
                } elseif (is_year()) {
                    printf('年份存档&lt;/h4&gt;
				&lt;h2&gt;' . get_the_time('Y年') . '&lt;/h2&gt;');
                    // If this is an author archive
                } elseif (is_author()) {
                    echo '&lt;/h4&gt;&lt;h2&gt;作者存档&lt;/h2&gt;';
                    // If this is a paged archive
                } elseif (isset($_GET['paged']) && !empty($_GET['paged'])) {
                    echo '&lt;/h4&gt;&lt;h2&gt;博客存档&lt;/h2&gt;';
                }
                ?&gt;
    &lt;/div&gt;
    &lt;?php
    global $wp_query;

    if (isset($_GET['order']) && ($_GET['order'] == 'rand')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' =&gt; 'rand',
            'paged' =&gt; $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query-&gt;query
        );
        query_posts($arms);
    } else if (isset($_GET['order']) && ($_GET['order'] == 'commented')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' =&gt; 'comment_count',
            'order' =&gt; 'DESC',
            'paged' =&gt; $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query-&gt;query
        );
        query_posts($arms);
    } else if (isset($_GET['order']) && ($_GET['order'] == 'alpha')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' =&gt; 'title',
            'order' =&gt; 'ASC',
            'paged' =&gt; $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query-&gt;query
        );
        query_posts($arms);
    }
    // 循环读取文章
    if (have_posts()) : while (have_posts()) : the_post(); ?&gt;
            &lt;div class="post"&gt;
                &lt;!-- 标题 --&gt;
                &lt;h3 class="title"&gt;&lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h3&gt;
                &lt;!-- 标签、日期等 --&gt;
                &lt;p class="sub"&gt;&lt;?php the_tags('标签：', ', ', ''); ?&gt; • &lt;?php the_time('Y年n月j日') ?&gt; • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?&gt;&lt;?php edit_post_link('编辑', ' • ', ''); ?&gt;&lt;/p&gt;
                &lt;!-- 图片 --&gt;
                &lt;?php $large_image_url = wp_get_attachment_image_src(get_post_thumbnail_id($post-&gt;ID), 'large');
                        if ($large_image_url[0] != "") : ?&gt;
                    &lt;img class="thumb" alt="&lt;?php the_title(); ?&gt;" src="&lt;?php echo $large_image_url[0]; ?&gt;" /&gt;
                &lt;?php endif; ?&gt;
                &lt;!-- 文章简述 --&gt;
                &lt;?php the_excerpt(); ?&gt;
            &lt;/div&gt;
        &lt;?php endwhile; ?&gt;

    &lt;?php else : ?&gt;
        &lt;h3 class="title"&gt;&lt;a href="#" rel="bookmark"&gt;未找到&lt;/a&gt;&lt;/h3&gt;
        &lt;p&gt;没有找到任何文章！&lt;/p&gt;
    &lt;?php endif; ?&gt;
&lt;/div&gt;
&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### header.php {#step-header}

头部内容基本是每一页的都要的<code class="language-markup">&lt;head&gt;</code>标签内容。这里主要是给出了自定义的标题和关键词、描述内容。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;!DOCTYPE html&gt;
&lt;html&gt;

&lt;head&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
    &lt;title&gt;&lt;?php if (is_home()) {
                bloginfo('name');
                echo " | ";
                bloginfo('description');
            } elseif (is_category()) {
                single_cat_title();
                echo " | ";
                bloginfo('name');
            } elseif (is_single() || is_page()) {
                single_post_title();
                echo " | ";
                bloginfo('name');
            } elseif (is_search()) {
                echo "搜索结果";
                echo " | ";
                bloginfo('name');
            } elseif (is_404()) {
                echo '页面未找到!';
            } else {
                wp_title('', true);
            } ?&gt;&lt;/title&gt;
    &lt;!-- 关键词、描述 --&gt;
    &lt;?php
    if (is_home() || is_page()) {
        $description = '小tid笔记，记录各种技术性文章，为大家提供简单、有效的、易上手的各种技术和便捷功能，有问题随时欢迎留言提问';
        $keywords = 'TiD,小tid,小tid笔记,tidnotes,技术,wordpress,前端,js';
    } elseif (is_single()) {
        if ($post-&gt;post_excerpt) { //如果文章摘要存在就以文章摘要为描述
            $description = $post-&gt;post_excerpt;
            $description = str_replace("\r\n", "", $description);
            $description = str_replace("\n", "", $description);
            $description = str_replace("\"", "'", $description);
            $description .= '...';
        } else { //如果文章摘要不存在就截断文章前200字为描述
            $description = mb_strimwidth(strip_tags($post-&gt;post_content), 0, 200, "");
            $description = str_replace("\r\n", "", $description);
            $description = str_replace("\n", "", $description);
            $description = str_replace("\"", "'", $description);
            $description .= '...';
        }
        $keywords = "";
        $tags = wp_get_post_tags($post-&gt;ID);
        foreach ($tags as $tag) {
            $keywords = $keywords . $tag-&gt;name . ",";
        }
    } elseif (is_category()) {
        $description = category_description() ? category_description() : single_cat_title('', false);
        $keywords = single_cat_title('', false);
    } elseif (is_tag()) {
        $keywords = single_tag_title('', false);
        $description = "关于标签 " . $keywords . " 的相关文章";
    }
    $description = trim(strip_tags($description));
    $keywords = trim(strip_tags($keywords));
    ?&gt;
    &lt;meta name="description" content="&lt;?php echo $description; ?&gt;" /&gt;
    &lt;meta name="keywords" content="&lt;?php echo $keywords; ?&gt;" /&gt;
    &lt;link rel="alternate" type="application/rss+xml" title="RSS 2.0 - 所有文章" href="&lt;?php bloginfo('rss2_url'); ?&gt;" /&gt;
    &lt;link rel="pingback" href="&lt;?php bloginfo('pingback_url'); ?&gt;" /&gt;
    &lt;!-- 样式表 --&gt;
    &lt;link rel="stylesheet" href="&lt;?php bloginfo('stylesheet_url'); ?&gt;" type="text/css" media="screen" /&gt;
&lt;/head&gt;

&lt;body&gt;
    &lt;header class="banner banner-pattern-seaOfClouds"&gt;
        &lt;h2&gt;&lt;?php bloginfo('name'); ?&gt;&lt;/h2&gt;
        &lt;h3&gt;&lt;?php bloginfo('description'); ?&gt;&lt;/h3&gt;
    &lt;/header&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### sidebar.php {#step-sidebar}

这部分可以根据自己的需要改写侧边栏内容，自己的部分只需要写在 <code class="language-markup">&lt;div&nbsp;class="sidebar"&gt;&lt;/div&gt;</code> 内就行。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;!-- 侧边栏 --&gt;
&lt;div class="sidebar"&gt;
    &lt;?php if (!function_exists('dynamic_sidebar') || !dynamic_sidebar('First_sidebar')) : ?&gt;
        &lt;h4&gt;分类目录&lt;/h4&gt;
        &lt;ul&gt;
            &lt;?php wp_list_categories('depth=1&title_li=&orderby=id&show_count=0&hide_empty=1&child_of=0'); ?&gt;
        &lt;/ul&gt;
        &lt;h4&gt;最近文章&lt;/h4&gt;
        &lt;ul&gt;
            &lt;?php
                $posts = get_posts('numberposts=6&orderby=post_date');
                foreach ($posts as $post) {
                    setup_postdata($post);
                    echo '&lt;li&gt;&lt;a href="' . get_permalink() . '"&gt;' . get_the_title() . '&lt;/a&gt;&lt;/li&gt;';
                }
                $post = $posts[0];
                ?&gt;
        &lt;/ul&gt;
    &lt;?php endif; ?&gt;

    &lt;?php if (!function_exists('dynamic_sidebar') || !dynamic_sidebar('Second_sidebar')) : ?&gt;
        &lt;h4&gt;标签云&lt;/h4&gt;
        &lt;div class="tag-cloud"&gt;
            &lt;?php
                $tags = get_tags();
                foreach ($tags as $tag) {
                    $tag_link = get_tag_link($tag-&gt;term_id);
                    echo "&lt;a href='{$tag_link}' title='查看关于“{$tag-&gt;name}”的文章' rel='{$tag-&gt;name} Tag'&gt;{$tag-&gt;name}&lt;/a&gt;";
                } ?&gt;
        &lt;/div&gt;
    &lt;?php endif; ?&gt;
&lt;/div&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### footer.php {#step-footer}

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;!-- 底部 --&gt;
&lt;div class="footer"&gt;
    &lt;div class="footer-item"&gt;
        &lt;div class="item"&gt;
            &lt;h3&gt;关于我们&lt;/h3&gt;
            &lt;div&gt;&lt;a href="&lt;?php echo home_url(); ?&gt;/常见问题"&gt;常见问题&lt;/a&gt;&lt;/div&gt;
            &lt;div&gt;&lt;a href="&lt;?php echo home_url(); ?&gt;/留言板"&gt;联系我们&lt;/a&gt;&lt;/div&gt;
        &lt;/div&gt;
        &lt;div class="item"&gt;
            &lt;h3&gt;友情链接&lt;/h3&gt;
            &lt;div&gt;&lt;a href="//www.tidnotes.ga/"&gt;小TiD笔记&lt;/a&gt;&lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="copyright"&gt;
        &lt;div&gt;Copyright © 2019 &lt;a href="//www.tidnotes.ga" title="小TiD笔记"&gt;小TiD笔记&lt;/a&gt;&lt;/div&gt;
        &lt;div&gt;Powered By WordPress | Design By Tidra&lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;

&lt;?php wp_footer(); ?&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 404.php {#step-404}

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php get_header(); ?&gt;
&lt;h2&gt;Error 404 - Not Found&lt;/h2&gt;
&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### comments.php {#step-comments}

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php
if (isset($_SERVER['SCRIPT_FILENAME']) && 'comments.php' == basename($_SERVER['SCRIPT_FILENAME']))
    die('Please do not load this page directly. Thanks!');
?&gt;

&lt;!-- 评论区 --&gt;
&lt;div class="comment"&gt;
    &lt;?php if ($post-&gt;comment_count &gt; 0) : ?&gt;
        &lt;h3 class="comment-title"&gt;回复&lt;/h3&gt;
        &lt;ol class="commentlist"&gt;
            &lt;?php
                if (!empty($post-&gt;post_password) && $_COOKIE['wp-postpass_' . COOKIEHASH] != $post-&gt;post_password) {
                    // if there's a password
                    // and it doesn't match the cookie
                    ?&gt;
                &lt;li class="decmt-box"&gt;
                    &lt;p&gt;&lt;a href="#addcomment"&gt;请输入密码再查看评论内容.&lt;/a&gt;&lt;/p&gt;
                &lt;/li&gt;
            &lt;?php
                } else if (!comments_open()) {
                    ?&gt;
                &lt;li class="decmt-box"&gt;
                    &lt;p&gt;&lt;a href="#addcomment"&gt;评论功能已经关闭!&lt;/a&gt;&lt;/p&gt;
                &lt;/li&gt;
            &lt;?php
                } else if (!have_comments()) {
                    ?&gt;
                &lt;li class="decmt-box"&gt;
                    &lt;p&gt;&lt;a href="#addcomment"&gt;还没有任何评论，你来说两句吧&lt;/a&gt;&lt;/p&gt;
                &lt;/li&gt;
            &lt;?php
                } else {
                    wp_list_comments('type=comment&callback=aurelius_comment');
                }
                ?&gt;
        &lt;/ol&gt;
    &lt;?php endif; ?&gt;
    &lt;?php
    if (!comments_open()) :
    // If registration required and not logged in.
    elseif (get_option('comment_registration') && !is_user_logged_in()) :
        ?&gt;
        &lt;p&gt;你必须 &lt;a href="&lt;?php echo wp_login_url(get_permalink()); ?&gt;"&gt;登录&lt;/a&gt; 才能发表评论.&lt;/p&gt;
    &lt;?php else : ?&gt;
        &lt;form id="commentform" name="commentform" action="&lt;?php echo get_option('siteurl'); ?&gt;/wp-comments-post.php" method="post"&gt;
            &lt;h3 class="comment-title"&gt;发表评论&lt;/h3&gt;
            &lt;div class="comment-list"&gt;
                &lt;?php if (!is_user_logged_in()) : ?&gt;
                    &lt;div class="comment-author"&gt;&lt;input type="text" name="author" id="author" placeholder="昵称*" value="&lt;?php echo $comment_author; ?&gt;" size="23" tabindex="1" /&gt;&lt;/div&gt;
                    &lt;div class="comment-email"&gt;&lt;input type="text" name="email" id="email" placeholder="电子邮件*" value="&lt;?php echo $comment_author_email; ?&gt;" size="23" tabindex="2" /&gt;&lt;/div&gt;
                    &lt;div class="comment-url"&gt;&lt;input type="text" name="url" id="url" placeholder="网址(选填)" value="&lt;?php echo $comment_author_url; ?&gt;" size="23" tabindex="3" /&gt;&lt;/div&gt;
                &lt;?php else : ?&gt;
                    &lt;p&gt;您已登录:&lt;a href="&lt;?php echo get_option('siteurl'); ?&gt;/wp-admin/profile.php"&gt;&lt;?php echo $user_identity; ?&gt;&lt;/a&gt;. &lt;a href="&lt;?php echo wp_logout_url(get_permalink()); ?&gt;" title="退出登录"&gt;退出 »&lt;/a&gt;&lt;/p&gt;
                &lt;?php endif; ?&gt;
            &lt;/div&gt;
            &lt;textarea id="message comment" name="comment" placeholder="评论内容..." tabindex="4" rows="3" cols="40"&gt;&lt;/textarea&gt;

            &lt;!-- Add Comment Button --&gt;
            &lt;input name="submit" type="submit" id="entry-comment-submit" class="submit-button" value="发表评论"&gt;

            &lt;?php comment_id_fields(); ?&gt;
            &lt;?php do_action('comment_form', $post-&gt;ID); ?&gt;
        &lt;/form&gt;
    &lt;?php endif; ?&gt;
&lt;/div&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 整合文件下载 {#download}

以上的基本是按照[露兜博客的《WordPress主题制作全过程》](https://www.ludou.org/create-wordpress-themes-page.html)更改的，可以点击[下载该作者的全部文件](https://xiazai.ludou.org/aurelius_final.zip)自行更改，或者[点击链接](https://github.com/Tidra/wp-tid-theme)下载我更改后的主题文件。

## 关于主题的函数 {#functions}

  * 要包含头部/页眉，请使用[<code class="language-php">get_header()</code>](https://developer.wordpress.org/reference/functions/get_header/)
  * 要包含侧边栏，请使用[<code class="language-php">get_sidebar()</code>](https://developer.wordpress.org/reference/functions/get_sidebar/)
  * 要包含页脚，请使用[<code class="language-php">get_footer()</code>](https://developer.wordpress.org/reference/functions/get_footer/)
  * 要包含搜索表单，请使用[<code class="language-php">get_search_form()</code>](https://developer.wordpress.org/reference/functions/get_search_form/)
  * 要包含自定义主题文件，请使用[<code class="language-php">get_template_part()</code>](https://developer.wordpress.org/reference/functions/get_template_part/)
      * 如文件myheader.php，则引用代码 <code class="language-php">&lt;?php get_template_part( 'myheader' ); ?&gt;</code> 。**注意：文件需要放在该主题的根目录。**

主题制作中大多数函数都是在循环（ The Loop ）中实现的，此部分详情请查看《[WordPress之主题循环（The Loop）及其函数](//www.tidnotes.ga/2019/11/wordpress-the-loop.html)》。

## 注意 {#note}

  * 注意每一部分的划分，尽量将相同的划在同一个php文件中，同时记得标签闭合问题，想header.php和footer.php中分别写是<code class="language-markup">&lt;html>&lt;body></code>和<code class="language-markup">&lt;/body>&lt;/html></code>。
  * 像 <code class="language-php">the_author()</code>函数一定要写在循环（The Loop）中。
  * 一个页面中尽量只使用一次循环。如果像在header.php中使用了循环，page.php再使用会出现错误，如果需要的话可以使用多次循环解决这个问题。多次循环可以查看《[WordPress之主题循环（The Loop）及其函数](//www.tidnotes.ga/2019/11/wordpress-the-loop.html)》，或者[官方文件](https://developer.wordpress.org/themes/basics/the-loop/)。
  * functions.php文件中，所有函数都应该写在<code class="language-php">&lt;?php //注释 ?></code>中，注释不要在标签外用<code class="language-markup">&lt;!-- 注释 --></code>，同时是php标签间也尽量不要有空行，否则有可能将空行等内容显示在html的最开始位置，从而造成错误。
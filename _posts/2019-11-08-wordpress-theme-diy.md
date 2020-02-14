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

在[官方的模板层次结构](https://developer.wordpress.org/themes/basics/template-hierarchy/)中也介绍了各种页面的加载顺序，大家想要了解更详细的内容可以到官方网站中查看相关内容。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构-1024x639.png" alt="WordPress主题模板层次结构可视图 | 小TiD笔记" class="wp-image-479" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构-1024x639.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构-300x187.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构-768x479.png 768w, https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构-1536x958.png 1536w, https://www.tidnotes.ga/wp-content/uploads/2020/01/WordPress主题模板层次结构.png 1685w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

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

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php get_header(); ?>
&lt;!-- 文章列表 -->
&lt;div class="article-list">
    &lt;!-- 循环读取文章 -->
    &lt;?php if (have_posts()) : while (have_posts()) : the_post(); ?>
            &lt;div class="post">
                &lt;!-- 标题 -->
                &lt;h3 class="title">&lt;a href="&lt;?php the_permalink(); ?>">&lt;?php the_title(); ?>&lt;/a>&lt;/h3>
                &lt;!-- 标签、日期等 -->
                &lt;p class="sub">&lt;?php the_tags('标签：', ', ', ''); ?> • &lt;?php the_time('Y年n月j日') ?> • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?>&lt;?php edit_post_link('编辑', ' • ', ''); ?>&lt;/p>
                &lt;!-- 图片 -->
                &lt;?php $large_image_url = wp_get_attachment_image_src(get_post_thumbnail_id($post->ID), 'large');
                        if ($large_image_url[0] != "") : ?>
                    &lt;img class="thumb" alt="&lt;?php the_title(); ?>" src="&lt;?php echo $large_image_url[0]; ?>" />
                &lt;?php endif; ?>
                &lt;!-- 文章简述 -->
                &lt;?php the_excerpt(); ?>
            &lt;/div>
        &lt;?php endwhile; ?>

    &lt;?php else : ?>
        &lt;h3 class="title">&lt;a href="#" rel="bookmark">未找到&lt;/a>&lt;/h3>
        &lt;p>没有找到任何文章！&lt;/p>
    &lt;?php endif; ?>
&lt;/div>
&lt;?php get_sidebar(); ?>
&lt;?php get_footer(); ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### page.php 和 single.php {#step-page}

页面和文章页差不多，主要是引入标题、正文内容和评论部分，文章页一般会在标题下加入标签、时间等信息。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;!-- 标签等 -->
&lt;p class="sub">&lt;?php the_tags('标签：', ', ', ''); ?> • &lt;?php the_time('Y年n月j日') ?> • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?>&lt;?php edit_post_link('编辑', ' • ', ''); ?>&lt;/p></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php get_header(); ?>
&lt;!-- 页面内容 -->
&lt;?php if (have_posts()) : the_post();
    update_post_caches($posts); ?>
    &lt;!-- 标题 -->
    &lt;h2 class="title">&lt;?php the_title(); ?>&lt;/h2>
    &lt;div class="article">
        &lt;!-- 正文 -->
        &lt;?php the_content(); ?>
        &lt;!-- 评论 -->
        &lt;?php comments_template(); ?>
    &lt;/div>
&lt;?php else : ?>
    &lt;div class="errorbox">
        没有找到你想要的页面！
    &lt;/div>
&lt;?php endif; ?>
&lt;?php get_sidebar(); ?>
&lt;?php get_footer(); ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### archive.php {#step-archive}

标签分类页和主页显示差不多，这里只是多了一个排序选项框，和排序所需要的代码。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php get_header(); ?>
&lt;!-- 页面 -->
&lt;!-- 文章列表 -->
&lt;div class="article-list">
    &lt;div class="sorting">
        &lt;div class="sort-by">
            &lt;h4>排序&lt;/h4>
            &lt;ul>
                &lt;li>&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'rand')) echo 'class="current"'; ?> href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' => 'rand'))); ?>">随机阅读&lt;/a>&lt;/li>
                &lt;li>&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'commented')) echo 'class="current"'; ?> href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' => 'commented'))); ?>">评论最多&lt;/a>&lt;/li>
                &lt;li>&lt;a &lt;?php if (isset($_GET['order']) && ($_GET['order'] == 'alpha')) echo 'class="current"'; ?> href="&lt;?php echo curPageURL() . '?' . http_build_query(array_merge($_GET, array('order' => 'alpha'))); ?>">标题排序&lt;/a>&lt;/li>
            &lt;/ul>
        &lt;/div>
        &lt;h4>浏览&lt;?php
                // If this is a category archive
                if (is_category()) {
                    printf('分类&lt;/h4>
			&lt;h2>' . single_cat_title('', false) . '&lt;/h2>');
                    if (category_description()) echo '&lt;p>' . category_description() . '&lt;/p>';
                    // If this is a tag archive
                } elseif (is_tag()) {
                    printf('标签&lt;/h4>
			&lt;h2>' . single_tag_title('', false) . '&lt;/h2>');
                    if (tag_description()) echo '&lt;p>' . tag_description() . '&lt;/p>';
                    // If this is a daily archive
                } elseif (is_day()) {
                    printf('日期存档&lt;/h4>
			&lt;h2>' . get_the_time('Y年n月j日') . '&lt;/h2>');
                    // If this is a monthly archive
                } elseif (is_month()) {
                    printf('月份存档&lt;/h4>
				&lt;h2>' . get_the_time('Y年n月') . '&lt;/h2>');
                    // If this is a yearly archive
                } elseif (is_year()) {
                    printf('年份存档&lt;/h4>
				&lt;h2>' . get_the_time('Y年') . '&lt;/h2>');
                    // If this is an author archive
                } elseif (is_author()) {
                    echo '&lt;/h4>&lt;h2>作者存档&lt;/h2>';
                    // If this is a paged archive
                } elseif (isset($_GET['paged']) && !empty($_GET['paged'])) {
                    echo '&lt;/h4>&lt;h2>博客存档&lt;/h2>';
                }
                ?>
    &lt;/div>
    &lt;?php
    global $wp_query;

    if (isset($_GET['order']) && ($_GET['order'] == 'rand')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' => 'rand',
            'paged' => $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query->query
        );
        query_posts($arms);
    } else if (isset($_GET['order']) && ($_GET['order'] == 'commented')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' => 'comment_count',
            'order' => 'DESC',
            'paged' => $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query->query
        );
        query_posts($arms);
    } else if (isset($_GET['order']) && ($_GET['order'] == 'alpha')) {
        $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
        $args = array(
            'orderby' => 'title',
            'order' => 'ASC',
            'paged' => $paged,
        );
        $arms = array_merge(
            $args,
            $wp_query->query
        );
        query_posts($arms);
    }
    // 循环读取文章
    if (have_posts()) : while (have_posts()) : the_post(); ?>
            &lt;div class="post">
                &lt;!-- 标题 -->
                &lt;h3 class="title">&lt;a href="&lt;?php the_permalink(); ?>">&lt;?php the_title(); ?>&lt;/a>&lt;/h3>
                &lt;!-- 标签、日期等 -->
                &lt;p class="sub">&lt;?php the_tags('标签：', ', ', ''); ?> • &lt;?php the_time('Y年n月j日') ?> • &lt;?php comments_popup_link('0 条评论', '1 条评论', '% 条评论', '', '评论已关闭'); ?>&lt;?php edit_post_link('编辑', ' • ', ''); ?>&lt;/p>
                &lt;!-- 图片 -->
                &lt;?php $large_image_url = wp_get_attachment_image_src(get_post_thumbnail_id($post->ID), 'large');
                        if ($large_image_url[0] != "") : ?>
                    &lt;img class="thumb" alt="&lt;?php the_title(); ?>" src="&lt;?php echo $large_image_url[0]; ?>" />
                &lt;?php endif; ?>
                &lt;!-- 文章简述 -->
                &lt;?php the_excerpt(); ?>
            &lt;/div>
        &lt;?php endwhile; ?>

    &lt;?php else : ?>
        &lt;h3 class="title">&lt;a href="#" rel="bookmark">未找到&lt;/a>&lt;/h3>
        &lt;p>没有找到任何文章！&lt;/p>
    &lt;?php endif; ?>
&lt;/div>
&lt;?php get_sidebar(); ?>
&lt;?php get_footer(); ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### header.php {#step-header}

头部内容基本是每一页的都要的<code class="language-markup">&lt;head&gt;</code>标签内容。这里主要是给出了自定义的标题和关键词、描述内容。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;!DOCTYPE html>
&lt;html>

&lt;head>
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0">
    &lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    &lt;title>&lt;?php if (is_home()) {
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
            } ?>&lt;/title>
    &lt;!-- 关键词、描述 -->
    &lt;?php
    if (is_home() || is_page()) {
        $description = '小tid笔记，记录各种技术性文章，为大家提供简单、有效的、易上手的各种技术和便捷功能，有问题随时欢迎留言提问';
        $keywords = 'TiD,小tid,小tid笔记,tidnotes,技术,wordpress,前端,js';
    } elseif (is_single()) {
        if ($post->post_excerpt) { //如果文章摘要存在就以文章摘要为描述
            $description = $post->post_excerpt;
            $description = str_replace("\r\n", "", $description);
            $description = str_replace("\n", "", $description);
            $description = str_replace("\"", "'", $description);
            $description .= '...';
        } else { //如果文章摘要不存在就截断文章前200字为描述
            $description = mb_strimwidth(strip_tags($post->post_content), 0, 200, "");
            $description = str_replace("\r\n", "", $description);
            $description = str_replace("\n", "", $description);
            $description = str_replace("\"", "'", $description);
            $description .= '...';
        }
        $keywords = "";
        $tags = wp_get_post_tags($post->ID);
        foreach ($tags as $tag) {
            $keywords = $keywords . $tag->name . ",";
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
    ?>
    &lt;meta name="description" content="&lt;?php echo $description; ?>" />
    &lt;meta name="keywords" content="&lt;?php echo $keywords; ?>" />
    &lt;link rel="alternate" type="application/rss+xml" title="RSS 2.0 - 所有文章" href="&lt;?php bloginfo('rss2_url'); ?>" />
    &lt;link rel="pingback" href="&lt;?php bloginfo('pingback_url'); ?>" />
    &lt;!-- 样式表 -->
    &lt;link rel="stylesheet" href="&lt;?php bloginfo('stylesheet_url'); ?>" type="text/css" media="screen" />
&lt;/head>

&lt;body>
    &lt;header class="banner banner-pattern-seaOfClouds">
        &lt;h2>&lt;?php bloginfo('name'); ?>&lt;/h2>
        &lt;h3>&lt;?php bloginfo('description'); ?>&lt;/h3>
    &lt;/header></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### sidebar.php {#step-sidebar}

这部分可以根据自己的需要改写侧边栏内容，自己的部分只需要写在 <code class="language-markup">&lt;div&nbsp;class="sidebar"&gt;&lt;/div&gt;</code> 内就行。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;!-- 侧边栏 -->
&lt;div class="sidebar">
    &lt;?php if (!function_exists('dynamic_sidebar') || !dynamic_sidebar('First_sidebar')) : ?>
        &lt;h4>分类目录&lt;/h4>
        &lt;ul>
            &lt;?php wp_list_categories('depth=1&title_li=&orderby=id&show_count=0&hide_empty=1&child_of=0'); ?>
        &lt;/ul>
        &lt;h4>最近文章&lt;/h4>
        &lt;ul>
            &lt;?php
                $posts = get_posts('numberposts=6&orderby=post_date');
                foreach ($posts as $post) {
                    setup_postdata($post);
                    echo '&lt;li>&lt;a href="' . get_permalink() . '">' . get_the_title() . '&lt;/a>&lt;/li>';
                }
                $post = $posts[0];
                ?>
        &lt;/ul>
    &lt;?php endif; ?>

    &lt;?php if (!function_exists('dynamic_sidebar') || !dynamic_sidebar('Second_sidebar')) : ?>
        &lt;h4>标签云&lt;/h4>
        &lt;div class="tag-cloud">
            &lt;?php
                $tags = get_tags();
                foreach ($tags as $tag) {
                    $tag_link = get_tag_link($tag->term_id);
                    echo "&lt;a href='{$tag_link}' title='查看关于“{$tag->name}”的文章' rel='{$tag->name} Tag'>{$tag->name}&lt;/a>";
                } ?>
        &lt;/div>
    &lt;?php endif; ?>
&lt;/div></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### footer.php {#step-footer}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;!-- 底部 -->
&lt;div class="footer">
    &lt;div class="footer-item">
        &lt;div class="item">
            &lt;h3>关于我们&lt;/h3>
            &lt;div>&lt;a href="&lt;?php echo home_url(); ?>/常见问题">常见问题&lt;/a>&lt;/div>
            &lt;div>&lt;a href="&lt;?php echo home_url(); ?>/留言板">联系我们&lt;/a>&lt;/div>
        &lt;/div>
        &lt;div class="item">
            &lt;h3>友情链接&lt;/h3>
            &lt;div>&lt;a href="//www.tidnotes.ga/">小TiD笔记&lt;/a>&lt;/div>
        &lt;/div>
    &lt;/div>
    &lt;div class="copyright">
        &lt;div>Copyright © 2019 &lt;a href="//www.tidnotes.ga" title="小TiD笔记">小TiD笔记&lt;/a>&lt;/div>
        &lt;div>Powered By WordPress | Design By Tidra&lt;/div>
    &lt;/div>
&lt;/div>

&lt;?php wp_footer(); ?>

&lt;/body>
&lt;/html></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 404.php {#step-404}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php get_header(); ?>
&lt;h2>Error 404 - Not Found&lt;/h2>
&lt;?php get_sidebar(); ?>
&lt;?php get_footer(); ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### comments.php {#step-comments}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php
if (isset($_SERVER['SCRIPT_FILENAME']) && 'comments.php' == basename($_SERVER['SCRIPT_FILENAME']))
    die('Please do not load this page directly. Thanks!');
?>

&lt;!-- 评论区 -->
&lt;div class="comment">
    &lt;?php if ($post->comment_count > 0) : ?>
        &lt;h3 class="comment-title">回复&lt;/h3>
        &lt;ol class="commentlist">
            &lt;?php
                if (!empty($post->post_password) && $_COOKIE['wp-postpass_' . COOKIEHASH] != $post->post_password) {
                    // if there's a password
                    // and it doesn't match the cookie
                    ?>
                &lt;li class="decmt-box">
                    &lt;p>&lt;a href="#addcomment">请输入密码再查看评论内容.&lt;/a>&lt;/p>
                &lt;/li>
            &lt;?php
                } else if (!comments_open()) {
                    ?>
                &lt;li class="decmt-box">
                    &lt;p>&lt;a href="#addcomment">评论功能已经关闭!&lt;/a>&lt;/p>
                &lt;/li>
            &lt;?php
                } else if (!have_comments()) {
                    ?>
                &lt;li class="decmt-box">
                    &lt;p>&lt;a href="#addcomment">还没有任何评论，你来说两句吧&lt;/a>&lt;/p>
                &lt;/li>
            &lt;?php
                } else {
                    wp_list_comments('type=comment&callback=aurelius_comment');
                }
                ?>
        &lt;/ol>
    &lt;?php endif; ?>
    &lt;?php
    if (!comments_open()) :
    // If registration required and not logged in.
    elseif (get_option('comment_registration') && !is_user_logged_in()) :
        ?>
        &lt;p>你必须 &lt;a href="&lt;?php echo wp_login_url(get_permalink()); ?>">登录&lt;/a> 才能发表评论.&lt;/p>
    &lt;?php else : ?>
        &lt;form id="commentform" name="commentform" action="&lt;?php echo get_option('siteurl'); ?>/wp-comments-post.php" method="post">
            &lt;h3 class="comment-title">发表评论&lt;/h3>
            &lt;div class="comment-list">
                &lt;?php if (!is_user_logged_in()) : ?>
                    &lt;div class="comment-author">&lt;input type="text" name="author" id="author" placeholder="昵称*" value="&lt;?php echo $comment_author; ?>" size="23" tabindex="1" />&lt;/div>
                    &lt;div class="comment-email">&lt;input type="text" name="email" id="email" placeholder="电子邮件*" value="&lt;?php echo $comment_author_email; ?>" size="23" tabindex="2" />&lt;/div>
                    &lt;div class="comment-url">&lt;input type="text" name="url" id="url" placeholder="网址(选填)" value="&lt;?php echo $comment_author_url; ?>" size="23" tabindex="3" />&lt;/div>
                &lt;?php else : ?>
                    &lt;p>您已登录:&lt;a href="&lt;?php echo get_option('siteurl'); ?>/wp-admin/profile.php">&lt;?php echo $user_identity; ?>&lt;/a>. &lt;a href="&lt;?php echo wp_logout_url(get_permalink()); ?>" title="退出登录">退出 »&lt;/a>&lt;/p>
                &lt;?php endif; ?>
            &lt;/div>
            &lt;textarea id="message comment" name="comment" placeholder="评论内容..." tabindex="4" rows="3" cols="40">&lt;/textarea>

            &lt;!-- Add Comment Button -->
            &lt;input name="submit" type="submit" id="entry-comment-submit" class="submit-button" value="发表评论">

            &lt;?php comment_id_fields(); ?>
            &lt;?php do_action('comment_form', $post->ID); ?>
        &lt;/form>
    &lt;?php endif; ?>
&lt;/div></code></pre>
  
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

  * 注意每一部分的划分，尽量将相同的划在同一个php文件中，同时记得标签闭合问题，想header.php和footer.php中分别写是<code class="language-markup">&lt;html&gt;&lt;body&gt;</code>和<code class="language-markup">&lt;/body&gt;&lt;/html&gt;</code>。
  * 像 <code class="language-php">the_author()</code>函数一定要写在循环（The Loop）中。
  * 一个页面中尽量只使用一次循环。如果像在header.php中使用了循环，page.php再使用会出现错误，如果需要的话可以使用多次循环解决这个问题。多次循环可以查看《[WordPress之主题循环（The Loop）及其函数](//www.tidnotes.ga/2019/11/wordpress-the-loop.html)》，或者[官方文件](https://developer.wordpress.org/themes/basics/the-loop/)。
  * functions.php文件中，所有函数都应该写在<code class="language-php">&lt;?php //注释 ?&gt;</code>中，注释不要在标签外用<code class="language-markup">&lt;!--&nbsp;注释&nbsp;--&gt;</code>，同时是php标签间也尽量不要有空行，否则有可能将空行等内容显示在html的最开始位置，从而造成错误。
---
id: 362
title: WordPress之主题循环(The Loop)、参数$post及其函数
date: 2019-11-09T16:19:43+08:00
author: TiD
layout: post
guid: http://www.tidnotes.ga/?p=362
permalink: /2019/11/wordpress-the-loop.html
categories:
  - WordPress使用技巧
tags:
  - Loop
  - post
  - WordPress
  - 主题
  - 主题制作
  - 函数
  - 循环
---
<blockquote class="wp-block-quote">
  <p>
    本文主要介绍主题制作时会用到的循环（The Loop）的使用方法，以及在循环中使用的WordPress函数，解答上文《<a href="http://www.tidnotes.ga/2019/11/wordpress-theme-diy.html">WordPress之主题制作</a>》中参数的问题；同时会涉及到参数 <a href="#post-it">$post</a>，本文也会详细介绍这个参数。
  </p>
  
  <cite>官方文档介绍：<a href="https://developer.wordpress.org/themes/basics/the-loop/">https://developer.wordpress.org/themes/basics/the-loop/</a> 、<br /> <a href="https://developer.wordpress.org/reference/classes/wp_post/">https://developer.wordpress.org/reference/classes/wp_post/</a> </cite>
</blockquote>

## 简介

循环是WordPress用于通过主题[模板文件](https://developer.wordpress.org/themes/basics/template-files/)输出帖子的默认机制。在循环中，WordPress检索要显示在当前页面上的每个帖子，并根据主题说明对其进行格式化。

循环可以应用于但不限于以下地方：

  * 在博客首页显示帖子标题和摘要；
  * 在单个帖子上显示内容和评论；
  * 使用模板标签在单个页面上显示内容；
  * 显示“自定义帖子类型”和“自定义字段”中的数据。

<!--more-->

## 详细说明及用法介绍

### 基本用法

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php 
if ( have_posts() ) : 
    while ( have_posts() ) : the_post(); 
        // 显示内容
    endwhile; 
endif; 
?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

上面就是循环的基本语句，将自己要显示的内容填写在上文注释部分即可。这段循环可以用在主页显示帖子标题和摘要上。

其中，利用 if 条件语句，先判断是否有帖子（<code class="language-php">have_posts()</code>），再用 while 循环语句。**注意：if 和 while 都需要结束语，if 对应的结束语是 endif，while 对应的是 endwhile。**

  * <code class="language-php">have_posts()</code>：被调用时实际上是调用全局变量<code class="language-php">$wp_query-&gt;have_posts()</code>成员函数，来简单检查一个全局数组（array）变量 $posts 的一个循环计数器，以确认是否还有post，如果有返回true(1)，如果没有返回false(0)。
  * <code class="language-php">the_post()</code>：调用<code class="language-php">$wp_query-&gt;the_post()</code>成员函数前移循环计数器，并且创建一个全局变量 [$post](#post-it) (不是 $posts )，把当前的post的所有信息都填进这个$post变量中，以备接下来使用。

### 循环中常见的模板标签

  * [<code class="language-php">next_post_link()</code>](https://developer.wordpress.org/reference/functions/next_post_link/)：指向当前帖子**之后**按时间顺序发布的帖子的链接
  * [<code class="language-php">previous_post_link()</code>](https://developer.wordpress.org/reference/functions/previous_post_link/)：指向当前帖子**之前**按时间顺序发布的帖子的链接
  * [<code class="language-php">the_category()</code>](https://developer.wordpress.org/reference/functions/the_category/)&nbsp;：与正在查看的帖子或页面相关的一个或多个类别
  * [<code class="language-php">the_author()</code>](https://developer.wordpress.org/reference/functions/the_author/)&nbsp;：帖子或页面的作者
  * [<code class="language-php">the_content()</code>](https://developer.wordpress.org/reference/functions/the_content/)&nbsp;：帖子或页面的主要内容
  * [<code class="language-php">the_excerpt()</code>](https://developer.wordpress.org/reference/functions/the_excerpt/)：帖子主要内容的前55个单词，后接省略号（…）或阅读全文的链接。您也可以使用帖子的“摘录”字段来自定义特定摘录的长度。
  * [<code class="language-php">the_ID()</code>](https://developer.wordpress.org/reference/functions/the_id/)&nbsp;：帖子或页面的ID
  * [<code class="language-php">the_meta()</code>](https://developer.wordpress.org/reference/functions/the_meta/)&nbsp;：与帖子或页面关联的自定义字段
  * [<code class="language-php">the_shortlink()</code>](https://developer.wordpress.org/reference/functions/the_shortlink/)&nbsp;：使用网站的网址和帖子或页面的ID的页面或帖子的链接
  * [<code class="language-php">the_tags()</code>](https://developer.wordpress.org/reference/functions/the_tags/)&nbsp;：与帖子相关的一个或多个标签
  * [<code class="language-php">the_title()</code>](https://developer.wordpress.org/reference/functions/the_title/)&nbsp;：帖子或页面的标题
  * [<code class="language-php">the_time()</code>](https://developer.wordpress.org/reference/functions/the_time/)：帖子或页面的时间或日期。可以使用标准的php日期函数格式进行自定义。

以上的函数需要在循环中，主要原因是因为它们需要设置全局变量 [$post](#post-it)。所以只要能得到变量 [$post](http://www.tidnotes.ga/wp-admin/post.php?post=362&action=edit#post-it) ，即可调用上面的函数。所以在文章页（single）、页面（page），可以用下面的代码即可代替循环。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php if (have_posts()) : the_post(); ?>
    // 页面内容
    &lt;?php the_content(); ?>
&lt;?php endif; ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 多个循环

在一个页面中，如果使用了循环，如果再次使用则会出错。例如在header.php中输出了文章标题，再在page.php中使用 <code class="language-php">&lt;?php&nbsp;if&nbsp;(have_posts())&nbsp;:&nbsp;the_post();&nbsp;?&gt; </code>会出现错误，得到并非想要的内容。所以这时候就要使用多循环。

例如，您可能想要在页面顶部的目录列表中显示帖子的标题，然后在页面下方显示内容。由于查询没有被更改，因此当我们需要第二次遍历帖子时，我们只需要倒退循环。为此，我们将使用功能[<code class="language-php">rewind_posts()</code>](https://developer.wordpress.org/reference/functions/rewind_posts/)。 

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers language-php"><code>&lt;?php
// 第一次循环
if ( have_posts() ) : 
    while ( have_posts() ) : the_post();
        the_title();
    endwhile;
endif;
 
// 使用rewind_posts()使第二次循环正常执行
rewind_posts();
 
// 第二次循环
while ( have_posts() ) : the_post();
    the_content();
endwhile;
?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 关于参数$post {#post-it}

下面是常用的 $post 的变量索引，更多内容可以查看[WP_Post](https://developer.wordpress.org/reference/classes/wp_post/)的详细说明：

  * <code class="language-php">$post–&gt;ID</code>：当前文章的ID；
  * <code class="language-php">$post–&gt;post_category</code>：检索文章类别；
  * <code class="language-php">$post–&gt;post_parent</code>：父页面。用于创建自定义导航元素；
  * <code class="language-php">$post–&gt;post_title</code>：文章标题；
  * <code class="language-php">$post–&gt;post_excerpt</code>：文章摘要；
  * <code class="language-php">$post–&gt;post_content</code>：检索所有文章内容以及任何标记；
  * <code class="language-php">$post–&gt;post_name</code>：检索帖子的别名；
  * <code class="language-php">$post–&gt;guid</code>：文章 Url；
  * <code class="language-php">$post–&gt;post_author</code>：文章作者ID；
  * <code class="language-php">$post–&gt;post_type</code>：返回分类类型，包括自定义分类、page或者post；
  * <code class="language-php">$post–&gt;post_date</code>：检索发布文章的本地时间戳；
  * <code class="language-php">$post-&gt;post_modified</code>：文章修改的本地时间；
  * <code class="language-php">$post–&gt;post_status</code>：检索文章的状态：发布，私有，草稿，等待复审；
  * <code class="language-php">$post–&gt;comment_count</code>：返回文章的评论数量。

上述参数可以根据大家需要修改主题文件，或者制作自己的主题。制作主题的教程可以到《[WordPress之主题制作](http://www.tidnotes.ga/2019/11/wordpress-theme-diy.html)》一文去查看。

<hr class="wp-block-separator" />

<p style="font-size:12px" class="h5c">
  官方文档介绍：<a href="https://developer.wordpress.org/themes/basics/the-loop/">https://developer.wordpress.org/themes/basics/the-loop/</a> 、<br /> <a href="https://developer.wordpress.org/reference/classes/wp_post/">https://developer.wordpress.org/reference/classes/wp_post/</a> <br />have_posts()、the_post()解析参考：<a href="https://www.cnblogs.com/drawblog/articles/8351327.html">https://www.cnblogs.com/drawblog/articles/8351327.html</a><br />$post参数参考：<a href="http://www.xuxiaoke.com/wpquestion/174.html">http://www.xuxiaoke.com/wpquestion/174.html</a>
</p>
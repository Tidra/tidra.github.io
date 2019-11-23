---
id: 373
title: WordPress之分页导航
date: 2019-11-11T14:13:22+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=373
permalink: /2019/11/wp-pagenavi.html
image: /wp-content/uploads/2019/11/image.png
categories:
  - WordPress使用技巧
tags:
  - pagenavi
  - WordPress
  - 分页导航
  - 文章数量
  - 自定义
---
<blockquote class="wp-block-quote">
  <p>
    WordPress自带有分页显示功能，但自制主题一般会缺少分页导航，WordPress利用插件 <em>WP</em>-PageNavi 、<em>wp</em>-page-numbers 也可以实现分页导航功能。本文适用于<strong>非插件式纯代码</strong>自制分页导航或自定义分页导航样式，同时提供自定义每页显示文章数量的代码。
  </p>
  
  <cite>本文代码参考《<a href="https://cloud.tencent.com/developer/article/1344975">非插件实现WordPress分页导航</a>》一文修改。每页显示文章数量代码来自<a href="http://wordpress.stackexchange.com/questions/21/show-a-different-number-of-posts-per-page-depending-on-context-e-g-homepage">WordPress Answers</a>。</cite>
</blockquote>

## 效果图<figure class="wp-block-image">

<a href="blob:https://www.tidnotes.ga/e6a4b65e-5c6d-4401-aafe-f1aca6197dde" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/11/image.png" alt="" class="wp-image-374" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/11/image.png 502w, https://www.tidnotes.ga/wp-content/uploads/2019/11/image-300x67.png 300w" sizes="(max-width: 502px) 100vw, 502px" /></a></figure> 

## 实现方法

### 1、functions.php

首先在主题根目录下的functions.php中加入下面代码。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">if ( !function_exists('pagenavi') ) {
    function pagenavi( $p = 2 ) { // 取当前页前后各 2 页
        if ( is_singular() ) return; // 文章与插页不用
        global $wp_query, $paged;
        $max_page = $wp_query->max_num_pages;
        if ( $max_page == 1 ) return; // 只有一页不用
        if ( empty( $paged ) ) $paged = 1;
        echo '&lt;div class="pagenavi">&lt;span class="pages">Page &lt;b>' . $paged . '&lt;/b> of &lt;b>' . $max_page . '&lt;/b>&lt;/span> '; // 显示页数
	    if ( $paged > 1 ) p_link( $paged - 1, '上一页', '&lsaquo;' );/* 如果当前页大于1就显示上一页链接 */
        if ( $paged > $p + 1 ) p_link( 1, '首页' );
		if ( $paged > $p + 2 ) echo '&lt;span class="page-more">...&lt;/span>';

        for( $i = $paged - $p; $i &lt;= $paged + $p; $i++ ) { // 中间页
            if ( $i > 0 && $i &lt;= $max_page ) $i == $paged ? print "&lt;span class='page-numbers current'>{$i}&lt;/span> " : p_link( $i );
        }
		if ( $paged &lt; $max_page - $p - 1 ) echo '&lt;span class="page-more">...&lt;/span>';
	    if ( $paged &lt; $max_page - $p ) p_link( $max_page, '最后页' );
		if ( $paged &lt; $max_page ) p_link( $paged + 1,'下一页', '&rsaquo;' );/* 如果当前页不是最后一页显示下一页链接 */
		echo '&lt;/div>';
    }
   function p_link( $i, $title = '', $linktype = '' ) {
        if ( $title == '' ) $title = "第 {$i} 页";
        if ( $linktype == '' ) { $linktext = $i; } else { $linktext = $linktype; }
        echo "&lt;a class='page-numbers' href='", esc_html( get_pagenum_link( $i ) ), "' title='{$title}'>{$linktext}&lt;/a> ";
    }
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 2、显示页加入显示代码

在index.php、archive.php等页面的适当位置加入下面代码。或者将原本主题的分页导航相关代码改为下面代码。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">&lt;?php if (function_exists('pagenavi')) { pagenavi();} ?></code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 3、更改显示样式

最直接的方法是在主题根目录的style.css加入下面代码，或者写到新的样式表中导入到页面中。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-css">.pagenavi {
    display: table;
    margin: 50px auto;
}

.pages, .page-more, .page-numbers {
    height: 40px;
    width: 40px;
    font-size: 18px;
    color: #666;
    display: block;
    float: left;
    position: relative;
    text-align: center;
    margin-right: 5px;
    margin-top: 15px;
}

.pages {
    width: auto;
    font-size: 14px;
    line-height: 40px;
    margin-right: 15px;
    text-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

.page-numbers {
    line-height: 40px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    border: #666 1px solid;
    border-radius: 10px;
}

.page-numbers:hover {
    color: #fff;
    background: rgba(0, 123, 255, 0.87);
    border: 6px double #fff;
    margin-top: 10px;
    box-shadow: none;
}

.pagenavi .current, .pagenavi .current:hover {
    color: #fff;
    background: #007AFF;
    border: 6px double #fff;
    margin-top: 10px;
    box-shadow: none;
}

.page-numbers a:hover, span.current {
    text-decoration: none;
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

样式内容可以根据自己的需求更改，改为自己喜欢的样式即可。

## 附加内容

  * 想要实现页面分页，可以在WordPress（5.0以上的Gutenberg编辑器）编辑页面找到区块：**布局元素 → 分页符**。
  * 更改主页或分类页等显示文章数量，可以到后台管理的 **设置 → 阅读（ 博客页面至多显示 ）**中设置。或者在functions.php加入下面代码。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">function custom_posts_per_page($query) {
    if (is_home()) {
        $query->set('posts_per_page', 8);
    }
    if (is_search()) {
        $query->set('posts_per_page', -1);
    }
    if (is_archive()) {
        $query->set('posts_per_page', 25);
    } //endif
} //function

//this adds the function above to the 'pre_get_posts' action     
add_action('pre_get_posts', 'custom_posts_per_page');</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>
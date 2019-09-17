---
id: 106
title: WordPress代码样式更改
date: 2019-08-18T01:04:08+08:00
author: TiD
layout: revision
guid: https://tidnotes.ga/2019/08/60-revision-v1.html
permalink: /2019/08/60-revision-v1.html
---
<blockquote class="wp-block-quote">
  <p>
    本文主要是简述怎样实现在网页中插入的代码实现高亮显示
  </p>
  
  <cite>小编为了实现类似CSDN中的代码显示，实验了不同的方案，最后得到了一个较好的结果，适用于目前最新版的WordPress 5.2.2</cite>
</blockquote>

实现的效果如下，如果有一定的前端基础，可以根据个人喜好更改样式。

<pre class="line-numbers"><code class="language-markup">&lt;html&gt;
	&lt;head&gt;
 		....
	&lt;/head&gt;
	&lt;body&gt;
		...
	&lt;/body&gt;
&lt;/html&gt;</code></pre>

## 准备工作

### 选择或编写高亮样式

有能力的同学可以自己编写样式，WordPress代码主要是由`<pre><code></code></pre>`或者`<code></code>`组成。所以编写标签`<pre>`和标签`<cord>`的样式表CSS就可以了。

小编直接使用了<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="https://prismjs.com/" target="_blank">prismjs.com</a>的样式，大家可以到<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="https://prismjs.com/download.html" target="_blank">prismjs的下载页</a>选择自己要的效果就行。也可以用小编我使用的文件<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="http://t.cn/AiHrQjH5" target="_blank">（点击下载）</a>，下载完解压缩会得到 prism.css 和 prism.js 两个文件，放到WordPress主题的根目录（如放在其他地方引用记得更改地址），即：<mark>wp安装目录/wp-content/themes/当前使用的主题/</mark>

### 改写functions.php

functions.php位于当前使用的主题目录下，就是 <mark>wp安装目录/wp-content/themes/当前使用的主题/functions.php </mark>。

在functions.php文件最后的`?>`前插入如下代码，没有`?>`就在最后加上`?>`。

<pre class="line-numbers"><code class="language-php">//Wordpress免插件实现代码高亮
//Prism.js开始
function add_prism() {
        wp_register_style(
            'prismCSS', 
            get_stylesheet_directory_uri() . '/prism.css' //自定义路径
         );
          wp_register_script(
            'prismJS',
            get_stylesheet_directory_uri() . '/prism.js' //自定义路径
         );
        wp_enqueue_style('prismCSS');
        wp_enqueue_script('prismJS');
}
add_action('wp_enqueue_scripts', 'add_prism');
//Prism.js结束</code></pre>

## 如何实现

### 方法一 ：改写 prism.css 文件 

删去prism.css 文件里code、pre后缀`[class*="language-"]`就可以看到效果了。想简便的可以用此方法。

### 方法二 ：用自定义HTML区块

WordPress 5.22的自义HTML区块可以直接写代码，格式是`<pre class="line-numbers"><code class="language-markup">自己的代码或者其他</code></pre>`。

`<pre>`标签中的 `class="line-numbers"` 是用来显示行数的，不用可以删去，`<code>`标签的class格式是`language-语言`，若果是HTML使用 `class="language-markup"` 。

如果中间添加的是HTML代码，使用转义后的代码，即`<`改为`&lt`，`>`改为`&gt`，不想转义可以在functions.php文件加入下面代码。

<pre class="line-numbers"><code class="language-php">//Pre标签内的HTML不转义
add_filter( 'the_content', 'pre_content_filter', 0 );
function pre_content_filter( $content ) {
    return preg_replace_callback( '|&lt;pre.*&gt;&lt;code.*&gt;(.*)&lt;/code&gt;&lt;/pre&gt;|isU' , 'convert_pre_entities', $content );
}

function convert_pre_entities( $matches ) {
    return str_replace( $matches[1], htmlentities( $matches[1] ), $matches[0] );
}</code></pre>

### 方法三 ：用代码编辑器（快捷键Ctrl+Shift+Alt+H）

先用代码区块将自己的代码写进去，然后打开代码编辑器，在`<pre>`、`<code>`两个标签加入相应的class就行了。

### 方法四 ：使用经典区块添加按钮
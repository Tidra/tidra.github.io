---
id: 275
title: WordPress之代码样式更改
date: 2019-09-02T22:30:27+08:00
author: TiD
layout: revision
guid: https://www.tidnotes.ga/2019/09/60-revision-v1.html
permalink: /2019/09/60-revision-v1.html
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

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 准备工作 {.h2c}

<p class="has-medium-font-size h4c">
  <strong>选择或编写高亮样式</strong>
</p>

有能力的同学可以自己编写样式，WordPress代码主要是由<code class="language-markup">&lt;pre&gt;&lt;code&gt;&lt;/code&gt;&lt;/pre&gt;</code>或者<code class="language-markup">&lt;code&gt;&lt;/code&gt;</code>组成。所以编写标签<code class="language-markup">&lt;pre&gt;</code>和标签<code class="language-markup">&lt;cord&gt;</code>的样式表CSS就可以了。

小编直接使用了<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="https://prismjs.com/" target="_blank">prismjs.com</a>的样式，大家可以到<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="https://prismjs.com/download.html" target="_blank">prismjs的下载页</a>选择自己要的效果就行。也可以用小编我使用的文件<a rel="noreferrer noopener" aria-label="（在新窗口打开）" href="http://t.cn/AiHrQjH5" target="_blank">（点击下载）</a>，下载完解压缩会得到 prism.css 和 prism.js 两个文件，放到WordPress主题的根目录（如放在其他地方引用记得更改地址），即：<mark>wp安装目录/wp-content/themes/当前使用的主题/</mark>

<p class="has-medium-font-size h4c">
  <strong>改写functions.php</strong>
</p>

functions.php位于当前使用的主题目录下，就是 <mark>wp安装目录/wp-content/themes/当前使用的主题/functions.php </mark>。

在functions.php文件最后的<code class="language-markup">?&gt;</code>前插入如下代码，没有<code class="language-markup">?&gt;</code>就在最后加上<code class="language-markup">?&gt;</code>。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">//Wordpress免插件实现代码高亮
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
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 如何实现 {.h2c}

<p class="has-medium-font-size h4c">
  <strong>方法一 ：改写 prism.css 文件 </strong>
</p>

删去prism.css 文件里code、pre后缀<code class="language-markup">[class*="language-"]</code>就可以看到效果了。想简便的可以用此方法。

<p class="has-medium-font-size h4c">
  <strong>方法二 ：用自定义HTML区块</strong>
</p>

WordPress 5.22的自义HTML区块可以直接写代码，格式是<code class="language-markup">&lt;pre class="line-numbers"&gt;&lt;code class="language-markup"&gt;自己的代码或者其他&lt;/code&gt;&lt;/pre&gt;</code>。

<code class="language-markup">&lt;pre&gt;</code>标签中的 <code class="language-markup">class="line-numbers"</code> 是用来显示行数的，不用可以删去，<code class="language-markup">&lt;code&gt;</code>标签的class格式是<code class="language-markup">language-语言</code>，若果是HTML使用 <code class="language-markup">class="language-markup" </code>。

如果中间添加的是HTML代码，使用转义后的代码，即<code class="language-markup">&lt;</code>改为<code class="language-markup">&lt</code>，<code class="language-markup">&gt;</code>改为<code class="language-markup">&gt</code>，不想转义可以在functions.php文件加入下面代码。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">//Pre标签内的HTML不转义
add_filter( 'the_content', 'pre_content_filter', 0 );
function pre_content_filter( $content ) {
    return preg_replace_callback( '|&lt;pre.*>&lt;code.*>(.*)&lt;/code>&lt;/pre>|isU' , 'convert_pre_entities', $content );
}

function convert_pre_entities( $matches ) {
    return str_replace( $matches[1], htmlentities( $matches[1] ), $matches[0] );
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<p class="has-medium-font-size h4c">
  <strong>方法三 ：用代码编辑器（快捷键Ctrl+Shift+Alt+H）</strong>
</p>

先用代码区块将自己的代码写进去，然后打开代码编辑器，在<code class="language-markup">&lt;pre&gt;</code>、<code class="language-markup">&lt;code&gt;</code>两个标签加入相应的class就行了。

<p class="has-text-color has-medium-font-size has-very-dark-gray-color h4c">
  <strong>方法四 ：使用经典区块添加按钮</strong>
</p>

这是我目前使用的方法，摸索时间最长，自我觉得使用起来最简便，设置会多一点（直接复制代码简单很多）。这一方法小编直接在[《WordPress之经典区块自定义按钮》](https://tidnotes.ga/2019/08/wordpress之经典区块自定义按钮.html)一文详细介绍。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

* * *

#### 主要参考链接以及代码来源

<ul style="list-style-type: square;">
  <li>
    <p>
      <a href="https://www.uoo2.com/wordpress-code-light.html" target="_blank" rel="noopener noreferrer">免插件实现WordPress代码高亮显示</a>
    </p>
  </li>
  
  <li>
    <p class="postTitle">
      <a id="cb_post_title_url" class="postTitle2" href="https://www.cnblogs.com/xbdeng/p/5296557.html">小板邓：wordpress如何扩展TinyMCE编辑器，添加自定义按钮及功能</a>
    </p>
  </li>
  
  <li>
    <a id="cb_post_title_url" class="postTitle2" href="https://www.cnblogs.com/huangcong/p/4787867.html">黄聪：TinyMCE 4 增强 添加样式、按钮、字体、下拉菜单和弹出式窗口</a>
  </li>
</ul>
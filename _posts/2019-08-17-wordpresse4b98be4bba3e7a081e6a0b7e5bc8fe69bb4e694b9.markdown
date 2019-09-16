---
author: TiD
comments: true
date: 2019-08-17 05:15:43+00:00
layout: post
link: https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e4%bb%a3%e7%a0%81%e6%a0%b7%e5%bc%8f%e6%9b%b4%e6%94%b9.html
slug: wordpress%e4%b9%8b%e4%bb%a3%e7%a0%81%e6%a0%b7%e5%bc%8f%e6%9b%b4%e6%94%b9
title: WordPress之代码样式更改
wordpress_id: 60
categories:
- WordPress使用技巧
tags:
- '5.2'
- Gutenberg（古腾堡）
- WordPress
- 代码样式
---




<blockquote>本文主要是简述怎样实现在网页中插入的代码实现高亮显示
> 
> 小编为了实现类似CSDN中的代码显示，实验了不同的方案，最后得到了一个较好的结果，适用于目前最新版的WordPress 5.2.2</blockquote>







实现的效果如下，如果有一定的前端基础，可以根据个人喜好更改样式。





    
    <code class="language-markup"><html>
    	<head>
     		....
    	</head>
    	<body>
    		...
    	</body>
    </html></code>








## 准备工作







**选择或编写高亮样式**







有能力的同学可以自己编写样式，WordPress代码主要是由`<pre><code></code></pre>`或者`<code></code>`组成。所以编写标签`<pre>`和标签`<cord>`的样式表CSS就可以了。







小编直接使用了[prismjs.com](https://prismjs.com/)的样式，大家可以到[prismjs的下载页](https://prismjs.com/download.html)选择自己要的效果就行。也可以用小编我使用的文件[（点击下载）](http://t.cn/AiHrQjH5)，下载完解压缩会得到 prism.css 和 prism.js 两个文件，放到WordPress主题的根目录（如放在其他地方引用记得更改地址），即：wp安装目录/wp-content/themes/当前使用的主题/







**改写functions.php**







functions.php位于当前使用的主题目录下，就是 wp安装目录/wp-content/themes/当前使用的主题/functions.php 。






在functions.php文件最后的`?>`前插入如下代码，没有`?>`就在最后加上`?>`。





    
    <code class="lan language-php">//Wordpress免插件实现代码高亮
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
    //Prism.js结束</code>

点击复制









## 如何实现







**方法一 ：改写 prism.css 文件 **







删去prism.css 文件里code、pre后缀`[class*="language-"]`就可以看到效果了。想简便的可以用此方法。







**方法二 ：用自定义HTML区块**







WordPress 5.22的自义HTML区块可以直接写代码，格式是`<pre class="line-numbers"><code class="language-markup">自己的代码或者其他</code></pre>`。







`<pre>`标签中的 `class="line-numbers"` 是用来显示行数的，不用可以删去，`<code>`标签的class格式是`language-语言`，若果是HTML使用 `class="language-markup" `。







如果中间添加的是HTML代码，使用转义后的代码，即`<`改为`&lt`，`>`改为`&gt`，不想转义可以在functions.php文件加入下面代码。






    
    <code class="lan language-php">//Pre标签内的HTML不转义
    add_filter( 'the_content', 'pre_content_filter', 0 );
    function pre_content_filter( $content ) {
        return preg_replace_callback( '|<pre.*><code.*>(.*)</code></pre>|isU' , 'convert_pre_entities', $content );
    }
    
    function convert_pre_entities( $matches ) {
        return str_replace( $matches[1], htmlentities( $matches[1] ), $matches[0] );
    }</code>

点击复制







**方法三 ：用代码编辑器（快捷键Ctrl+Shift+Alt+H）**







先用代码区块将自己的代码写进去，然后打开代码编辑器，在`<pre>`、`<code>`两个标签加入相应的class就行了。







**方法四 ：使用经典区块添加按钮**







这是我目前使用的方法，摸索时间最长，自我觉得使用起来最简便，设置会多一点（直接复制代码简单很多）。这一方法小编直接在[《WordPress之经典区块自定义按钮》](https://tidnotes.ga/2019/08/wordpress之经典区块自定义按钮.html)一文详细介绍。








* * *




#### 主要参考链接以及代码来源






  * 


[免插件实现WordPress代码高亮显示](https://www.uoo2.com/wordpress-code-light.html)





  * 


[小板邓：wordpress如何扩展TinyMCE编辑器，添加自定义按钮及功能](https://www.cnblogs.com/xbdeng/p/5296557.html)





  * [黄聪：TinyMCE 4 增强 添加样式、按钮、字体、下拉菜单和弹出式窗口](https://www.cnblogs.com/huangcong/p/4787867.html)



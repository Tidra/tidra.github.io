---
id: 163
title: WordPress之Gutenberg（古腾堡）自定义块（一）
date: 2019-08-27T17:30:28+08:00
author: TiD
layout: post
guid: https://tidnotes.ga/?p=163
permalink: '/2019/08/wordpress%E4%B9%8Bgutenberg(%E5%8F%A4%E8%85%BE%E5%A0%A1)%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9D%97(%E4%B8%80).html'
categories:
  - WordPress使用技巧
tags:
  - Gutenberg（古腾堡）
  - WordPress
  - 自定义块
---
<blockquote class="wp-block-quote">
  <p>
    本文内容主要参考 <a href="https://www.haibakeji.com/archives/author/1">海拔科技</a> 以及 <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a> ，介绍并解读新版WordPress所采用的 <em>Gutenberg 编辑器</em> <em>（ Block Editor/块编辑器 ）</em>如何创建自定义编辑块，包括块的样式以及扩展工具栏等。
  </p>
  
  <cite>本文适用于WordPress 5.22。关于WordPress Gutenberg自定义系列目录如下： <br /><em>1、</em><a href="https://www.tidnotes.ga/?p=163">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>3、</em><a href="https://www.tidnotes.ga/?p=214">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a><br /><em>4、<a href="https://www.tidnotes.ga/?p=238">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em> </cite>
</blockquote>

本文内容来自海拔科技： <https://www.haibakeji.com/archives/582.html> ，详细介绍各个属性可阅读WordPress之Gutenberg（古腾堡）自定义块（一）。

<!--more-->

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## Block介绍 {#wznav_0.h2c}

新的编辑器采用Block块的方式插入文章，把内容分成各种块，方便内容的调整和修改，同时也大大的扩展了编辑器的功能。

目前相关的中文内容还是很少，需要了解更多内容可以参考官方介绍:

  * <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/" target="_blank">Gutenberg官方网站</a>
  * <a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a>
  * <a rel="noreferrer noopener" href="https://developer.wordpress.org/resource/dashicons/#businessman" target="_blank">WordPress 官方图标</a> 

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 效果截图 {.h2c}

<ul class="wp-block-gallery columns-2 is-cropped">
  <li class="blocks-gallery-item">
    <figure><a href="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465542.gif" data-fancybox="images"><img class="wp-image-584 alignnone" src="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465542.gif" alt="" data-id="584" data-link="https://www.haibakeji.com/?attachment_id=584" /></a></figure>
  </li>
  <li class="blocks-gallery-item">
    <figure><a href="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465519.gif" data-fancybox="images"><img class="wp-image-585" src="https://www.haibakeji.com/wp-content/uploads/2019/04/2019040611465519.gif" alt="" data-id="585" data-link="https://www.haibakeji.com/?attachment_id=585" /></a></figure>
  </li>
</ul>

如图所示，通过创建自定义块可以更方便的调整文章内容功能和效果，在此我以实现上图的两个自定义块为例，一步一步的创建。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 详细教程 {#wznav_2.h2c}

创建自定义的过程大致分为三步，只要按照我的教程一步一步的来，还是很简单的

  1. 在function中注册相关的脚本文件
  2. 编辑块Block的JS文件
  3. 编辑块的css外观

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 注册 Gutenberg Block块 {#wznav_3.h3c}

找到你主题的 function.php文件，在最下方添加以下代码：

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">// 古腾堡编辑器扩展
function duxq_block() {
    wp_register_script( //引入核心js文件
        'duxq_block',
        get_stylesheet_directory_uri().'/js/gb_block.js',
        array( 'wp-blocks', 'wp-element' )
    );

    wp_register_style(  //引入css外观样式文件
        'duxq_block',
        get_stylesheet_directory_uri().'/css/editor-style.css',
        array( 'wp-edit-blocks' )
    );

    register_block_type( 'duxq/block', array(
        'editor_script' => 'duxq_block',
        'editor_style'  => 'duxq_block',
    ) );
}
if (function_exists('register_block_type')) { //判断是否使用古腾堡编辑器
    add_action( 'init', 'duxq_block' );
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 语法解释： {#wznav_4.h4c}

  * **wp\_register\_script ()&nbsp;**引入核心的js文件
  * **wp\_register\_style()&nbsp;**引入css外观样式文件
  * 最后我们检测一下是否使用古腾堡，然后排队注册

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 编辑Block块JS内容 {#wznav_5.h3c}

块是的核心就是JS文件控制的，要实现的所有功能也是靠这个就是文件。

按照我们上面引入的js文件，我们打开编辑这个文件。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-js">(function(blocks, editor, element, components, _) {
    var el = element.createElement;
    var RichText = editor.RichText;
	var AlignmentToolbar = editor.AlignmentToolbar;
    var BlockControls = editor.BlockControls;
    var Fragment = element.Fragment;

/*---------创建第一个自定义块---------*/
    blocks.registerBlockType('reilve/quote', {
        title: 'DUXQ引言',
		category: 'layout',
        icon: {
            src: 'format-quote',
            foreground: '#f85253'
        },
        description: '几种不同的引言框',
        attributes: {   //设定自定义属性
            content: {
                type: 'array',
                source: 'children',
                selector: 'span',
            },
            typeClass: {
                source: 'attribute',
                selector: '.quote_q',
                attribute: 'class',
            }
        },
        edit: function(props) {   //编辑器函数
            var content = props.attributes.content, 
            typeClass = props.attributes.typeClass || 'quote_q qe_wzk_lan',
            isSelected = props.isSelected;
            function onChangeContent(newContent) {
                props.setAttributes({
                    content: newContent
                })
            }
            function changeType(event) {
                var type = event.target.className;
                props.setAttributes({
                    typeClass: 'quote_q ' + type
                })
            }
            var richText = el(RichText, {   //内容输入框
                tagName: 'p',
                onChange: onChangeContent,
                value: content,
                isSelected: props.isSelected,
                placeholder: '请输入...'
            });
            var outerHtml = el('div', {
                className: typeClass
            },
            richText);
            var selector = el('div', {
                className: 'duxq anz'
            },
            //在此添加4个可点击的按钮
            [el('button', {className: 'qe_wzk_lan',onClick: changeType}), 
            el('button', {className: 'qe_wzk_lv',onClick: changeType}), 
            el('button', {className: 'qe_wzk_hui',onClick: changeType}),
            el('button', {className: 'qe_wzk_hong',onClick: changeType})]
            );
            return el('div', {},[outerHtml, isSelected && selector])},
        save: function(props) {   //保存的函数
            var content = props.attributes.content,
            typeClass = props.attributes.typeClass || 'quote_q qe_wzk_lan';
            var outerHtml = el('div', {
                className: typeClass
            },
            el('i', {
                className: 'fa fa-quote-left '
            }), el('span', {},
            content));
            return el('div', {},
            outerHtml)
        },
    });

/*---------创建第二个自定义块---------*/
    blocks.registerBlockType('aduxq/button', {
        title: 'UDXQ 按钮',
		category: 'layout',
        icon: {
            src: 'marker',
            foreground: '#f85253'
        },
        attributes: {
            content: {
                type: 'array',
                source: 'children',
                selector: 'span',
            },
            alignment: {
                type: 'string',
            },
            typeClass: {
                source: 'attribute',
                selector: '.an_q',
                attribute: 'class',
            }
        },
        edit: function(props) {
            var content = props.attributes.content,
            typeClass = props.attributes.typeClass || 'qe_fxan b1',
            alignment = props.attributes.alignment,
            isSelected = props.isSelected;
            function onChangeContent(newContent) {
                props.setAttributes({
                    content: newContent
                })
            }
            function changeType(event) {
                var type = event.target.className;
                props.setAttributes({
                    typeClass: 'an_q ' + type
                })
            }
            function onChangeAlignment(newAlignment) {
                props.setAttributes({
                    alignment: newAlignment
                })
            }
            var richText = el(RichText, {
                tagName: 'span',
                onChange: onChangeContent,
                value: content,
                isSelected: props.isSelected,
                placeholder: '按钮'
            });
            var outerHtml1 = el('div', {
                className: typeClass
            },
            richText);
            var outerHtml = (el(element.Fragment, null, el(BlockControls, null, el(AlignmentToolbar, {
                value: alignment,
                onChange: onChangeAlignment,
            })), outerHtml1));
            var selector = el('div', {
                className: 'duxq anz'
            },
            [el('button', {
                className: 'qe_fxan b1',
                onClick: changeType
            },
            ''), el('button', {
                className: 'qe_fxan b2',
                onClick: changeType
            },
            ''), el('button', {
                className: 'qe_fxan b3',
                onClick: changeType
            },
            ''), el('button', {
                className: 'qe_fxan b4',
                onClick: changeType
            },
            ''), el('button', {
                className: 'qe_fxan b5',
                onClick: changeType
            },
            ''), ]);
            return el('div', {
                style: {
                    textAlign: alignment
                }
            },
            [outerHtml, isSelected && selector])
        },
        save: function(props) {
            var content = props.attributes.content,
            alignment = props.attributes.alignment,
            typeClass = props.attributes.typeClass || 'qe_fxan b1';
            if (alignment) {
                var outerHtml = el('div', {
                    style: {
                        textAlign: alignment
                    }
                },
                el('span', {
                    className: typeClass
                },
                content))
            } else {
                var outerHtml = el('span', {
                    className: typeClass
                },
                content)
            }
            return outerHtml
        },
    })
})(window.wp.blocks, window.wp.editor, window.wp.element, window.wp.components, window._, );</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

在以上代码中我们创建了两个自定义块，分别是DUXQ标题和DUXQ按钮，点击块就会出现上面图片中的块，包含了文字内容输入，和几个按钮，按下按钮会切换内容的css Class，以实现外观样式的改变！

#### 语法解释： {#wznav_6.h4c}

  * **blocks, editor, i18n, element, components**等均是官方的API接口，实现数据传递
  * **blocks.registerBlockType()**&nbsp;创建Block的函数接口
  * **registerBlockType的几个参数：**title（标题）、icon（图标）、category（分组）、attributes（自定义属性）
  * 两个核心函数：**edit**&nbsp;和&nbsp;**save**&nbsp;，分别定义了编辑时候的函数和保存的函数
  * 上面我们增加了几个按钮，传递**onClick**事件，实现点击切换不同的**className**

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## css外观样式 {#wznav_7.h3c}

通过创建了自定义块，能实现加载不同的css&nbsp;**className**&nbsp;了，那我们添加一些样式，就可以看到效果了！

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-css">.duxq.anz button {
   margin: 10px;
   padding: .5em 1em;
   min-width: 33px;
   min-height: 33px;
   cursor: pointer
 }
 .duxq.anz button:hover {
   box-shadow: 0 0 10px #ddd;
   opacity: .8
 }
 .qe_wzk_hong {
   margin: 10px 0;
   padding: .6em 1em;
   border: 1px solid #f1d3d3;
   border-radius: 4px;
   background: #fff7f7;
   color: #dc3f3f
 }
 .qe_wzk_lan {
   margin: 10px 0;
   padding: .6em 1em;
   border: 1px solid #b3daf1;
   border-radius: 4px;
   background: #f7fcff;
   color: #197cb1
 }
 .qe_wzk_hui {
   margin: 10px 0;
   padding: .6em 1em;
   border: 1px solid #d4d4d4;
   background: #f5f5f5;
   color: #757575
 }
 .qe_wzk_lv {
   margin: 10px 0;
   padding: .6em 1em;
   border: 1px solid #b4e6b1;
   border-radius: 4px;
   background: #f7fff9;
   color: #1d9c24
 }
 .quote_q:before {
   content: "“";
   position: absolute;
   color: #ccc;
   font-size: 120px;
   top: -60px;
   left: 0
 }
 .qe_fxan {
   display: inline-block;
   margin: .5em;
   padding: .6em .8em;
   min-width: 80px;
   border: none;
   border-radius: 60px;
   box-shadow: -1px 4px 10px rgba(0,0,0,.2);
   color: #fff;
   text-align: center;
   transition: all .2s ease
 }
 .qe_fxan a,.qe_fxan a:hover {
   color: #fff
 }
 .qe_fxan.b1 {
   background-image: linear-gradient(135deg,#f58852 10%,#e43e2f 100%)
 }
 .qe_fxan.b2 {
   background-image: linear-gradient(135deg,#59b7fb 10%,#036bff 100%)
 }
 .qe_fxan.b3 {
   background-image: linear-gradient(135deg,#CE9FFC 10%,#7367F0 100%)
 }
 .qe_fxan.b4 {
   background-image: linear-gradient(135deg,#FCCF31 10%,#f77f2d 100%)
 }
 .qe_fxan.b5 {
   background-image: linear-gradient(135deg,#54ea98 10%,#0db757 100%)
 }</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

以上css内容除了要添加到刚刚引入的css文件中，还需要添加到主题的相关css文件中，才能实现文章页中也显示相同效果！同时css样式可能还需要根据你的主题做一些优先级调整，才能显示正确的效果，这里就不再详细赘述了！

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 提示: {.h3c}

代码添加完可在添加区块-布局元素中找到刚才添加的区块，同时你也可以给根据需要将自定义块添加到其他分组或新建分组。

本文简单介绍了怎样构建自定义块，下一文《WordPress之Gutenberg（古腾堡）自定义块（二）》将会详细解读构建过程以及个属性值。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

<p class="has-small-font-size h5c">
  <em><strong>WordPress Gutenberg其他相关自定义系列文章：</strong></em> <br /><em>1、</em><a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/?p=214">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a><br /><em>3、<a href="https://www.tidnotes.ga/?p=238">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em>
</p>
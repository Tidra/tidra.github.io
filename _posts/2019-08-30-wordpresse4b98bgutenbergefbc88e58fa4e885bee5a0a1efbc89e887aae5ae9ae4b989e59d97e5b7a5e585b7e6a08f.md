---
id: 238
title: WordPress之Gutenberg（古腾堡）自定义块工具栏
date: 2019-08-30T05:09:04+08:00
author: TiD
excerpt: WordPress Gutenberg（古腾堡）除了可以自定义区块、扩展栏，也可以自定义块工具栏。利用wp.richText.registerFormatType()可以自定义特有样式用于自定义工具栏，且可以在全部文本编辑块中以工具栏形式呈现。
layout: post
guid: https://www.tidnotes.ga/?p=238
permalink: '/2019/08/wordpress%e4%b9%8bgutenberg%ef%bc%88%e5%8f%a4%e8%85%be%e5%a0%a1%ef%bc%89%e8%87%aa%e5%ae%9a%e4%b9%89%e5%9d%97%e5%b7%a5%e5%85%b7%e6%a0%8f.html'
categories:
  - WordPress使用技巧
tags:
  - Gutenberg（古腾堡）
  - WordPress
  - 工具栏
  - 自定义块
---
<blockquote class="wp-block-quote">
  <p>
    <em>本文内容主要参考&nbsp;</em><a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a><em>&nbsp;，介绍并解读新版WordPress所采用的&nbsp;Gutenberg 编辑器&nbsp;（ Block Editor/块编辑器 ）如何创建自定义编辑块，包括块的样式以及扩展工具栏等。</em>
  </p>
  
  <cite> <em>本文适用于WordPress 5.2.2。关于WordPress Gutenberg自定义系列目录如下：</em><br /><em>1、</em><a href="https://www.tidnotes.ga/?p=163">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>3、</em><a href="https://www.tidnotes.ga/?p=214">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a><br /><em>4、<a href="https://www.tidnotes.ga/?p=238">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em> </cite>
</blockquote>

WordPress Gutenberg（古腾堡）除了可以自定义区块、扩展栏，也可以自定义块工具栏。利用<code class="language-js">wp.richText.registerFormatType()</code>可以自定义特有样式用于自定义工具栏，且可以在全部文本编辑块中以工具栏形式呈现。自定义块也可以用<code class="language-js">wp.editor.BlockControls</code>显示特有工具栏。

<!--more-->

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 效果截图 {.h2c}<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5.png" alt="Gutenberg（古腾堡）自定义块工具栏 | 小TiD笔记" class="wp-image-240" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5.png 694w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5-300x92.png 300w" sizes="(max-width: 694px) 100vw, 694px" /></a></figure> 

本文效果同《[WordPress之经典区块自定义按钮](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e7%bb%8f%e5%85%b8%e5%8c%ba%e5%9d%97%e8%87%aa%e5%ae%9a%e4%b9%89%e6%8c%89%e9%92%ae.html)》一文，将选中的代码更改为选中的样式。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 详细教程  {.h2c}

基本步骤如下：

  1. 在functions.php中注册相关的脚本文件
  2. 编辑工具栏JS文件
  3. 编辑css外观 

自定义块工具栏和自定义块基本步骤一样，但在编辑块中注册并不需要引入css文件，css文件只需要引入主题css用于在文章显示。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 注册新格式 {.h4c}

找到你主题的 function.php文件，在最下方添加以下代码：

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-php">//古腾堡编辑器工具栏
function my_custom_format_script_register() {
    wp_register_script(
        'my-custom-format-js',
        get_stylesheet_directory_uri().'/js/my-custom-format.js',
        array( 'wp-rich-text', 'wp-element', 'wp-editor', 'wp-components' )
    );
}
add_action( 'init', 'my_custom_format_script_register' );
 
function my_custom_format_enqueue_assets_editor() {
    wp_enqueue_script( 'my-custom-format-js' );
}
add_action( 'enqueue_block_editor_assets', 'my_custom_format_enqueue_assets_editor' );

//Wordpress免插件实现代码高亮
//Prism.js开始
function add_prism() {
        wp_register_style(
            'prismCSS', 
            get_stylesheet_directory_uri() . '/css/prism.css' //自定义路径
         );
          wp_register_script(
            'prismJS',
            get_stylesheet_directory_uri() . '/js/prism.js' //自定义路径
         );
        wp_enqueue_style('prismCSS');
        wp_enqueue_script('prismJS');
}
add_action('wp_enqueue_scripts', 'add_prism');
//Prism.js结束</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

wp-rich-text是注册新样式必须的，wp-element、wp-editor是自定义工具栏必须的，其他的根据需要添加到PHP文件中的dependencies数组。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 编辑js文件 {.h4c}

在你主题的js文件夹添加my-custom-format.js（根据自己的位置添加），添加以下代码：

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-js">( function( wp ) {
    var el = wp.element.createElement;
    var BlockControls = wp.editor.BlockControls;
    var DropdownMenu = wp.components.DropdownMenu;
    var richText = wp.richText;
     
    const MyDropdownMenu = function (props) {
        return el(
            BlockControls, 
            null, 
            el(
                'div',
                {className: 'components-toolbar'},
                el(
                    DropdownMenu,
                    {
                        icon: 'editor-code',
                        label: '选择语言类型',
                        controls: [
                            {
                                icon: 'editor-code',
                                title: 'js代码',
                                onClick: function() {
                                    props.onChange( richText.toggleFormat(
                                        props.value,
                                        { type: 'core/my-code' }
                                    ) );
                                }
                            },
                            {
                                icon: 'editor-code',
                                title: 'html代码',
                                onClick: function() {
                                    props.onChange( richText.toggleFormat(
                                        props.value,                                        
                                        {type: 'code', attributes: {class: 'language-markup'}}
                                    ) );
                                }
                            },
                            {
                                icon: 'editor-code',
                                title: 'css代码',
                                onClick: function() {
                                    props.onChange( richText.toggleFormat(
                                        props.value,                                        
                                        {type: 'code', attributes: {class: 'language-css'}}
                                    ) );
                                }
                            },
                        ],
                    })
                )
        );
    }

    /* -------创建定义工具栏---------*/
    richText.registerFormatType(
        'core/my-code', {
            title: 'code html',
            tagName: 'code',
            className: 'language-js',
            edit: MyDropdownMenu,
        }
    );
} )( window.wp );</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

以上是利用注册新样式来添加自定义工具栏，如果不需要注册新样式且只在特定块中显示该工具栏，只需要在所需工具栏中edit函数中添加MyDropdownMenu这一部分即可。

如果只是需要的只是单个按钮，而不是下拉框，则可以将 MyDropdownMenu 改为以下的 MyCustomButton 。

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-js">var MyCustomButton = function( props ) {
    return wp.element.createElement(
        wp.editor.RichTextToolbarButton, {
            icon: 'editor-code',
            title: 'Sample output',
            onClick: function() {
                //自定义函数
            },
        }
    );
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 语法解析：

  * **wp.editor.BlockControls**：工具栏显示元素。
  * **wp.editor.RichTextToolbarButton**：富文本按钮，基本属性如下。
      * icon：图标，同自定义块图标一样
      * title：显示的附带文字
      * label：鼠标焦点时的提示文字
      * onClick：点击调用函数
  * **wp.components.DropdownMenu**：下拉框组件，其中controls为按钮的列表，按钮的属性与 **wp.editor.RichTextToolbarButton** 相同。
  * **wp.richText.toggleFormat()**：对选中的内容应用样式，第一个变量为内容，第二个变量为样式对象。已注册样式格式为<code class="language-js">{ type: '样式名' }</code>，未注册可以用<code class="language-js">{type: '标签名', attributes: {class: '类名'}}</code>。
  * **wp.richText.registerFormatType()：**注册新样式，新样式命名规则同自定义块相同。对象的属性如下。
      * title：样式显示名
      * tagName：标签名
      * className：预设类名
      * edit：同自定义块edit函数

### CSS文件部分 {.h4c}

本文主要为实现选中代码高亮，所以同 《[WordPress之经典区块自定义按钮](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e7%bb%8f%e5%85%b8%e5%8c%ba%e5%9d%97%e8%87%aa%e5%ae%9a%e4%b9%89%e6%8c%89%e9%92%ae.html)》一文的css文件一样，这部分如有问题可以去前文去看看，这里不做详细解释。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

<p class="has-small-font-size h5c">
  <em><strong>WordPress Gutenberg其他相关自定义系列文章：</strong></em><br /> <em>1、</em><a href="https://www.tidnotes.ga/?p=163">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>3、</em><a href="https://www.tidnotes.ga/?p=214">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a>
</p>
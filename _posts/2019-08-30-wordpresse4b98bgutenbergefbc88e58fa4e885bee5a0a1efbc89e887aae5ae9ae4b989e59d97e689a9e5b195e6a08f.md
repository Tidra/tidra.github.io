---
id: 214
title: WordPress之Gutenberg（古腾堡）自定义块扩展栏
date: 2019-08-30T03:29:44+08:00
author: TiD
excerpt: 对于Gutenberg（古腾堡）自定义块，实现预设好的固定单一样式是比较简单的；但如果想更改如字体大小的样式，预设则显得较为困难。所以引入扩展栏，能使我们能更自由地更改自定义样式。本文利用之前自定义代码高亮的需求，自定义了一个带扩展栏的代码块。
layout: post
guid: https://www.tidnotes.ga/?p=214
permalink: '/2019/08/wordpress%E4%B9%8Bgutenberg(%E5%8F%A4%E8%85%BE%E5%A0%A1)%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9D%97%E6%89%A9%E5%B1%95%E6%A0%8F.html'
categories:
  - WordPress使用技巧
tags:
  - Gutenberg（古腾堡）
  - WordPress
  - 扩展栏
  - 自定义块
---
<blockquote class="wp-block-quote">
  <p>
    本文内容主要参考&nbsp;<a href="https://www.wpdaxue.com/wordpress-gutenberg-block-api-extending-blocks.html">WordPress大学</a>&nbsp;以及&nbsp;<a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a>&nbsp;，介绍并解读新版WordPress所采用的&nbsp;<em>Gutenberg 编辑器</em>&nbsp;<em>（ Block Editor/块编辑器 ）</em>如何创建自定义编辑块，包括块的样式以及扩展工具栏等。
  </p>
  
  <cite> 本文适用于WordPress 5.2.2。关于WordPress Gutenberg自定义系列目录如下：<br />1、<a href="https://www.tidnotes.ga/?p=163">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br />2、<a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br />3、<a href="https://www.tidnotes.ga/?p=214">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a> <br /><em>4、<a href="https://www.tidnotes.ga/?p=238">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em> </cite>
</blockquote>

对于Gutenberg（古腾堡）自定义块，实现预设好的固定单一样式是比较简单的；但如果想更改如字体大小的样式，预设则显得较为困难。所以引入扩展栏，能使我们能更自由地更改自定义样式。本文利用之前[自定义代码高亮](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e4%bb%a3%e7%a0%81%e6%a0%b7%e5%bc%8f%e6%9b%b4%e6%94%b9.html)的需求，自定义了一个带扩展栏的代码块。

<!--more-->

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 效果截图 {.h2c}<figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/08/image.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-1024x326.png" alt="Gutenberg（古腾堡）自定义块扩展栏 | 小TiD笔记" class="wp-image-217" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-1024x326.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image-300x96.png 300w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image-768x245.png 768w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image.png 1162w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

WordPress Gutenberg编辑器的扩展栏如上图所示，显示在右边的区块设置栏上，注意使用扩展栏时把设置_（Ctrl+Shift+,）_打开。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 详细教程 {.h2c}

Gutenberg（古腾堡）自定义块扩展栏主要步骤与创建自定义块步骤基本相同

  1. 在function中注册相关的脚本文件
  2. 编辑块Block以及扩展栏的JS文件
  3. 编辑块的css外观

步骤1与步骤3，分别在 [WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163) 和[WordPress之代码样式更改](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e4%bb%a3%e7%a0%81%e6%a0%b7%e5%bc%8f%e6%9b%b4%e6%94%b9.html)中介绍过，而且在编辑时没用应用到css外观，所以在 function中注册相关的脚本文件就不用将css文件引入，css文件引入主题样式即可。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 编辑块JS内容 {#wznav_5.h4c}

引入js文件后，编写内容如下

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-js">( function( wp ) {
    var el = wp.element.createElement;
    var blocks = wp.blocks;
    var PlainText = wp.editor.PlainText;
    var Fragment = wp.element.Fragment;
    var InspectorControls = wp.editor.InspectorControls;
    var TextControl = wp.components.TextControl;
    var RadioControl = wp.components.RadioControl;

    /* -------创建定义块---------*/
    blocks.registerBlockType('my-code/code', {
        title: '自定义代码',
        category: 'common',
        icon: {
            src: 'editor-code',
            foreground: '#f85253'
        },
        description: '代码框',
        supports: {
            customClassName: false,
            className: false,
            html: false,
        },
        attributes: {
            content: {
                type: 'string',
                source: 'html',
                selector: 'code',
            },
            typeClass: {
                source: 'attribute',
                selector: '.lan',
                attribute: 'class',
            },
            option: {
                source: 'attribute',
                selector: '.wp-block-my-code-code',
                attribute: 'class',
            }
        },
        edit: function(props) {
            var content = props.attributes.content, 
            typeClass = (props.attributes.typeClass || 'lan language-markup').replace( /lan language-/g, '' ),
            option = props.attributes.option || 'line-numbers',
            isSelected = props.isSelected;
            option = (option.search('line-numbers') &lt; 0) ? 'no-line' : 'line-numbers';

            function onChangeContent(newContent) {
                props.setAttributes({
                    content: newContent
                });
            }
            var nameText = el(Fragment, null, el(InspectorControls, { key: 'inspector' },
                el(TextControl, {
                    label: '代码语言',
                    help: "默认语言为HTML",
                    value: typeClass,
                    onChange: function (newcodeName) {
                        props.setAttributes({
                            typeClass: newcodeName
                        });
                    }
                }),
                el(RadioControl, {
                    label: "显示代码行数",
                    selected: option,
                    options: [
                        { label: '是', value: 'line-numbers' },
                        { label: '否', value: 'no-line' }
                        ],
                    onChange: function (option) {
                        props.setAttributes({
                            option: option
                        })
                    }
                })
            ));

            var text = el(PlainText, {   //内容输入框
                onChange: onChangeContent,
                value: content,
                isSelected: props.isSelected,
                placeholder: '请输入...'
            });
            var outerHtml = el('div', {
                className: 'editor-block-list__block-edit'
            }, el('div', {
                className: 'wp-block-code'
            }, text));

            return el('div', {}, outerHtml, nameText);
        },
        save: function (props) {
            var content = props.attributes.content,
            typeClass = (props.attributes.typeClass || 'lan language-markup').replace( /lan language-/g, '' ),
            option = props.attributes.option || 'line-numbers';
            var outerHtml = el('code', {
                className: 'lan language-' + typeClass
            },
            content);
            return el('pre', {className: option}, outerHtml);
        }

    })
} )( window.wp );</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

在以上代码中，我们为自定义块“自定义代码”添加了InspectorControls元素以及TextControl和RadioControl两个组件。点击块时，将显示区块设置选项卡，选项卡内显示为编辑文本框和单选按钮。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 语法解析 {.h4c}

  * **wp.editor.InspectorControls**  
    自定义块扩展栏（即设置边栏）用于显示不常用的设置或需要更多屏幕空间的设置。设置边栏应仅用于**块级设置**，而且应该时用于块全局设置，而不是选定内容。

  * **wp.components.TextControl**  
    TextControl组件允许用户输入和编辑文本 ，基本属性有：
      * **label**：标签名
      * **help**：提示语
      * **value**：编辑框内容
      * **type**&nbsp;：类型，默认text
      * **hideLabelFromVision**&nbsp;：标签是否隐藏，默认false
      * **onChange**：接收输入值的函数 <figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-2.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-2.png" alt="Gutenberg（古腾堡）文本编辑框 | 小TiD笔记" class="wp-image-227" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-2.png 555w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image-2-300x41.png 300w" sizes="(max-width: 555px) 100vw, 555px" /></a></figure> 

  * **wp.components.RadioControl**  
    RadioControl组件为单选框，基本属性有：
      * **label**：标签名
      * **help**：提示语 
      * **selected**&nbsp;：当前所选选项的value属性 
      * **options**：选项，以<code class="language-js">{label: '', value: ''}</code>键值对组成的数组
      * **onChange**：接收输入值的函数 <figure class="wp-block-image">

<a href="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-3.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-3.png" alt="Gutenberg（古腾堡）单选框 | 小TiD笔记" class="wp-image-228" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/08/image-3.png 495w, https://www.tidnotes.ga/wp-content/uploads/2019/08/image-3-300x184.png 300w" sizes="(max-width: 495px) 100vw, 495px" /></a></figure> 

  * **wp.editor.PlainText**  
    明文编辑框，由于本自定义块用于编写代码，所以不对输入文本进行转义，保留回车符，空行等格式。

该自定义块还使用了正则来获取当前块用到的类，用于更改区块样式，从而实现不同代码的高亮样式。对于Gutenberg（古腾堡）自定义块扩展栏可以根据个人需求，增加不同的组件来实现不同的功能。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

<p class="has-small-font-size h5c">
  <em><strong>WordPress Gutenberg其他相关自定义系列文章：</strong></em><br /><em>1、</em><a href="https://www.tidnotes.ga/?p=163">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/?p=208">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>3、<a href="https://www.tidnotes.ga/?p=238">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em>
</p>
---
author: TiD
comments: true
date: 2019-08-27 19:56:20+00:00
layout: post
link: https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8bgutenberg%ef%bc%88%e5%8f%a4%e8%85%be%e5%a0%a1%ef%bc%89%e8%87%aa%e5%ae%9a%e4%b9%89%e5%9d%97%ef%bc%88%e4%ba%8c%ef%bc%89.html
slug: wordpress%e4%b9%8bgutenberg%ef%bc%88%e5%8f%a4%e8%85%be%e5%a0%a1%ef%bc%89%e8%87%aa%e5%ae%9a%e4%b9%89%e5%9d%97%ef%bc%88%e4%ba%8c%ef%bc%89
title: WordPress之Gutenberg（古腾堡）自定义块（二）
wordpress_id: 208
categories:
- WordPress使用技巧
tags:
- Gutenberg（古腾堡）
- WordPress
- 自定义块
---




<blockquote>本文内容主要参考 [海拔科技](https://www.haibakeji.com/archives/author/1) 以及 [Gutenberg 开发API](https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/) ，介绍并解读新版WordPress所采用的 _Gutenberg 编辑器_ _（ Block Editor/块编辑器 ）_如何创建自定义编辑块，包括块的样式以及扩展工具栏等。
> 
> 本文适用于WordPress 5.22。关于WordPress Gutenberg自定义系列目录如下：   
_1、_[WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163)  
_2、_[WordPress之Gutenberg（古腾堡）自定义块（二）](https://www.tidnotes.ga/?p=208)  
_3、_[WordPress之Gutenberg（古腾堡）自定义块扩展栏](https://www.tidnotes.ga/?p=214)  
_4、[WordPress之Gutenberg（古腾堡）自定义块工具栏](https://www.tidnotes.ga/?p=238)_  </blockquote>







本文内容主要根据  Gutenberg 开发API ，为上文《 [WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163) 》中的js代码做解读，让大家更了解自定义的构建。









## 基本结构







利用`wp.blocks.registerBlockType('namespace/block-name', {})`来构建一个新的自定义块，基本格式如下：






    
    <code class="lan language-js">blocks.registerBlockType('namespace/block-name', {
             title: '',
             category: ''
             icon: {},
             description: '',
             attributes: {},
             edit: function(props) {},
             save: function(props) {}
    });</code>

点击复制









### 属性说明







  * namespace/block-name：自定义块的名称，其中namespace是插件或主题的名称
  * title：自定义块显示名称
  * category：所在分类目录，可选为“ common 、formatting 、layout 、widgets 、embed ”，对应分别是：常用区块、格式、布局元素、小工具、嵌入
  * icon：显示的图标
  * description：描述文字
  * attributes：自定义属性，用于保存属性值
  * edit：编辑时调用的函数，返回一个编辑时的html格式 
  * save：保存时调用的函数，返回一个最后呈现的html格式 






#### 图标（icon）







输入值为 String 或者 Object







当属性值为 String 时， 可以是任何[WordPress的Dashicons](https://developer.wordpress.org/resource/dashicons/)， 也可以是自定义svg元素。 






    
    <code class="lan language-js">// Specifying a dashicon for the block
    icon: 'book-alt',
     
    // Specifying a custom svg for the block
    icon: <svg viewBox="0 0 24 24" xmlns="<a href="http://www.w3.org/2000/svg">http://www.w3.org/2000/svg</a>"><path fill="none" d="M0 0h24v24H0V0z" /><path d="M19 13H5v-2h14v2z" /></svg>, </code>

点击复制







当属性值是Object时，如上所述，图标应该包含在src属性中。除了src之外，对象可以包含背景和前景色，例如：  






    
    <code class="lan language-js"> icon: {
         // 背景色
         background: '#7e70af',
         // 前景色
         foreground: '#fff',
         // 图标属性
         src: 'book-alt',
     } ,</code>

点击复制







#### 属性（attributes） 







用attribute从标记中提取属性的值。最简单的一个例子如下：






    
    <code class="lan language-js">{
         url: {
             type: 'string',
         }
     } </code>

点击复制







url就相当于一个字符变量，可以在自定义块中调用。在edit和save中，可以利用`props.attributes.url`调用url值，利用`props.setAttributes( { url: value } ); `设置url值。注意：type只能是 null 、 boolean 、 object 、 array 、 number 、 string 、 integer 。







作为提取属性的值，需要加入source（内容来源）和selector（过滤器）两个属性。这个根据不同的需要而相应改变，可以详细阅读 [Gutenberg 开发API ：Attributes](https://developer.wordpress.org/block-editor/developers/block-api/block-attributes/)。这里提供三个常用的例子。






    
    <code class="lan language-js">//例子1，提取块html中<code>标签内的内容到content中，返回值是字符串形式
    content: {
         type: 'string',
         source: 'html',
         selector: 'code',
     },</code>

点击复制






    
    <code class="lan language-js">//例子2，提取块中<span>标签内容到content中，返回值是数组形式
    content: {
         type: 'array',
         source: 'children',
         selector: 'span',
     },</code>

点击复制






    
    <code class="lan language-js">//例子3，提取包含类名为lan的类，用于提取某个标签的类。
    typeClass: {
         source: 'attribute',
         selector: '.lan',
         attribute: 'class',
     },</code>

点击复制







#### 函数 edit 和 save







edit 函数在编辑器的上下文中描述块的结构，显示编辑器在使用块时将呈现的内容。save函数定义了将不同属性组合到最终标记中的方式，表示块在网站前面的显示方式。 所以函数返回内容都应该是标准的HTML格式。如：






    
    <code class="lan language-js">edit: function() {
         return wp.element.createElement(
             'div',
             null,
             'Your block.'
         );
     }
     save: function() {
         return wp.element.createElement(
             'div',
             null,
             'Your block.'
         );
     }</code>

点击复制







这个需要根据自己的需求来构建不同的显示内容，本文主要根据上文《 [WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163) 》的js代码中主要的内容进行解析。







  * **参数 props **  
props相当于该自定义块的数据结构，包含了之前定义的 attributes 内的各属性值，也有创建的函数。 
  * **wp.element.createElement( )**  
这个与HTML的 `document.createElement( )` 函数相似，常见用法如 `wp.element.createElement( 'nodename', { className: 'classname' }, content）` 。nodename为元素名；classname为css类名，该部分可以添加各种属性值，如button的`onClick`事件等；content为内容，可以为 Document 对象或者空值等。需要在php中引入js文件的`array()`中添加 `'wp-element'` 。
  * **wp.editor.RichText **  
简单说是wp特有的文本编辑， 需要在php中引入js文件的`array()`中添加 `'wp-editor'` 。  
主要属性有：
    * value：内容
    * onChange：内容改变时调用的函数
    * placeholder：提示内容
    * multiline：每一行添加的标签名，可选
    * tagName：全部内容的标签名，可选 
  * **wp.element.Fragment  **  
使其子元素没有任何包装元素的组件。 
  * **wp.editor.BlockControls **  
当块的`edit`实现返回时，呈现图标按钮的工具栏。此部分可以阅读 [wordpress / editor ](https://developer.wordpress.org/block-editor/packages/packages-editor/)关于 BlockControls 的介绍。
  * **wp.editor.AlignmentToolbar **  
`AlignmentToolbar`需要为`BlockControls`元素的子元素，作为块的文本对齐的预配置组件。 








## 总结







自定义块想实现单一的样式功能并不困难，将想要的样式通过css导入，在js文件中将编辑内容save在一个带有你css相应类的标签中即可。想要实现复杂的样式功能，则需要块的扩展以及工具栏等自定义内容了。关于块扩展以及自定义工具栏可以阅读《 WordPress之Gutenberg（古腾堡）自定义块扩展栏》、《WordPress之Gutenberg（古腾堡）自定义块工具栏 》。









_**WordPress Gutenberg其他相关自定义系列文章：**_  
_1、_[WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163)  
_2、_[WordPress之Gutenberg（古腾堡）自定义块扩展栏](https://www.tidnotes.ga/?p=214)  
_3、[WordPress之Gutenberg（古腾堡）自定义块工具栏](https://www.tidnotes.ga/?p=238)_   




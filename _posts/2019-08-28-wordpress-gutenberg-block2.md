---
id: 208
title: WordPress之Gutenberg（古腾堡）自定义块（二）
date: 2019-08-28T03:56:20+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=208
permalink: /2019/08/wordpress-gutenberg-block2.html
categories:
  - WordPress使用技巧
tags:
  - Gutenberg（古腾堡）
  - WordPress
  - 自定义块
---
<blockquote class="wp-block-quote">
  <p>
    本文内容主要参考&nbsp;<a href="https://www.haibakeji.com/archives/author/1">海拔科技</a>&nbsp;以及&nbsp;<a rel="noreferrer noopener" href="https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/" target="_blank">Gutenberg 开发API</a>&nbsp;，介绍并解读新版WordPress所采用的&nbsp;<em>Gutenberg 编辑器</em>&nbsp;<em>（ Block Editor/块编辑器 ）</em>如何创建自定义编辑块，包括块的样式以及扩展工具栏等。
  </p>
  
  <cite> 本文适用于WordPress 5.22。关于WordPress Gutenberg自定义系列目录如下： <br /><em>1、</em><a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-block1.html">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-block2.html">WordPress之Gutenberg（古腾堡）自定义块（二）</a><br /><em>3、</em><a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-extension.html">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a><br /><em>4、<a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-toolbar.html">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em> </cite>
</blockquote>

本文内容主要根据  Gutenberg 开发API ，为上文《 <a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-block1.html" target="_blank" rel="noreferrer noopener" aria-label="（在新窗口打开）">WordPress之Gutenberg（古腾堡）自定义块（一）</a> 》中的js代码做解读，让大家更了解自定义的构建。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 基本结构 {.h2c}

利用<code class="language-js">wp.blocks.registerBlockType('namespace/block-name', {})</code>来构建一个新的自定义块，基本格式如下：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>blocks.registerBlockType('namespace/block-name', {
         title: '',
         category: ''
         icon: {},
         description: '',
         attributes: {},
         edit: function(props) {},
         save: function(props) {}
});</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

### 属性说明 {.h3c}

  * namespace/block-name：自定义块的名称，其中namespace是插件或主题的名称
  * title：自定义块显示名称
  * category：所在分类目录，可选为“ common 、formatting 、layout 、widgets 、embed&nbsp;”，对应分别是：常用区块、格式、布局元素、小工具、嵌入
  * icon：显示的图标
  * description：描述文字
  * attributes：自定义属性，用于保存属性值
  * edit：编辑时调用的函数，返回一个编辑时的html格式 
  * save：保存时调用的函数，返回一个最后呈现的html格式 

#### 图标（icon） {.h4c}

输入值为 String 或者 Object

当属性值为 String 时， 可以是任何[WordPress的Dashicons](https://developer.wordpress.org/resource/dashicons/)， 也可以是自定义svg元素。 

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>// Specifying a dashicon for the block
icon: 'book-alt',
 
// Specifying a custom svg for the block
icon: &lt;svg viewBox="0 0 24 24" xmlns="&lt;a href="http://www.w3.org/2000/svg"&gt;http://www.w3.org/2000/svg&lt;/a&gt;"&gt;&lt;path fill="none" d="M0 0h24v24H0V0z" /&gt;&lt;path d="M19 13H5v-2h14v2z" /&gt;&lt;/svg&gt;,</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

当属性值是Object时，如上所述，图标应该包含在src属性中。除了src之外，对象可以包含背景和前景色，例如： 

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>icon: {
     // 背景色
     background: '#7e70af',
     // 前景色
     foreground: '#fff',
     // 图标属性
     src: 'book-alt',
 } ,</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 属性（attributes）  {.h4c}

用attribute从标记中提取属性的值。最简单的一个例子如下：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>{
     url: {
         type: 'string',
     }
 } </code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

url就相当于一个字符变量，可以在自定义块中调用。在edit和save中，可以利用<code class="language-markup language-other">props.attributes.url</code>调用url值，利用<code class="language-markup language-other">props.setAttributes( { url: value } ); </code>设置url值。注意：type只能是 null 、 boolean 、 object 、 array 、 number 、 string 、 integer 。

作为提取属性的值，需要加入source（内容来源）和selector（过滤器）两个属性。这个根据不同的需要而相应改变，可以详细阅读 <a rel="noreferrer noopener" aria-label="Gutenberg 开发API ：Attributes（在新窗口打开）" href="https://developer.wordpress.org/block-editor/developers/block-api/block-attributes/" target="_blank">Gutenberg 开发API ：Attributes</a>。这里提供三个常用的例子。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>//例子1，提取块html中&lt;code&gt;标签内的内容到content中，返回值是字符串形式
content: {
     type: 'string',
     source: 'html',
     selector: 'code',
 },</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>//例子2，提取块中&lt;span&gt;标签内容到content中，返回值是数组形式
content: {
     type: 'array',
     source: 'children',
     selector: 'span',
 },</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>//例子3，提取包含类名为lan的类，用于提取某个标签的类。
typeClass: {
     source: 'attribute',
     selector: '.lan',
     attribute: 'class',
 },</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 函数 edit 和 save {.h4c}

edit 函数在编辑器的上下文中描述块的结构，显示编辑器在使用块时将呈现的内容。save函数定义了将不同属性组合到最终标记中的方式，表示块在网站前面的显示方式。 所以函数返回内容都应该是标准的HTML格式。如：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-php"><code>edit: function() {
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
 }</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

这个需要根据自己的需求来构建不同的显示内容，本文主要根据上文《 [WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/2019/08/wordpress-gutenberg-block1.html) 》的js代码中主要的内容进行解析。

  * **参数 props**  
    props相当于该自定义块的数据结构，包含了之前定义的 attributes 内的各属性值，也有创建的函数。 
  * **wp.element.createElement( )**  
    这个与HTML的 <code class="language-js">document.createElement( )</code> 函数相似，常见用法如 <code class="language-js">wp.element.createElement( 'nodename', { className: 'classname' }, content）</code> 。nodename为元素名；classname为css类名，该部分可以添加各种属性值，如button的<code class="language-js">onClick</code>事件等；content为内容，可以为 Document 对象或者空值等。需要在php中引入js文件的<code class="language-js">array()</code>中添加 <code class="language-js">'wp-element'</code> 。
  * **wp.editor.RichText**  
    简单说是wp特有的文本编辑， 需要在php中引入js文件的<code class="language-js">array()</code>中添加 <code class="language-js">'wp-editor'</code> 。  
    主要属性有：
      * value：内容
      * onChange：内容改变时调用的函数
      * placeholder：提示内容
      * multiline：每一行添加的标签名，可选
      * tagName：全部内容的标签名，可选 
  * **wp.element.Fragment**  
    使其子元素没有任何包装元素的组件。 
  * **wp.editor.BlockControls**  
    当块的<code class="language-js">edit</code>实现返回时，呈现图标按钮的工具栏。此部分可以阅读 [wordpress / editor](https://developer.wordpress.org/block-editor/packages/packages-editor/) 关于 BlockControls 的介绍。
  * **wp.editor.AlignmentToolbar**  
    <code class="language-js">AlignmentToolbar</code>需要为<code class="language-js">BlockControls</code>元素的子元素，作为块的文本对齐的预配置组件。 

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

## 总结 {.h2c}

自定义块想实现单一的样式功能并不困难，将想要的样式通过css导入，在js文件中将编辑内容save在一个带有你css相应类的标签中即可。想要实现复杂的样式功能，则需要块的扩展以及工具栏等自定义内容了。关于块扩展以及自定义工具栏可以阅读《 [WordPress之Gutenberg（古腾堡）自定义块扩展栏](https://www.tidnotes.ga/2019/08/wordpress-gutenberg-extension.html)》、《[WordPress之Gutenberg（古腾堡）自定义块工具栏](https://www.tidnotes.ga/2019/08/wordpress-gutenberg-toolbar.html) 》。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer">
</div>

<p class="has-small-font-size h5c">
  <em><strong>WordPress Gutenberg其他相关自定义系列文章：</strong></em><br /><em>1、</em><a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-block1.html">WordPress之Gutenberg（古腾堡）自定义块（一）</a><br /><em>2、</em><a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-extension.html">WordPress之Gutenberg（古腾堡）自定义块扩展栏</a><br /><em>3、<a href="https://www.tidnotes.ga/2019/08/wordpress-gutenberg-toolbar.html">WordPress之Gutenberg（古腾堡）自定义块工具栏</a></em>
</p>
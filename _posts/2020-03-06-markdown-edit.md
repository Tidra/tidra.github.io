---
id: 548
title: Markdown基本语法
date: 2020-03-06T03:04:23+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=548
permalink: /2020/03/markdown-edit.html
image: /wp-content/uploads/2020/03/image-1.png
categories:
  - 工具
tags:
  - GitHub
  - Markdown
  - 语法
---
最近写GitHub上的README.md文件，要用到Markdown语法，所以本文总结一下用于写 <code class="language-markup">.md</code>，<code class="language-markup">.markdown</code> 结尾的文档的基本语法。

网上有不少在线的Markdown编辑器，本人一般用GitHub直接编写然后在线预览，或者用UltraEdit编辑器实时预览。

## 目录

  * **<a href="#标题" rel="nofollow" >标题</a>**
  * **<a href="#格式" rel="nofollow" >格式</a>**
      * <a href="#换行" rel="nofollow" >换行</a>、<a href="#字体" rel="nofollow" >字体</a>、<a href="#分割线" rel="nofollow" >分割线</a>、<a href="#删除线" rel="nofollow" >删除线</a>、<a href="#下划线" rel="nofollow" >下划线</a>
  * **<a href="#列表" rel="nofollow" >列表</a>**、**<a href="#引用" rel="nofollow" >区块（引用）</a>**
  * **<a href="#代码" rel="nofollow" >代码</a>**
  * **<a href="#链接" rel="nofollow" >链接</a>**、**<a href="#图片" rel="nofollow" >图片</a>**
  * **<a href="#表格" rel="nofollow" >表格</a>**
  * **<a href="#兼容" rel="nofollow" >兼容</a>**

## 标题 {#标题}

可以用<code class="language-markup">=</code>标记一级标题、<code class="language-markup">-</code> 标记二级标题，或者用<code class="language-markup">#</code> 标记各级标题（符号后有空格）。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>一级标题
=================
二级标题
-----------------

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/5b83b91b-0a58-4202-99f0-b85de368b993" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-1.png" alt=" Markdown 标题" class="wp-image-577" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-1.png 635w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-1-300x213.png 300w" sizes="(max-width: 635px) 100vw, 635px" /></a><figcaption> Markdown 标题</figcaption></figure>
</div>

## 格式 {#格式}

### 换行 {#换行}

**两个以上空格加上回车**，或者在段落后面使用一个空行来表示重新开始一个段落。 具体可以看下下面的演示图。

### 字体 {#字体}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>*斜体文本*
_斜体文本_

**粗体文本**
__粗体文本__

***粗斜体文本***
___粗斜体文本___</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-2.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-2.png" alt="Markdown 字体" class="wp-image-578" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-2.png 601w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-2-300x57.png 300w" sizes="(max-width: 601px) 100vw, 601px" /></a><figcaption>Markdown 字体</figcaption></figure>
</div>

### 分隔线 {#分割线}

在一行中用三个以上的星号、减号、底线来建立一个分隔线

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>***
* * *
*****

- - -
----------

_ _ _
___</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 删除线 {#删除线}

在文字的两端加上两个波浪线 <code class="language-markup">~~</code> 即可，部分编辑器单个波浪线也可。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>~删除线~
~~删除线~~</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 下划线 {#下划线}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>&lt;u&gt;下划线&lt;/u&gt;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 列表 {#列表}

**无序列表**使用星号(<code class="language-markup">*</code>)、加号(<code class="language-markup">+</code>)或是减号(<code class="language-markup">-</code>)作为列表标记，**有序列表**使用数字并加上 <code class="language-markup">.</code> 号来表示。注意符号后有空格，可嵌套使用。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>* 第一项
* 第二项
+ 第一项
+ 第二项
- 第一项
- 第二项

1. 第一项
2. 第二项
3. 第三项

嵌套
1. 第一层
	- 第二层
		* 第三层
2. 第一层
	+ 第二层
		1. 第三层</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-3.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-3.png" alt="Markdown 列表" class="wp-image-579" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-3.png 578w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-3-300x258.png 300w" sizes="(max-width: 578px) 100vw, 578px" /></a><figcaption>Markdown 列表</figcaption></figure>
</div>

## 区块（引用） {#引用}

区块引用是在段落开头使用 <code class="language-markup">></code> 符号 ，然后后面紧跟一个**空格**。注意换行使用两空格和直接空行的区别。区块也可以嵌套使用，也可以和列表混合嵌套。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>&gt; 区块引用
&gt; 第一行后没用两空格的内容  
&gt; 第二行用了两空格用于换行
&gt; 
&gt; 上一行行空行效果

&gt; 最外层
&gt; &gt; 第一层嵌套
&gt; &gt; &gt; 第二层嵌套

&gt; 区块中使用列表
&gt; 1. 第一项
&gt; 2. 第二项
&gt; + 第一项
&gt; 	&gt; 引用  
&gt;   &gt; 内容
&gt; + 第二项</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-4.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-4.png" alt="Markdown 区块引用" class="wp-image-580" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-4.png 594w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-4-300x232.png 300w" sizes="(max-width: 594px) 100vw, 594px" /></a><figcaption>Markdown 区块引用</figcaption></figure>
</div>

## 代码 {#代码}

段落上的一个函数或片段的代码可以用反引号把它包起来（<code class="language-markup">`</code>）。代码区块使用 **4 个空格**或者一个**制表符（Tab 键）**，或者用 <code class="language-markup">```</code> 包裹一段代码，并指定一种语言（也可以不指定）。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>`printf()` 函数

## 代码区块

    function a() {
       retrun 0;
    }

```javascript
$(document).ready(function () {
    alert('Hi!');
});
```</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-5.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-5.png" alt="Markdown 代码" class="wp-image-581" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-5.png 622w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-5-300x157.png 300w" sizes="(max-width: 622px) 100vw, 622px" /></a><figcaption>Markdown 代码</figcaption></figure>
</div>

## 链接 {#链接}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>[链接名称](链接地址)

&lt;链接地址&gt;
&lt;https://www.tidnotes.ga&gt;

这个链接用 1 作为网址变量: [Google][1]  
这个链接用 tidnotes 作为网址变量: [TiD][tidnotes]  
然后在文档的结尾为变量赋值（网址）

[1]: https://www.google.com/
[tidnotes]: https://www.tidnotes.com/</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-6.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-6.png" alt="Markdown 链接" class="wp-image-582" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-6.png 521w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-6-300x98.png 300w" sizes="(max-width: 521px) 100vw, 521px" /></a><figcaption>Markdown 链接</figcaption></figure>
</div>

## 图片 {#图片}

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-8.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-8.png" alt="Markdown 图片" class="wp-image-585" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-8.png 425w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-8-300x80.png 300w" sizes="(max-width: 425px) 100vw, 425px" /></a><figcaption>Markdown 图片</figcaption></figure>
</div>

Markdown不能定义图片大小，可以用<code class="language-markup">&lt;img&gt;</code>标签来插入图片。

## 表格 {#表格}

使用 <code class="language-markup">|</code>来分隔不同的单元格，使用 <code class="language-markup">-</code> 来分隔表头和其他行。

  * <code class="language-markup">&lt;strong>-:&lt;/strong> </code>设置内容和标题栏居右对齐。
  * <code class="language-markup">&lt;strong>:-&lt;/strong> </code>设置内容和标题栏居左对齐。
  * <code class="language-markup">&lt;strong>:-:&lt;/strong> </code>设置内容和标题栏居中对齐。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-md"><code>|  表头   | 表头   |
|  -----  | ------ |
| 单元格  | 单元格 |
| 单元格  | 单元格 |

| 对齐方式：左对齐 | 对齐方式：右对齐 | 对齐方式：居中对齐 |
| :----- | -----: | :------: |
| 单元格 | 单元格 | 单元格   |
| 单元格 | 单元格 | 单元格   |</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large"><a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-9.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-9.png" alt="Markdown 表格" class="wp-image-586" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/image-9.png 538w, https://www.tidnotes.ga/wp-content/uploads/2020/03/image-9-300x142.png 300w" sizes="(max-width: 538px) 100vw, 538px" /></a><figcaption>Markdown 表格</figcaption></figure>
</div>

## 兼容 {#兼容}

Markdown是支持HTML的，想要更好的显示效果可以使用HTML的写法来编辑文本。
---
id: 391
title: '[JS]RGB色与Hex色互换代码'
date: 2019-11-17T14:59:47+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=391
permalink: /2019/11/js-rgb-hex-exchange.html
categories:
  - JavaScript
  - 前端
  - 工具
tags:
  - hex
  - JavaScript
  - rgb
  - 颜色
---
<blockquote class="wp-block-quote">
  <p>
    本文主要介绍用Javascript实现RGB三原色与Hex十六进制色互转的思路以及编写代码。
  </p>
  
  <cite>在线<a href="https://www.tidnotes.ga/color">颜色表、颜色选择器、RGB和Hex互转</a>链接：<br /><a href="https://www.tidnotes.ga/color">https://www.tidnotes.ga/color</a></cite>
</blockquote>

RGB三原色与Hex十六进制色基本就是十进制数和十六进制数的不同表达形式，所以在处理两者转换的方法可以简单的认为是进制的转换问题。

进制转换有不少的方法，本文采取js的简单的转换方法。

<!--more-->

## 转换思路

  1. 取得rgb或hex的十进制数或十六进制数。
  2. 将十进制数和十六进制数互换。
  3. 将互换后的结果加上rgb或hex的特有标识。

想取rgb或hex的十进制数或十六进制数，可以利用正则的方法获取；或者直接利用两者的特点，根据分割特点来读取相应的数即可。

## 代码

### rgb色转hex色部分

利用<code class="language-js">match()</code>方法，读取出rgb的数字部分（<code class="language-js">/\d+/g</code> 是正则里取所有连着的数字）；然后将十进制数换算为十六进制的字符，不足两位则补零；最后输出“#xxxxxx”的hex形式。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-js"><code>function rgb2hex(rgb) {
    var rgb = rgb.match(/\d+/g);
    function hex(x) { return ("0" + parseInt(x).toString(16)).slice(-2); }
    return rgb = "#" + hex(rgb[0]) + hex(rgb[1]) + hex(rgb[2]);
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### hex色转rgb色部分

同样利用<code class="language-js">match()</code>方法，<code class="language-js">/[\d\w]{2}/g</code> 是取两个两个的字母或数字的任意组合，排除符号；然后将十六进制换算为十进制；最后输出“rgb(xxx,xxx,xxx)”的rgb形式。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers language-js"><code>function hex2rgb(hex) {
    var hex = hex.match(/[\d\w]{2}/g);
    function rgb(x) { return parseInt(x, 16); }
    return hex = "rgb(" + rgb(hex[0]) + "," + rgb(hex[1]) + "," + rgb(hex[2]) + ")";
}</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 最后

本文中，进制数的转换主要用了<code class="language-js">parseInt()</code>和<code class="language-js">toString()</code>两个方法完成的，同样适合其他进制的转换，这是我觉得最为简单的方法。本文rgb色和hex色的互换是分为两个函数来写，如果想要自动识别然后互转的话，可以自行将上面两个函数组合起来。还有什么疑问可以在下方留言，本人会在能力之下进行解答。
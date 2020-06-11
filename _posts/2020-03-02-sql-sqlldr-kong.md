---
id: 542
title: '[SQL]ORACLE中SQLLDR关于空格的问题'
date: 2020-03-02T16:12:37+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=542
permalink: /2020/03/sql-sqlldr-kong.html
categories:
  - SQL
tags:
  - oracle
  - sql
  - sqlldr
---
<blockquote class="wp-block-quote">
  <p>
    关于Oracle中使用SQLLDR有时候会出现关于空格保留或去除的问题，就这个问题的解决方案有不少，但如果是由于参数设置问题，可能就本文所说的问题解决。
  </p>
  
  <cite>参考文章： <a href="http://blog.sina.com.cn/s/blog_701218960100l0gt.html" rel="nofollow" >http://blog.sina.com.cn/s/blog_701218960100l0gt.html</a> </cite>
</blockquote>

使用SQLLDR加载入库，一般就使用分隔符取值或者定长取值。使用**分隔符取值**时，空格是会保留的，而使用**定长取值**的时候就会自动去除空格（本文所说空格指内容前后的空格，不包括文字中的空格）。

<!--more-->

## 关于参数“**PRESERVE BLANKS**”

SQLLDR中有一个参数“**PRESERVE BLANKS**”，用于控制定长时的空格保留。

<p style="color:#0577a7" class="has-text-color">
  当 <em><strong>input file</strong> </em>是分隔符时，<strong><em>control file</em></strong> 中的 <strong><em>PRESERVE BLANKS</em></strong> 无效；<br />当 <em><strong>input file</strong> </em>是定长时，<strong><em>control file</em> </strong>中的 <strong><em>PRESERVE BLANKS </em></strong>有效。
</p>

所以，**定长取值**时，可以加 **PRESERVE BLANKS** 这个参数，_保留空格入库_。

可以在 **TRUNCATE INTO TABLE** 中加入该参数，全部字段都保留空格，如：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers language-sql"><code>LOAD DATA 
CHARACTERSET 'UTF8'
INFILE '/home/a.dat' 
TRUNCATE PRESERVE BLANKS INTO TABLE A
(
a POSITION(1:5), 
b POSITION(6:11), 
d POSITION(12:13) 
)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

也可以在字段后加如该参数，只保留该字段空格，如：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers language-sql"><code>LOAD DATA 
INFILE '/home/a.dat' 
TRUNCATE INTO TABLE A
 (
 a POSITION(1:5), 
 b POSITION(6:11)  PRESERVE BLANKS , 
 d POSITION(12:13) 
 )</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 利用trim()去除空格

定长取值默认是自动去除空格的，而分隔符取值则会保留空格入库。所以，去除空格可以利用<code class="language-js">trim()</code>函数。如：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers language-sql"><code>LOAD DATA 
CHARACTERSET 'UTF8'
INFILE '/home/a.txt' 
TRUNCATE INTO TABLE A
FIELDS TERMINATED BY '|'
(
a "trim(:a)", 
b "trim(:b)", 
d "trim(:d)"
)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 总结

对于SQLLDR保留或去除空格，可以分按如下操作：

  * **定长：**
      * 保留：加入参数 **PRESERVE BLANKS**
      * 去除：默认去除，无需操作
  * **分隔符：**
      * 保留：默认保留
      * 去除：使用<code class="language-js">trim()</code>函数
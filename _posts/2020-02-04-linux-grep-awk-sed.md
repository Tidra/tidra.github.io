---
id: 502
title: '[Linux]关于grep、awk、sed命令'
date: 2020-02-04T22:31:15+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=502
permalink: /2020/02/linux-grep-awk-sed.html
categories:
  - Linux
tags:
  - awk
  - grep
  - linux
  - sed
  - shell
---
<blockquote class="wp-block-quote">
  <p>
    对于一些文件字段或文件名等截取或重命名等操作，我们一般会用到正则等方法实现，Linux中的<a href="#grep">grep</a>、<a href="#awk">awk</a>、<a href="#sed">sed</a>命令同样能得到上述的效果，本文主要是介绍这三者的区别和用法。
  </p>
  
  <cite>本文参考文章：<a href="https://blog.csdn.net/song_aq/article/details/78527571">linux命令小记（grep、awk、sed）</a></cite>
</blockquote>

## grep命令 {#grep}

**grep**（global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。

<!--more 阅读更多-->

### 常用选项

  * **-c** 计算匹配的列数。
  * **-C<显示列数>或-<显示列数>** 除了显示匹配的那一列之外，并显示该列之前后的内容。
  * **-d<进行动作>** 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作。
  * **-e<范本样式>** 指定字符串作为查找文件内容的范本样式。
  * **-E** 将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式。
  * **-f<范本文件>** 指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每一列的范本样式。
  * **-F** 将范本样式视为固定字符串的列表。
  * **-h** 在显示匹配的那一列之前，不标示该列所属的文件名称。
  * **-H** 在显示匹配的那一列之前，标示该列的文件名称。
  * **-i** 忽略字符大小写的差别。
  * **-l** 列出文件内容匹配的文件名称。
  * **-L** 列出文件内容不匹配的文件名称。
  * **-n** 在显示匹配的那一列之前，标示出该列的编号。
  * **-q** 不显示任何信息。
  * **-R/-r** 此参数的效果和指定“-d recurse”参数相同。
  * **-s** 不显示错误信息。
  * **-v** 反转查找。
  * **-y** 此参数效果跟“-i”相同。
  * **-o** 只输出文件中匹配到的部分。

**补充：[egrep](https://man.linuxde.net/egrep)命令**用于在文件内查找指定的字符串，egrep执行效果与<code class="language-shell">grep -E</code>相似。**[fgrep](https://man.linuxde.net/fgrep)命令**和<code class="language-shell">grep -F</code>命令是一样的，但出错和用法消息不同，-s 标志功能也不同。

### 常见用法

在文件中搜索一个单词，命令会返回一个包含**“match_pattern”**的文本行： 

<div class="" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-shell"><code>grep match_pattern file_name
grep "match_pattern" file_name

# 多文件查找
grep "match_pattern" file_1 file_2 file_3 ...

# 标记匹配颜色
grep "match_pattern" file_name --color=auto</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

使用正则匹配：

<div class="" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-shell"><code>grep -E "[1-9]+"
egrep "[1-9]+"

# 只输出文件中匹配到的部分
echo this is a test line. | grep -o -E "[a-z]+\."
echo this is a test line. | egrep -o "[a-z]+\."
&gt; line.

# 忽略大小写
echo "hello world" | grep -i "HELLO"
>hello</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

多个匹配样式：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>echo this is a text line | grep -e "is" -e "line" -o
>is
>line

# 也可以使用-f选项来匹配多个样式，在样式文件中逐行写出需要匹配的字符。
cat patfile
>aaa
>bbb

echo aaa bbb ccc ddd eee | grep -f patfile -o
>aaa
>bbb</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

在多级目录中对文本进行递归搜索：

<div class="" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-shell"><code># .表示当前目录
grep "text" . -r -n

#只在目录中所有的.php和.html文件中递归搜索字符"main()"
grep "main()" . -r --include *.{php,html}

#在搜索结果中排除所有README文件
grep "main()" . -r --exclude "README"

#在搜索结果中排除filelist文件列表里的文件
grep "main()" . -r --exclude-from filelist</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## awk命令 {#awk}

**[awk](https://man.linuxde.net/awk)**是一种编程语言，用于在linux/unix下对文本和数据进行处理。数据可以来自标准输入(stdin)、一个或多个文件，或其它命令的输出。它支持用户自定义函数和动态正则表达式等先进功能，是linux/unix下的一个强大编程工具。

### 常用命令和选项

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>awk [options] 'script' var=value file(s)
awk [options] -f scriptfile var=value file(s)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 选项

  * **-F fs：**fs指定输入分隔符，fs可以是字符串或正则表达式，如-F:。
  * **-v var=value：**赋值一个用户定义变量，将外部变量传递给awk。
  * **-f scripfile：**从脚本文件中读取awk命令。
  * **-m[fr] val：**对val值设置内在限制，-mf选项限制分配给val的最大块数目；-mr选项限制记录的最大数目。这两个功能是Bell实验室版awk的扩展功能，在标准awk中不适用。

#### awk内置变量（预定义变量）

<div class="" style="position: relative;">
  <pre class="line-numbers language-javascript"><code>$n 当前记录的第n个字段，比如n为1表示第一个字段，n为2表示第二个字段。 
$0 这个变量包含执行过程中当前行的文本内容。
ARGC 命令行参数的数目。
ARGV 包含命令行参数的数组。
FILENAME 当前输入文件的名。
FS 字段分隔符（默认是任何空格）。
NF 表示字段数，在执行过程中对应于当前的字段数。
NR 表示记录数，在执行过程中对应于当前的行号。
OFMT 数字的输出格式（默认值是%.6g）。
OFS 输出字段分隔符（默认值是一个空格）。
ORS 输出记录分隔符（默认值是一个换行符）。
RS 记录分隔符（默认是一个换行符）。</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 简单用法

打印每一行的第二、第三和最后一个字段：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>awk '{ print $2,$3,$NF }' filename</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

打印第一行：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>awk 'NR==1{print}' filename</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

统计文件中的行数：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>awk 'END{ print NR }' filename</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

指定分隔符：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>echo 111__222__333 | awk 'BEGIN{FS="__"}{print $1}'
echo 111__222__333 | awk -F "__" '{print $1}'
>111</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

匹配：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code># 输出正则匹配"match_pattern"的一行
awk '/match_pattern/' filename

# 输出正则匹配第二个字段的行
awk '{if($2~/^80$/)print}' filename

# 输出正则不匹配第二个字段的行
awk '{if($2!~/^80$/)print}' filename

# 输出第二个字段为"match_pattern"的行
awk '{if($2=="match_pattern")print}' filename</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## sed命令 {#sed}

[sed](https://man.linuxde.net/sed)操作的是一个输入文件在内存的一个副本，对副本内容进行编辑活动，如果没有重定向到一个文件，会将文件修改的结果输出到屏幕。和[awk](#awk)一样，不会修改输入文件的内容。

### 基本命令和选项

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>sed [options] 'command' file(s)
sed [options] -f scriptfile file(s)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 选项

  * **-e<script>或&#8211;expression=<script>：**以选项中的指定的script来处理输入的文本文件；
  * **-f<script文件>或&#8211;file=<script文件>：**以选项中指定的script文件来处理输入的文本文件； 
  * **-h或&#8211;help：**显示帮助；
  * **-n或&#8211;quiet或&#8211;silent：**仅显示script处理后的结果； 
  * **-V或&#8211;version：**显示版本信息。

#### 命令

  * **a\** 在当前行下面插入文本。
  * **i\** 在当前行上面插入文本。 
  * **c\** 把选定的行改为新的文本。 
  * **d** 删除，删除选择的行。 
  * **s** 替换指定字符。
  * **p** 打印模板块的行。
  * **r file** 从file中读行。
  * **w file** 写并追加模板块到file末尾。 
  * **!** 表示后面的命令对所有没有被选定的行发生作用。
  * **=** 打印当前行号码。

#### 替换标记 

  * **g** 表示行内全面替换。 
  * **p** 表示打印行。 
  * **w** 表示把行写入一个文件。 
  * **x** 表示互换模板块中的文本和缓冲区中的文本。 
  * **y** 表示把一个字符翻译为另外的字符（但是不用于正则表达式）。 
  * **\n** 第n个匹配字符串。
  * **&** 已匹配所有字符串。

#### 元字符集 

  * **^** 匹配行开始，如：/^sed/匹配所有以sed开头的行。
  * **$** 匹配行结束，如：/sed$/匹配所有以sed结尾的行。 
  * **.** 匹配一个非换行符的任意字符，如：/s.d/匹配s后接一个任意字符，最后是d。 
  * ***** 匹配0个或多个字符，如：/*sed/匹配所有模板是一个或多个空格后紧跟sed的行。 
  * **[]** 匹配一个指定范围内的字符，如/[<a rel="noreferrer noopener" href="http://man.linuxde.net/ss" target="_blank">ss</a>]<a rel="noreferrer noopener" href="http://man.linuxde.net/ed" target="_blank">ed</a>/匹配sed和Sed。 
  * **[^]** 匹配一个不在指定范围内的字符，如：/[^A-RT-Z]ed/匹配不包含A-R和T-Z的一个字母开头，紧跟ed的行。 
  * **\(..\)** 匹配子串，保存匹配的字符，如s/\(love\)able/\1rs，loveable被替换成lovers。 
  * **&** 保存搜索字符用来替换其他字符，如s/love/\*\*&\*\*/，love这成\*\*love\*\*。 
  * **\<** 匹配单词的开始，如:/\<love/匹配包含以love开头的单词的行。 
  * **\>** 匹配单词的结束，如/love\>/匹配包含以love结尾的单词的行。 
  * **x\{m\}** 重复字符x，m次，如：/0\{5\}/匹配包含5个0的行。
  * **x\{m,\}** 重复字符x，至少m次，如：/0\{5,\}/匹配至少有5个0的行。 
  * **x\{m,n\}** 重复字符x，至少m次，不多于n次，如：/0\{5,10\}/匹配5~10个0的行。

### 常用用法

替换文本中的字符串：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code>sed 's/book/books/' file

# -n选项和p命令一起使用表示只打印那些发生替换的行
sed -n 's/test/TEST/p' file

# 直接编辑文件选项-i，会匹配file文件中每一行的第一个book替换为books
sed -i 's/book/books/g' file

# 当需要从第N处匹配开始替换时，可以使用 /Ng
echo sksksksksksk | sed 's/sk/SK/3g'
>skskSKSKSKSK</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

删除操作：

<div class="" style="position: relative;">
  <pre class="line-numbers language-shell"><code># 删除空白行
sed '/^$/d' file

# 删除文件的第2行
sed '2d' file

# 删除文件的第2行到末尾所有行
sed '2,$d' file</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 最后

如果只是过滤文本，可使用grep，其效率要比其他的高很多。sed默认只处理模式空间，不处理原数据，如果你处理的数据是针对行处理的，可以使用sed。如果对处理的数据需要生成报告之类的信息，或者你处理的数据是按列进行处理的，最好使用awk。
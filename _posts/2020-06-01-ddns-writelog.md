---
id: 624
title: 关于DDNS日志输出中文问题
date: 2020-06-01T01:41:14+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=624
permalink: /2020/06/ddns-writelog.html
categories:
  - Linux
  - 工具
tags:
  - ddns
  - linux
  - openwrt
  - urlencode
  - write_log
---
最近在使用OpenWrt的DDNS发现，如果使用write\_log来实现日志输出，中文不会显示出来，会出现格式错误。对dynamic\_dns\_functions.sh的源代码进行细读发现，write\_log函数会调用urlencode函数，而该函数是不支持中文的。

对该函数改为支持中文的URL编码即可，将<code class="language-bash" id="{&x&:794.09375,&y&:382,&width&:114.359375,&height&:19,&top&:382,&right&:908.453125,&bottom&:401,&left&:794.09375}">urlencode(){}</code>改写代码如下：  
_<span class="has-inline-color has-vivid-cyan-blue-color">注：dynamic_dns_functions.sh文件地址一般为 /usr/lib/ddns/</span>_

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">urlencode() {
local __ENC
[ $# -ne 2 ] && write_log 12 "Error calling 'urlencode()' - wrong number of parameters"
__ENC=$(echo "$2" | awk 'BEGIN {
        split ("1 2 3 4 5 6 7 8 9 A B C D E F", hextab, " ")
        hextab [0] = 0
        for (i=1; i&lt;=255; ++i) {
            ord [ sprintf ("%c", i) "" ] = i + 0
        }
    }
    {
        encoded = ""
        for (i=1; i&lt;=length($0); ++i) {
            c = substr ($0, i, 1)
            if ( c ~ /[a-zA-Z0-9.-]/ ) {
                encoded = encoded c             # safe character
            } else if ( c == " " ) {
                encoded = encoded "+"   # special handling
            } else {
                # unsafe character, encode it as a two-digit hex-number
                lo = ord [c] % 16
                hi = int (ord [c] / 16);
                encoded = encoded "%" hextab [hi] hextab [lo]
            }
        }
        print encoded
    }')
eval "$1=\"$__ENC\""
return 0
}</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

## 其他方法

除了改URL编码原函数外，其实可以更改write_log函数，可以看到函数里有下面一段代码（可以直接所搜关键代码跳到对应位置）。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">if [ -n "$password" ]; then
urlencode __MSE "$__MSG"
__MSG=$( echo -e "$__MSE" \
| sed -e "s/$URL_PASS/***PW***/g" \
|sed -e "s/+/ /g; s/%00/\n/g; s/%/\\\\x/g" | xargs -0 printf "%b") 
fi</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

该部分代码主要是将密码隐藏掉，其中有一部分使用了URL编码，如果确认你使用的ddns没有使用到特殊符号的url地址，可以将这部分改为以下代码：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">if [ -n "$password" ]; then
__MSG=$( echo -e "$__MSE" \
| sed -e "s/$URL_PASS/***PW***/g") 
fi</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>
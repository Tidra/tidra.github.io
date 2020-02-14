---
id: 436
title: '[Linux]shell脚本实现ftp/sftp上传下载总结'
date: 2020-01-05T21:25:38+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=436
permalink: /2020/01/linux-shell-ftp.html
categories:
  - Linux
tags:
  - ftp
  - linux
  - sftp
  - shell
---
最近在使用shell脚本时，需要使用到ftp进行上传和下载，趁最近一段时间还算有空，总结一下ftp和sftp的一些Linux命令和利用shell脚本实现ftp和sftp批量上传下载的方法。

<!--more-->

## FTP和SFTP区别

**在linux系统中，最常见的文件传输的方式莫过于ftp和sftp了。** 

<p style="color:#068cda;font-size:19px" class="has-text-color">
  <strong>FTP（File Transfer Protocol），即文件传输协议，用于Internet上控制文件的双向传输。</strong>
</p>

FTP在linux系统中，传输默认的端口为21端口，通常以ASCII码和二进制的方式传输数据，支持主动模式和被动模式两种方式。

<p style="color:#068cda;font-size:19px" class="has-text-color">
  <strong>SFTP（Secure File Transfer Protocol），即文件加密传输协议</strong>。
</p>

SFTP在linux系统中，传输默认的端口为22端口，这种传输方式更为安全，传输双方既要进行密码安全验证，还要进行基于密钥的安全验证，有效的防止了“中间人”的威胁和攻击。

**两个比较起来，ftp传输会比sftp传输速率快，毕竟sftp牺牲了一定的效率，以保证传输过程的安全。**

## FTP常用命令

#### 1.初始或连接 &#8211; ftp {#ftp}

<div class="" style="position: relative;">
  <pre class="language-shell"><code>ftp [-pinegvtd] [Host]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

<p style="font-size:18px">
  <strong>参数：</strong>
</p>

  * **-p ：**启用被动模式。
  * **-i&nbsp;：**传送多个文件时禁用交互提示。&nbsp;
  * **-n&nbsp;：**在建立初始连接后禁止自动登录功能。&nbsp;
  * **-e ：**禁用行读取。
  * **-g&nbsp;：**禁用文件名组合。Glob 允许使用星号 (*) 和问号 (?) 作为本地文件和路径名的通配符字符。
  * **-v&nbsp;：**详细模式，显示指令执行过程。
  * **-t ：**启用数据包跟踪。
  * **-d&nbsp;：**启用调试、显示在&nbsp;**FTP**&nbsp;客户端和&nbsp;**FTP**&nbsp;服务器之间传递的所有**命令**。&nbsp; 
  * **Host&nbsp;：**指定要连接的计算机名、IP 地址或 IPv6 地址。如果指定了主机名或地址，则其必须是**命令**行的最后一个参数。

**注意：**该命令为 0.17 版本的 ftp 命令，不同版本间有细微的差异，其中 **[-dignv]** 5个命令为通用命令，各版本一致。具体可以使用 <code class="language-shell">ftp -help</code> 这一命令查看。

**提示：**部分版本会用 **[-A]** 命令，如果出现 “**connect: 没有到主机的路由**”这一问题，可以使用 **[-A]** 命令解决。

#### 2. 连接FTP &#8211; open

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; open Host [port]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数** **：** port为端口号，Host同上。

如果使用上述“**[ftp](#ftp)**”命令时已经加上Host参数则不需要再使用该命令。

#### 3.登录用户 &#8211; user

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; user username [password] [account]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：**

  * **username ：**用户名。
  * **password ：**username 的密码。如果没有填写，但必须填写，ftp 会提示输入密码。
  * **account ：**登录到远程计算机所使用的帐户。如果没有填写account，但是需要填写，ftp 会提示您输入帐户。 

#### 4.结束 &#8211; close/disconnect/bye/!/quit

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; close
FTP &gt; disconnect
FTP &gt; bye
FTP &gt; by
FTP &gt; !
FTP &gt; quit</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

close 和 disconnect，只结束与远程服务器的 FTP 会话，还留在 FTP 程序内。bye（或 by）、！、quit，关闭 FTP 对话并退出 FTP。

#### 5.编码 &#8211; ascii/binary

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; ascii
FTP &gt; binary
FTP &gt; bi</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

FTP 支持两种文件传送类型，ASCII 码和二进制码（binary 或 bi）。 

#### 6.更改目录 &#8211; cd/cdup/lcd {#cd}

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; cd remote-dir
FTP &gt; cdup
FTP &gt; lcd [directory]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

  * **cd ：**更改的远程计算机上的目录，跳转到 remote-dir 这个目录 。
  * **cdup ：**更改的远程计算机上的目录，跳到上一层目录。
  * **lcd ：**更改本地计算机上的目录为 directory。如果没有填写 directory，将显示本地计算机中当前的工作目录。 

#### 7.上传 &#8211; send/put/mput

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; send local-file [remote-file]
FTP &gt; put local-file [remote-file]
FTP &gt; mput local-files</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：** 

  * **local-file(s) ：**复制的本地文件。
  * **remote-file ：**在远程计算机上使用的名称。如果没有，文件将命名为 local-file。 

send 和 put 是上传单个文件，mput 是上传多个文件。

#### 8.下载 &#8211; get/mget/reget/recv

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; get remote-file [local-file]
FTP &gt; recv remote-file [local-file]
FTP &gt; reget remote-file [local-file]
FTP &gt; mget remote-files</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：**

  * **remote-file(s) ：**复制的远程文件。
  * **local-file ：**在本地计算机上使用的名称。如果没有，文件将命名为 remote-file。 

get 和 recv 一样，下载单个文件，reget 类似 get，但若 local-file 存在，则从上次传输中断处续传。mget 则下载多个文件。

#### 9.帮助 &#8211; ?/help

<div class="" style="position: relative;">
  <pre class="language-shell"><code>FTP &gt; ? [command]
FTP &gt; help [command]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：**command 是需要帮助的命令的名称。如果没有，ftp 将显示全部远程命令的列表。

## SFTP常用命令

#### 1.连接登录SFTP &#8211; sftp {#sftp}

<div class="" style="position: relative;">
  <pre class="language-shell"><code>sftp [user@]host</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：**user 是登录的用户名；host 是远程的ip地址。

执行上面的命令后， linux shell 会提示用户输入密码， 输入password后就可以成功建立 sftp 连接。 

#### 2.帮助 &#8211; help

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; help</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

#### 3.查看当前目录 &#8211; pwd/lpwd

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; pwd
SFTP &gt; lpwd</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

pwd 是查看远端服务器的目录， 即 sftp 服务器默认的当前目录。lpwd 是看本地目录。

#### 4.显示目录文件和子目录的缩写列表 &#8211; ls/lls

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; ls
SFTP &gt; lls</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

ls 是查看远端服务器的。lls 是看本地的。

#### 5.上传 &#8211; put {#sput}

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; put [-P] local [remote]

#如：将本地文件a.txt上传到远程主机/tmp/目录
SFTP &gt; put a.txt /tmp/</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

上传多个文件用 ***** 等模糊匹配命令即可，参数 **-P** 指把文件的权限和时间戳都复制过来。

#### 6.下载 &#8211; get

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; get [-P] local [remote]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

用法与 [put](#sput) 类似。

#### 7. 执行本地命令 &#8211; !

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; !cmd</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

**参数：**cmd为命令，执行为本地执行，并非远程主机执行。

FTP 有同样的用法，上面没写上。

#### 8.退出 &#8211; exit/quit

<div class="" style="position: relative;">
  <pre class="language-shell"><code>SFTP &gt; exit
SFTP &gt; quit
SFTP &gt; bye
SFTP &gt; !</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

除了 **!** 是保留进程退回到本地 shell 界面外，其他都是直接退出 SFTP 进程。

#### 9.移动目录 &#8211; cd/lcd

同 ftp 的 [cd/lcd](#cd) 命令。

## shell脚本

所用命令参数可以查看上面的 [FTP 命令](#ftp)和 [SFTP 命令](#sftp)。

### FTP实现上传

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers language-shell"><code>#!/bin/bash
ftp -n&lt;&lt;!
open 192.168.1.1
user guest 123456
binary
cd /home/data
lcd /home/databackup
prompt
mput *
close
bye
!</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### FTP实现下载

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers language-shell"><code>#!/bin/bash
ftp -n&lt;&lt;!
open 192.168.1.1
user guest 123456
binary
cd /home/data
lcd /home/databackup
prompt
mget *
close
bye
!</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### SFTP实现上传

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers language-shell"><code>#!/bin/sh
sftp guest@192.168.1.1 &lt;&lt; EOF
cd /home/data/
lcd /home/databackup/
-put 201912
-put 202001
quit
EOF</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### SFTP实现下载

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers line-numbers language-shell"><code>#!/bin/sh
sftp guest@192.168.1.1 &lt;&lt; EOF
cd /home/data/
lcd /home/databackup/
-get 201912
-get 202001
quit
EOF</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 说明

  1.  **<<** 是使用即时文件重定向输入。
  2.  **! 或 EOF** 是即时文件的标志，它必须成对出现，以标识即时文件的开始和结尾。两者在 FTP 和 SFTP 都可以使用。
  3.  **get** 命令前加一个“**&#8211;**”以防止其执行错误时 sftp 执行过程被终止。

上述脚本需要修改 **IP、登录用户名、密码和文件路径（文件名）**，自定义的FTP（SFTP）命令需要在即时文件的标志（**! 或 EOF**）中。

FTP 需要实现单文件上传下载，将 mget 改为 get 等单文件命令即可。SFTP 需要实现批量文件上下传可以将具体文件名改为 ***** 等模糊匹配标志即可。

SFTP 脚本执行时会出现登录密码输入提醒，需要输入正确的密码才能继续执行。如果需要实现全自动脚本，可以使用 **lftp** 等命令，或者使用密钥对实现。如果后续有时间会更新这部分内容，敬请关注。
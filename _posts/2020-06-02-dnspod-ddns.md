---
id: 628
title: '[Linux]自定义脚本实现DNSPod DDNS'
date: 2020-06-02T14:55:46+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=628
permalink: /2020/06/dnspod-ddns.html
categories:
  - Linux
  - 工具
tags:
  - ddns
  - dnspod
  - linux
  - openwrt
  - shell
---
OpenWrt原生的DDNS并不支持DNSPod，所以自行查了一下DNSPod的API，自行写了一个shell脚本。

本脚本实现了简单的更新功能，体积极小，代码简单，可以用作参考来修改适合自己的脚本，后续我会根据需求再完善一下全部的功能。

## 实现步骤

### 脚本

首先新建一个shell文件，本文以“ddns_dnspod.sh”为例。将下面的代码复制到新建的shell脚本中。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">#!/bin/sh

LOGIN_TOKEN='****,************'	
DOMAIN='tidnotes.ga'	
RECORD_ID='****'
SUB_DOMAIN='www'
RECORD_TYPE=AAAA
RECORD_NAME=${SUB_DOMAIN}.${DOMAIN}

# 远端IP
if nslookup $RECORD_NAME|grep Address >/dev/null; then
  #IPV6
  remote_ip=`nslookup ${RECORD_NAME}|grep -Eo '[0-9a-f]+(:[0-9a-f:]+)+'`
  #IPV4
  #remote_ip=`nslookup ${RECORD_NAME}|grep 'Address '|grep -Eo '[0-9]+(\.[0-9a-f\.]+)+'| head -n1`
  echo "Remote IP: "$remote_ip
else
  exit 1
fi
 
# 本地IP
if ifconfig pppoe-wan>/dev/null ; then
  #IPV6
  local_ip=`ifconfig pppoe-wan|grep 'inet6 addr: 24.*'|grep -Eo '24[0-9a-f:]+'`
  #IPV4
  #local_ip=`ifconfig pppoe-wan|grep 'inet'|grep -Eo '[0-9]+(\.[0-9a-f\.]+)+'| head -n1`
  echo "Local IP : "$local_ip
else
  echo "Command: 'ifconfig pppoe-wan' failed"
  exit 1;
fi
 
if [ $remote_ip != $local_ip ]; then
  curl -X POST https://dnsapi.cn/Record.Modify -d "login_token=${LOGIN_TOKEN}&format=json&domain=${DOMAIN}&record_id=${RECORD_ID}&sub_domain=${SUB_DOMAIN}&value=${local_ip}&record_type=${RECORD_TYPE}&record_line=%e9%bb%98%e8%ae%a4"
else
  echo "Same IPs, skip unchanged"
  exit 0
fi</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

将脚本中一些参数改为对应的内容：

  * LOGIN_TOKEN：由DnsPod密钥提供，由’ID,Token‘组合而成，用英文的逗号分割，原本的账号密码鉴定方式已经弃用。
  * DOMAIN：根域名。
  * SUB_DOMAIN：子域名。
  * RECORD_ID：需要更改的域名对应的ID，可以利用代码<code class="language-bash" id="{&x&:530.09375,&y&:643.375,&width&:537,&height&:106,&top&:643.375,&right&:1067.09375,&bottom&:749.375,&left&:530.09375}">curl -X POST https://dnsapi.cn/Record.List -d 'login_token=${LOGIN_TOKEN}&format=json&domain=${DOMAIN}&sub_domain=${SUB_DOMAIN}'</code>查询。
  * RECORD_TYPE：记录类型，ipv4用“A”，ipv6用“AAAA”。

本脚本用的是ipv6类型的，使用ipv4的记得改为ipv4相应的代码和内容。脚本主要实现了域名IP的更新，没有加入新增功能，后续有时间的话会进一步更新这个脚本，大家可以用这个脚本来做一个参考修改。

### 设置定时任务

利用OpenWrt的crontab实现定时更新。

对脚本文件更改权限，我的脚本文件放在 <span class="has-inline-color has-vivid-cyan-blue-color">/root/crontab/</span> 中：

<div class="code-copy" style="position: relative;">
  <pre class="command-line"><code class="language-bash">cd /root/crontable/
chmod +x ddns_dnspod.sh</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

然后进入在OpenWrt后台，选择’系统→计划任务‘，输入下面语句：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">0 2 * * * /root/crontable/ddns_dnspod.sh</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

然后重启路由或者重启cron即可定时在每天凌晨2点执行一次脚本，想要其他时间可以按需更改。
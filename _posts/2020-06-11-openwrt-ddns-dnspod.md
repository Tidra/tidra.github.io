---
id: 633
title: OpenWrt原生动态DNS实现DNSPod支持
date: 2020-06-11T21:18:45+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=633
permalink: /2020/06/openwrt-ddns-dnspod.html
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
使用openwrt可以自定义安装原生的动态dns插件（Dynamic DNS），但是并不支持DNSPod的ddns自动更新ip。

对于目前这个问题，一般可以通过编写脚本来实现，或者可以添加DNSPod的功能支持。

目前发现，L大的LEDE源码中已经集成了该插件源码（<a rel="noreferrer noopener" href="https://www.nixonli.com/go/?url=https://github.com/coolsnowwolf/lede/tree/master/package/lean/ddns-scripts_dnspod" target="_blank" rel="nofollow" >https://github.com/coolsnowwolf/lede/tree/master/package/lean/ddns-scripts_dnspod</a>），并且做了优化集成了.cn和.com的脚本维护者是：Small_5。还有<a href="https://github.com/nixonli" rel="nofollow" >nixonli</a>也编写了一个简单的代码支持（<a href="https://github.com/nixonli/ddns-scripts_dnspod" rel="nofollow" >https://github.com/nixonli/ddns-scripts_dnspod</a>）。

下面是介绍以nixonli的代码使用方法。  
**注意：如果ddns显示的日志中文部分出现问题，可以参考《[关于DDNS日志输出中文问题](https://www.tidnotes.ga/2020/06/ddns-writelog.html)》修改。**下面方法都是在ddns插件已安装的情况下完成的。

## 方法一：添加代码文件

编辑添加文件“/usr/lib/ddns/update\_dnspod\_cn.sh”。以下代码是根据nixonli的代码修改了一部分提示。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">#!/bin/sh
 
#检查传入参数
[ -z "$username" ] && write_log 14 "配置错误![用户名]不能为空"
[ -z "$password" ] && write_log 14 "配置错误![密码]不能为空"
 
#检查外部工具curl,sed
command -v curl >/dev/null 2>&1 || write_log 13 "需要curl支持,请先安装"
command -v sed >/dev/null 2>&1 || write_log 13 "需要 sed 支持，请先安装"
 
# 变量声明
local __HOST __DOMAIN __TYPE __RECIP __RECID DATFILE
 
# 从 $domain 分离主机和域名
[ "${domain:0:2}" == "@." ] && domain="${domain/./}" # 主域名处理
[ "$domain" == "${domain/@/}" ] && domain="${domain/./@}" # 未找到分隔符，兼容常用域名格式
__HOST="${domain%%@*}"
__DOMAIN="${domain#*@}"
[ -z "$__HOST" -o "$__HOST" == "$__DOMAIN" ] && __HOST="@"
 
# 设置记录类型
[ $use_ipv6 -eq 0 ] && __TYPE="A" || __TYPE="AAAA"
 
#添加解析记录
add_domain() {
DATFILE=`curl -s -d "login_token=$username,$password&format=json&domain=$__DOMAIN&sub_domain=$__HOST&record_type=$__TYPE&record_line_id=0&value=${__IP}" "https://dnsapi.cn/Record.Create"`
value=`jsonfilter -s "$DATFILE" -e "@.status.code"`
if [ $value == 1 ];then
	write_log 7 "添加新解析记录IP:[$__HOST],[$__TYPE],[${__IP}]成功!"
else
	write_log 13 "添加解析记录IP:[$__HOST],[$__TYPE],[${__IP}]失败! 返回code:$value"
fi
}
 
#修改解析记录
update_domain() {
DATFILE=`curl -s -d "login_token=$username,$password&format=json&domain=$__DOMAIN&record_id=$__RECID&value=${__IP}&record_type=$__TYPE&record_line_id=0&sub_domain=$__HOST" "https://dnsapi.cn/Record.Modify"`
value=`jsonfilter -s "$DATFILE" -e "@.status.code"`
if [ $value == 1 ];then
	write_log 7 "修改解析记录host:[$__HOST],type:[$__TYPE],ip:[${__IP}]成功!"
else
	write_log 13 "修改解析记录host:[$__HOST],type:[$__TYPE],ip:[${__IP}]失败! 返回code:$value"
fi
}
 
#获取域名解析记录
describe_domain() {
	DATFILE=`curl -s -d "login_token=$username,$password&format=json&domain=$__DOMAIN" "https://dnsapi.cn/Record.List"`
	value=`jsonfilter -s "$DATFILE" -e "@.records[@.name='$__HOST'].name"`
	if [ "$value" == "" ]; then
		write_log 4 "解析记录:[$__HOST]不存在,类型: HOST"
		ret=1
	else
		value=`jsonfilter -s "$DATFILE" -e "@.records[@.name='$__HOST'].type"`
		if [ "$value" != "$__TYPE" ]; then
				write_log 4 "当前解析类型:[$__TYPE], 获得不匹配类型: TYPE"
				ret=2; continue
		else
			__RECID=`jsonfilter -s "$DATFILE" -e "@.records[@.name='$__HOST'].id"`
			write_log 7 "获得解析记录ID:[$__RECID], 类型: ID"
			__RECIP=`jsonfilter -s "$DATFILE" -e "@.records[@.name='$__HOST'].value"`
			if [ "$__RECIP" != "${__IP}" ]; then
				write_log 6 "地址需要修改,本地地址:[${__IP}]"
				ret=2
			fi
		fi
	fi
	return $ret
}
describe_domain
ret=$?
if [ $ret == 1 ];then
	sleep 3 && add_domain
elif [ $ret == 2 ];then
	sleep 3 && update_domain
else
	write_log 15 "本地IP：“${__IP}” 解析记录IP：“$__RECIP”地址不需要修改"
fi

return 0</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

编辑文件“/etc/ddns/services”，添加以下内容。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">"dnspod.cn"		"update_dnspod_cn.sh"</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

编辑文件“/etc/ddns/services_ipv6″，添加以下内容。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers"><code class="language-bash">"dnspod.cn"		"update_dnspod_cn.sh"</code></pre>
  
  <button name="copy-btn">点击复制</button>
</div>

完成上述操作就可以在ddns内选择dnspod进行域名解析了。

## 方法二：直接安装插件

下载插件的安装包（<a href="https://www.nixonli.com/wp-content/uploads/2019/08/d89579eb74acd37.zip" rel="nofollow" >opwnwrt x86 ddns-scripts_dnspod</a>），或者通过自行编译，编译代码见原作者的github：<a href="https://github.com/nixonli/ddns-scripts_dnspod" rel="nofollow" >https://github.com/nixonli/ddns-scripts_dnspod</a>。

得到安装包后，到openwrt的后台，进入**系统→软件包（Software）**，上传文件包（Upload Package）等安装完即可。

<div style="height:50px" aria-hidden="true" class="wp-block-spacer">
</div>

<blockquote class="wp-block-quote">
  <p>
    本文根据Nixonli博客的<a href="https://www.nixonli.com/23133.html" rel="nofollow" >openwrt 原生动态DNS(DDNS) 支持DnsPod解析</a>编写，其中更改了部分的代码问题。
  </p>
  
  <cite>对于update_dnspod_cn.sh中的代码可以根据自己需要更改，复杂功能可以查看LEDE的源码，那个更加符合ddns的原来设计，不过代码大小会多一点。想要简单实现可以参考<a href="https://www.tidnotes.ga/2020/06/dnspod-ddns.html">[Linux]自定义脚本实现DNSPod DDNS</a>。</cite>
</blockquote>
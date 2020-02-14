---
id: 527
title: '[SQL]关于锁表以及解决方法'
date: 2020-02-15T02:11:18+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=527
permalink: /2020/02/sql-unlock.html
categories:
  - SQL
tags:
  - mysql
  - oracle
  - sql
  - 锁表
---
数据库锁表，指在数据库里，同一个数据可能有多个人来读取或更改，为了防止更改的时候别人也同时更改，所以要**锁住表**防止别人更改。

简单来说，锁表主要发生在以下几种情况：

  1. 锁表主要发生在<code class="language-sql">insert</code>、<code class="language-sql">update</code>、<code class="language-sql">delete</code>中；
  2. 在执行上面语句时，没有执行<code class="language-sql">commite</code>、回滚或退出数据库用户时，在另一进程执行上述语句会进入资源正忙的异常（即卡死），此时已锁表；
  3. 多个更改语句一起执行，而不是顺序执行时回锁表；
  4. <code class="language-sql">insert</code>等超多个语句一直执行，而不<code class="language-sql">commite</code>，会发生锁表。

以上情况只是简单的锁表情况，还有很多复杂的情况就不一一列举出来。如果出现<code class="language-sql">insert</code>等SQL语句执行时，长时间无反应甚至卡死状态，很有可能发生了锁表。

## Oracle锁表解决

查看当前系统锁表情况

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-sql"><code>select * from v$locked_object a,v$session b 
where a.session_id = b.sid;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

得到的数据库中所有DML语句（指对数据库中表记录的操作）产生的所锁，包括行锁和表锁。**解决死锁**主要是要表中的 **sid、serial#** 两个字段。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-sql"><code>-- sid 和 serial# 是上面sql语句得到的数值
alter system kill session 'sid,serial#';</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## MySQL锁表解决

查锁表的进程

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-sql"><code>SHOW PROCESSLIST;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

找到锁表的那个进程的 **Id**，然后杀掉被锁的表

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-sql"><code>-- ID 即被锁进程的ID值
KILL ID;</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>
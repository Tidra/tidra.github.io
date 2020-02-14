---
id: 423
title: '[Python]关于‘DataFrame’对象没有‘sort’属性'
date: 2019-11-24T21:18:37+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=423
permalink: /2019/11/python-error-sort.html
categories:
  - Python
tags:
  - attribute
  - Python
  - rolling_mean
  - sort
  - 关联规则
  - 属性
---
最近在阅读《Python数据分析与挖掘实战》一书，其中发现不少内容没有更新，导致提供的代码直接运行会出现错误。

下面是第8章《中医证型关联规则挖掘》的“**代码清单8-1 数据聚类离散化代码**”：

<!--more-->

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-python"><code>#-*- coding:utf-8 -*-

from __future__ import print_function
import pandas as pd
from sklearn.cluster import KMeans

datafile = '../data/data.xls'
processedfile = '../tmp/data_processed.xls'
typelabel = {u'肝气郁结证型系数':'A', u'热毒蕴结证型系数':'B', u'冲任失调证型系数':'C', u'气血两虚证型系数':'D', u'脾胃虚弱证型系数':'E', u'肝肾阴虚证型系数':'F'}
k = 4

data = pd.read_excel(datafile)
keys = list(typelabel.keys())
result = pd.DataFrame()

if __name__ == '__main__':
    for i in range(len(keys)):
        print(u'正在进行“%s”的聚类...' % keys[i])
        kmodel = KMeans(n_clusters=k, n_jobs=4)
        kmodel.fit(data[[keys[i]]].as_matrix())

        r1 = pd.DataFrame(kmodel.cluster_centers_, columns=[typelabel[keys[i]]])
        r2 = pd.Series(kmodel.labels_).value_counts()
        r2 = pd.DataFrame(r2, columns=[typelabel[keys[i]] + 'n'])
        r = pd.concat([r1, r2], axis=1).sort(typelabel[keys[i]])
        r.index = [1,2,3,4]
        r[typelabel[keys[i]]] = pd.rolling_mean(r[typelabel[keys[i]]], 2)
        r[typelabel[keys[i]]][1] = 0.0
        result = result.append(r.T)

    result = result.sort()
    result.to_excel(processedfile)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

其中，第25、31行中会出现 **&#8216;DataFrame&#8217; object has no attribute &#8216;sort&#8217;** 错误，第27行会出现 **module &#8216;pandas&#8217; has no attribute &#8216;rolling_mean&#8217;** 的错误。

## 关于 **&#8216;DataFrame&#8217; object has no attribute &#8216;sort&#8217;** 

**sort** 已经弃用，代替使用的是 [sort_values](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html) 或者 [sort_index](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_index.html) 。

  * **sort_values** 基本用法：
      * 根据“col1”排序：<code class="language-python">df.sort_values(by=['col1'])</code>
      * 根据多个排序：<code class="language-python">df.sort_values(by=['col1', 'col2'])</code>
      * 倒叙排序（省略为默认正序）：<code class="language-python">df.sort_values(by='col1', ascending=False)</code>
      * 缺省值NaNs显示在前（省略默认在后）：`<code class="language-python">df.sort_values(by='col1', ascending=False, na_position='first')`</code>
      * **注意：只有by是必须的，其他可缺省。**
  * **sort_index** 基本用法：
      * 直接使用，不需要添加参数：<code class="language-python">df.sort_index()</code>

## 关于 module &#8216;pandas&#8217; has no attribute &#8216;rolling_mean&#8217; ****

pandas包中关于“rolling_mean”已经更新用法，代替使用的是 [rolling](https://pandas.pydata.org/pandas-docs/version/0.23/generated/pandas.DataFrame.rolling.html)。

“rolling_mean” 的用法应该对应为<code class="language-python">df.rolling(2).mean()</code>。

## 修改版代码

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-python"><code>#-*- coding:utf-8 -*-

from __future__ import print_function
import pandas as pd
from sklearn.cluster import KMeans

datafile = '../data/data.xls'
processedfile = '../tmp/data_processed.xls'
typelabel = {u'肝气郁结证型系数':'A', u'热毒蕴结证型系数':'B', u'冲任失调证型系数':'C', u'气血两虚证型系数':'D', u'脾胃虚弱证型系数':'E', u'肝肾阴虚证型系数':'F'}
k = 4

data = pd.read_excel(datafile)
keys = list(typelabel.keys())
result = pd.DataFrame()

if __name__ == '__main__':
    for i in range(len(keys)):
        print(u'正在进行“%s”的聚类...' % keys[i])
        kmodel = KMeans(n_clusters=k, n_jobs=4)
        kmodel.fit(data[[keys[i]]].as_matrix())

        r1 = pd.DataFrame(kmodel.cluster_centers_, columns=[typelabel[keys[i]]])
        r2 = pd.Series(kmodel.labels_).value_counts()
        r2 = pd.DataFrame(r2, columns=[typelabel[keys[i]] + 'n'])
        r = pd.concat([r1, r2], axis=1).sort_values(typelabel[keys[i]])
        r.index = [1,2,3,4]
        r[typelabel[keys[i]]] = r[typelabel[keys[i]]].rolling(2).mean()
        r[typelabel[keys[i]]][1] = 0.0
        result = result.append(r.T)

    result = result.sort_index()
    result.to_excel(processedfile)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>
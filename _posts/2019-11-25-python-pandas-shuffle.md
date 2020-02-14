---
id: 427
title: '[Python]关于DataFrame和NumPy数组如何打乱数据'
date: 2019-11-25T14:24:44+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=427
permalink: /2019/11/python-pandas-shuffle.html
categories:
  - Python
tags:
  - dataframe
  - numpy
  - pandas
  - Python
  - shuffle
  - sklearn
  - 数据打乱
---
之前在[《[Python]关于‘DataFrame’对象没有‘sort’属性》](https://www.tidnotes.ga/2019/11/python-error-sort.html)一文中，发现了《Python数据分析与挖掘实战》一书中关于第8章实验代码的一些在新版本的pandas库中出现错误，同时给出了相应的解决方案。在第9章的学习中也发现，其中shuffle（打乱）数据也出现了一些问题。

<!--more-->

所以，本文主要是讲解一下关于pandas如何打乱数据的一些方法。

## 关于pandas使用random.shuffle(data)的错误结果

该书中“第9章 基于水色图像的水质评价”中关于数据打乱引入的包是**random**，利用<code class="language-python">random.shuffle(data)</code>后会出现如下结果：

<div class="" style="position: relative;">
  <pre class="language-python"><code>[[ 1.00000000e+00  1.00000000e+00  5.82822907e-01 ... -1.26431370e-02
  -1.60903640e-02 -4.15362390e-02]
 [ 1.00000000e+00  1.00000000e+01  6.41659507e-01 ...  9.72713600e-03
  -3.72381400e-03 -3.77944800e-03]
 [ 1.00000000e+00  1.00000000e+01  6.41659507e-01 ...  9.72713600e-03
  -3.72381400e-03 -3.77944800e-03]
 ...
 [ 4.00000000e+00  8.00000000e+00  4.73493371e-01 ...  3.87451300e-03
   2.20928100e-03  2.36937400e-03]
 [ 2.00000000e+00  3.00000000e+00  4.91916017e-01 ...  9.28491600e-03
   9.66301000e-03  1.15485330e-02]
 [ 4.00000000e+00  1.50000000e+01  4.61240440e-01 ... -1.23856500e-03
   5.01603000e-04  6.81254900e-03]]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

可以看出，第1行数据和第5行数据是相同的，而原本数据中并没有完全相同的数据，所以说使用<code class="language-python">random.shuffle(data)</code>使数据重复而且缺失了，下面是将全部数据的类别输出以做更进一步的解释：

<div class="" style="position: relative;">
  <pre class="language-python"><code>[1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 2. 1. 1. 2. 1. 1. 1. 1. 1. 1. 2. 1. 2.
 1. 1. 1. 1. 1. 2. 2. 2. 2. 2. 1. 1. 1. 1. 1. 2. 2. 1. 2. 1. 2. 1. 2. 1.
 1. 1. 1. 1. 2. 2. 2. 1. 1. 1. 1. 3. 3. 1. 2. 2. 1. 2. 1. 1. 3. 1. 2. 3.
 3. 2. 3. 3. 2. 1. 2. 3. 2. 3. 3. 2. 3. 1. 3. 1. 3. 2. 1. 3. 2. 3. 1. 2.
 1. 1. 2. 2. 1. 3. 3. 3. 1. 3. 1. 1. 2. 1. 3. 1. 1. 3. 3. 2. 3. 1. 1. 3.
 1. 3. 1. 3. 3. 3. 3. 3. 1. 1. 1. 4. 3. 2. 2. 1. 3. 3. 1. 1. 2. 1. 4. 2.
 1. 4. 4. 3. 1. 3. 1. 1. 3. 2. 2.]</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

可以看出，数据总量是不变的，但是类别缺少了**类别5**，所以使用该shuffle是会导致后面的结果出现问题的。

利用<code class="language-python">type()</code>方法查看数据类型可以得知，该**data**的数据类型是**NumPy数组**，对NumPy数组进行测试可以得知：

  * **random.shuffle(data)并不完全支持NumPy数组**

经过我的初步实验，结果得出<code class="language-python">random.shuffle(data)</code>对普通的数组等都是支持的，但是对**NumPy数组**会出现类如重复、缺失等现象，所以说对于**NumPy数组**并不适合用**random**库来实现数据打乱。

同样的，pandas中的**DataFrame也是不适用这种方式打乱数据的**。

## 打乱数据方法

### 1、NumPy特有方法

numpy库中有<code class="language-python">np.random.shuffle(x)</code>和<code class="language-python">np.random.permutation(x)</code>两种打乱顺序的方法。前一个是改变数据自身顺序；后一个是返回一个随机排列，自身数据不变。

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-python"><code>import numpy as np

#shuffle使用
np.random.shuffle(data)

#permutation使用
data = np.random.permutation(data)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 2、DataFrame特有方法

pandas库自带有DataFrame数据打乱的方法，基本的写法如下：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-python"><code># 假设df = DataFrame
df.sample(frac=1)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

其中，参数**frac**是返回数据的比例，1即100%，如果只需要数据的80%，参数即为**frac=0.8**。如果需要打乱后数据集的index（索引）还是按照正常的排序，则如下：

<div class="code-copy" style="position: relative;">
  <pre class="language-python"><code>df.sample(frac=1).reset_index(drop=True)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

### 3、sklearn(机器学习的库）的shuffle方法

sklearn库中shuffle方法是适用于DataFrame以及NumPy数组的，它的基本用法如下：

<div class="code-copy" style="position: relative;">
  <pre class="line-numbers line-numbers line-numbers language-python"><code>from sklearn.utils import shuffle
df = shuffle(df)</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

个人觉得，在不太清楚数据类型的时候，使用sklearn库的shuffle方法是最好的。
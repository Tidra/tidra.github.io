---
id: 607
title: Github fork后同步更新
date: 2020-03-11T16:30:59+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=607
permalink: /2020/03/github-fork-update.html
image: /wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G.png
categories:
  - 工具
tags:
  - fork
  - GitHub
  - update
---
github有一个fork功能，相当于拷贝一份别人的项目到自己的仓库中，但是并不会随原项目更新而更新自己fork来的项目中。

目前，github还没有一键更新的功能，可以使用 **“New pull request”** 来实现。

## 实现步骤

1、选择自己仓库中fork的项目，点击 **“New pull request”** 。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/AXV6@IQUQGYB1VWM22I.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/AXV6@IQUQGYB1VWM22I.png" alt="Github fork后同步更新 | 点击 “New pull request”" class="wp-image-608" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/AXV6@IQUQGYB1VWM22I.png 1020w, https://www.tidnotes.ga/wp-content/uploads/2020/03/AXV6@IQUQGYB1VWM22I-300x101.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/AXV6@IQUQGYB1VWM22I-768x258.png 768w" sizes="(max-width: 1020px) 100vw, 1020px" /></a></figure> 

2、页面跳转到以下页面，左边选择为自己的仓库项目。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/@U8WOUC7AL_LCJ3GNU1FF.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/@U8WOUC7AL_LCJ3GNU1FF.png" alt="Github fork后同步更新 | 选择自己的仓库项目" class="wp-image-609" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/@U8WOUC7AL_LCJ3GNU1FF.png 1012w, https://www.tidnotes.ga/wp-content/uploads/2020/03/@U8WOUC7AL_LCJ3GNU1FF-300x145.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/@U8WOUC7AL_LCJ3GNU1FF-768x372.png 768w" sizes="(max-width: 1012px) 100vw, 1012px" /></a></figure> 

3、等待页面跳转到**master**页面，点击 **“compare across forks”**。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7-1024x487.png" alt="Github fork后同步更新 | 点击 “compare across forks”" class="wp-image-610" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7-1024x487.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7-300x143.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7-768x365.png 768w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4Z29KK99VA2ITMW7.png 1026w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

4、步骤3后会出现以下页面，**左边选择自己的项目，右边选择源项目**。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G.png" alt="Github fork后同步更新 | 左边选择自己的项目，右边选择源项目" class="wp-image-611" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G.png 1020w, https://www.tidnotes.ga/wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G-300x109.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/ZCCNOC9Q59IFH0W2SNX6G-768x280.png 768w" sizes="(max-width: 1020px) 100vw, 1020px" /></a></figure> 

5、选择后，页面会显示源项目更新的内容，点击 **“Create pull request”**。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/9QANF@H4IMWLTLTVNF.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/9QANF@H4IMWLTLTVNF.png" alt="Github fork后同步更新 | 点击 “Create pull request”" class="wp-image-612" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/9QANF@H4IMWLTLTVNF.png 1010w, https://www.tidnotes.ga/wp-content/uploads/2020/03/9QANF@H4IMWLTLTVNF-300x171.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/9QANF@H4IMWLTLTVNF-768x438.png 768w" sizes="(max-width: 1010px) 100vw, 1010px" /></a></figure> 

6、内容随自己需求编写，或直接点击 **“Create pull request”**。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/W68VJ5K63MD@HMXN.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/W68VJ5K63MD@HMXN.png" alt="Github fork后同步更新 | 直接点击 “Create pull request”" class="wp-image-613" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/W68VJ5K63MD@HMXN.png 1014w, https://www.tidnotes.ga/wp-content/uploads/2020/03/W68VJ5K63MD@HMXN-300x177.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/W68VJ5K63MD@HMXN-768x453.png 768w" sizes="(max-width: 1014px) 100vw, 1014px" /></a></figure> 

7、页面会变成下图样子，找到点击 **“Merge pull request”**，进行数据合并。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P-1024x724.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P-1024x724.png" alt="Github fork后同步更新 | 点击 “Merge pull request”" class="wp-image-614" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P-1024x724.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P-300x212.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P-768x543.png 768w, https://www.tidnotes.ga/wp-content/uploads/2020/03/4K5C_HJ9Z@B6Q6L509P.png 1060w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

8、点击 **“Confirm merga”**，进行合并，最后完成更新。<figure class="wp-block-image size-large">

<a href="https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW.png" target="_blank" rel="noreferrer noopener"><img src="https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW-1024x524.png" alt="Github fork后同步更新 | 点击 “Conflrm merga”，进行合并" class="wp-image-615" srcset="https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW-1024x524.png 1024w, https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW-300x153.png 300w, https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW-768x393.png 768w, https://www.tidnotes.ga/wp-content/uploads/2020/03/62A8YUJLHWN3FKNW.png 1044w" sizes="(max-width: 1024px) 100vw, 1024px" /></a></figure> 

根据上述步骤，即可以实现fork项目的更新。
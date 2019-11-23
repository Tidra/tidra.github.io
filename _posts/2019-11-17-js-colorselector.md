---
id: 395
title: '[JS]纯代码版基于JQuery的颜色选择器'
date: 2019-11-17T17:01:37+08:00
author: TiD
layout: post
guid: https://www.tidnotes.ga/?p=395
permalink: /2019/11/js-colorselector.html
image: /wp-content/uploads/2019/11/image-2.png
categories:
  - JavaScript
  - 前端
  - 工具
tags:
  - hex
  - JavaScript
  - rgb
  - 颜色
  - 颜色选择器
---
<blockquote class="wp-block-quote">
  <p>
    本文介绍一个基于Jquery的自制颜色选择器，本文会将颜色选择器的制作思路和代码供大家学习、参考。想直接引用的也可以直接使用我给出的代码，但请注明出处，谢谢。
  </p>
  
  <cite> 在线<a href="https://www.tidnotes.ga/color">颜色表、颜色选择器、RGB和Hex互转</a>链接：<br /><a href="https://www.tidnotes.ga/color">https://www.tidnotes.ga/color</a> </cite>
</blockquote>

以下内容是基于jQuery写的一个颜色选择器，大家可以根据需要学习、修改或引用，引用还请注明出处。

## 成品效果<figure class="wp-block-image">

[<img src="https://www.tidnotes.ga/wp-content/uploads/2019/11/image-2.png" alt="颜色选择器 | 小TiD笔记" class="wp-image-397" srcset="https://www.tidnotes.ga/wp-content/uploads/2019/11/image-2.png 507w, https://www.tidnotes.ga/wp-content/uploads/2019/11/image-2-300x178.png 300w" sizes="(max-width: 507px) 100vw, 507px" />](https://www.tidnotes.ga/color)<figcaption>[在线版颜色选择器](https://www.tidnotes.ga/color)</figcaption></figure> 

## 制作思路

颜色选择器的类型有不少，本文用的是主色在主板上，主色变色条在侧边的形式，大家可以根据需要更改样式。制作该颜色选择器基本就思路可以简化如下：

  1. 在主色板上呈现红、黄、绿、青、蓝、粉、红的渐变变化；
  2. 在横向渐变色的基础上，叠加纵向颜色加深，即逐渐叠加黑色；
  3. 在侧边颜色条显示当前主色板颜色，颜色逐渐变浅，即叠加白色；
  4. 最后显示选中的颜色。

### 关于颜色

  * 可以利用h5的<code class="language-markup">&lt;canvas></code>标签来绘制颜色；
  * 主颜色的变化规律如下：#ff0000 → #ffff → #00ff00 → #00ffff → #0000ff → #ff00ff → #ff0000；
  * 深色变化利用 rgba(0,0,0,0) → rgba(0,0,0,1) 实现；
  * 浅色变化利用 rgba(255,255,255,0) → rgba(255,255,255,1) 实现。

## 使用方法

先引入JQuery的文件：  
<code class="language-markup">&lt;script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js">&lt;/script> </code>

直接复制下面的代码，或是将GitHub上的[colorSelector.js](https://github.com/Tidra/ColorSelector-for-HTML/blob/master/colorSelector.js)下载到本地，在需要显示的地方用<code class="language-markup">&lt;script src="colorSelector.js">&lt;/script></code>即可显示颜色选择器。 

或者直接使用<code class="language-markup">&lt;script src="https://raw.githubusercontent.com/Tidra/ColorSelector-for-HTML/master/colorSelector.js">&lt;/script></code>即可。

## 实现代码（colorSelector.js）

<div style="position: relative;">
  <pre class="line-numbers"><code class="lan language-js">/**
 * 作者(Author)：tidra
 * 作者URI(Author URI)：https://www.tidnotes.ga
 * 版本(Version)：1.0
 * 许可证(License)：GNU通用公共许可证v3.0或更高版本(GNU General Public License v3.0 or later)
 * 许可证URI(License URI)：https://github.com/Tidra/ColorSelector-for-HTML/blob/master/LICENSE
 */

function createBox() {
    var htmlText = '&lt;div class="color-box">&lt;div style="position: relative;margin-right: 20px;">&lt;canvas class="colorbck" id="colorbck" width="255" height="255">&lt;/canvas>&lt;div class="it" id="it">&lt;/div>&lt;/div>&lt;div style="position: relative;margin-right: 20px;">&lt;canvas class="colorbar" id="colorbar" width="10" height="255">&lt;/canvas>&lt;div class="choose-it" id="choose-it">&lt;div>&lt;/div>&lt;/div>&lt;/div>&lt;div style="line-height: 30px;">&lt;b>当前选择颜色：&lt;/b>&lt;div id="show">&lt;/div>&lt;div id="showColor">&lt;/div>&lt;/div>&lt;/div>';
    
    document.write(htmlText);

    $('.color-box').css({
        'display': 'flex',
        'width': '465px',
        'background-color': 'rgb(209, 209, 209)',
        'color': 'rgb(53, 53, 53)',
        'padding': '10px',
        'border-radius': '10px',
    })

    $('.it').css({
        'position': 'absolute',
        'top': '-2px',
        'left': '-2px',
        'width': '4px',
        'height': '4px',
        'border': '1px solid rgba(95, 91, 91, 0.8)',
        'border-radius': '100%'
    })

    $('.choose-it').css({
        'font-size': '10px',
        'color': 'rgba(148, 148, 148, 0.89)',
        'position': 'absolute',
        'top': '0px',
        'left': '-1px'
    })

    $('.choose-it div').css({
        'width': '10px',
        'height': '1px',
        'border': '1px solid rgba(128, 128, 128, 0.89)',
        'border-radius': '100%',
    })

    $('.choose-it').append("&lt;style>#choose-it::before{position: absolute;content: '▶';right: 10px;top: -7px;}&lt;/style>").append("&lt;style>#choose-it::after{position: absolute;content: '◀';left: 10px;top: -7px;}&lt;/style >");

    $('#show').css({
        'width': '50px',
        'height': '24px',
        'margin': '15px 0',
    })

    $('#showColor').css({
        'background-color': '#ececec',
        'width': '135px',
        'padding': '10px',
        'border-radius': '10px',
    })
}

function boxActive() {
    // 调色板绘制
    var cbck = document.getElementById('colorbck').getContext("2d");
    var my_gra = cbck.createLinearGradient(1, 0, 254, 0);
    my_gra.addColorStop(0, "#ff0000");
    my_gra.addColorStop(1 / 6, "#ffff00");
    my_gra.addColorStop(2 / 6, "#00ff00");
    my_gra.addColorStop(3 / 6, "#00ffff");
    my_gra.addColorStop(4 / 6, "#0000ff");
    my_gra.addColorStop(5 / 6, "#ff00ff");
    my_gra.addColorStop(1, "#ff0000");
    cbck.fillStyle = my_gra;
    cbck.fillRect(0, 0, 255, 255);
    var my_gradient = cbck.createLinearGradient(0, 1, 0, 254);
    my_gradient.addColorStop(0, "rgba(0,0,0,0)");
    my_gradient.addColorStop(1, "rgba(0,0,0,1)");
    cbck.fillStyle = my_gradient;
    cbck.fillRect(0, 0, 255, 255);

    // 调色条绘制
    var cbar = document.getElementById('colorbar').getContext("2d");
    var my_g1 = cbar.createLinearGradient(0, 1, 0, 254);
    my_g1.addColorStop(0, "rgba(255,255,255,0)");
    my_g1.addColorStop(1, "rgba(255,255,255,1)");
    cbar.fillStyle = my_g1;
    cbar.fillRect(0, 0, 10, 255);
    var my_g = cbar.createLinearGradient(0, 1, 0, 254);
    my_g.addColorStop(0, "rgba(255,0,0,1)");
    my_g.addColorStop(1, "rgba(255,0,0,0)");
    cbar.fillStyle = my_g;
    cbar.fillRect(0, 0, 10, 255);

    // 颜色变化
    function clickIt(X = 0, Y = 0, who = 'bck') {
        if (X &lt; 0) {
            X = 0;
        } else if (X > 254) {
            X = 254;
        }
        if (Y &lt; 0) {
            Y = 0;
        } else if (Y > 254) {
            Y = 254;
        }
        var imgData = [];
        var bar = $('#choose-it');
        if (who == 'bck') {
            imgData = cbck.getImageData(X, Y, 1, 1).data;
            cbar.clearRect(0, 0, 10, 255);
            cbar.fillStyle = my_g1;
            cbar.fillRect(0, 0, 10, 255);
            my_g = cbar.createLinearGradient(0, 1, 0, 254);
            my_g.addColorStop(0, "rgba(" + imgData[0] + "," + imgData[1] + "," + imgData[2] + ",1)");
            my_g.addColorStop(1, "rgba(" + imgData[0] + "," + imgData[1] + "," + imgData[2] + ",0)");
            cbar.fillStyle = my_g;
            cbar.fillRect(0, 0, 10, 255);

            X = X - 2;
            Y = Y - 2;
            $('#it').css({
                'top': Y,
                'left': X
            });
        } else {
            bar.css('top', Y);
        }
        Y = bar.css('top').replace("px", "");
        imgData = cbar.getImageData(0, Y, 1, 1).data;
        var color = 'rgb(' + imgData[0] + ',' + imgData[1] + ',' + imgData[2] + ')';
        var hex = rgb2hex(color);
        $('#show').css({
            'background-color': color
        })
        $('#showColor').html(color + '&lt;br>' + hex);

    }

    // 调色板点击事件
    $('#colorbck').click(function (e) {
        e.preventDefault();
        var X = e.offsetX;
        var Y = e.offsetY;
        clickIt(X, Y);
    });

    // 调色板拖拽事件
    $('#it').mousedown(function (e) {
        var bar = $('#colorbck').offset();
        $(document).mousemove(function (e) {
            var X = e.pageX - bar.left;
            var Y = e.pageY - bar.top;
            clickIt(X, Y);
        }).mouseup(function () {
            $(document).off('mousemove');
        });
    }).click(function (e) {
        var bar = $('#colorbck').offset();
        e.preventDefault();
        var X = e.pageX - bar.left;
        var Y = e.pageY - bar.top;
        clickIt(X, Y);
    });

    // 调色条点击事件
    $('#colorbar').click(function (e) {
        e.preventDefault();
        var Y = e.offsetY;
        clickIt(X = 5, Y, 'bar');
    });

    // 调色条拖拽事件
    $('#choose-it').mousedown(function (e) {
        var bar = $('#colorbar').offset();
        $(document).mousemove(function (e) {
            var Y = e.pageY - bar.top;
            clickIt(X = 5, Y, 'bar');
        }).mouseup(function () {
            $(document).off('mousemove');
        });
    }).click(function (e) {
        var bar = $('#colorbar').offset();
        e.preventDefault();
        var Y = e.pageY - bar.top;
        clickIt(X = 5, Y, 'bar');
    });
}

// 绘制调色选择器
createBox();
// 对事件做绑定
boxActive();</code></pre>
  
  <button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button>
</div>

## 最后

本颜色编辑器是基于jQuery写的，所以一定要引入jQuery后再使用。

颜色板的颜色变化都是从第一个像素点到倒数第二个像素点的，从0到最后会出现无法取最边缘的颜色，个人认为和取色的一个像素点有关。同时，颜色条的变化先要去除原来的底色，再重新绘制，否则会出现多颜色叠加的情况。

如有其他的问题、错漏地方或更好的方案，欢迎在下方留言。
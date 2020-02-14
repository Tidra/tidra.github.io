---
id: 377
title: 颜色表、颜色选择器、RGB和Hex互转
date: 2019-11-16T21:34:21+08:00
author: TiD
layout: page
guid: https://www.tidnotes.ga/?page_id=377
image: /wp-content/uploads/2019/11/colorChart.png
---
## 颜色选择器

<div class="color-box">
  <div style="display: flex;">
    <div style="position: relative;margin-right: 14px;">
      <canvas class="colorbck" id="colorbck" width="255" height="255"></canvas> 
      
      <div class="it" id="it">
      </div>
    </div>
    
    <div style="position: relative;">
      <canvas class="colorbar" id="colorbar" width="10" height="255"></canvas> 
      
      <div class="choose-it" id="choose-it">
        <div>
        </div>
      </div>
    </div>
  </div>
  
  <div style="line-height: 30px;margin-left: 20px;">
    <div>
      <b>当前选择颜色：</b> 
      
      <div id="show">
      </div>
    </div>
    
    <div id="showColor">
    </div>
  </div>
</div>

## RGB色和Hex色互转

<div class="r-h">
  <div class="inValue">
    rgb(<input name="r" type="number" min="0" max="255" value="0" />,<input name="g" type="number" min="0" max="255" value="0" />,<input name="b" type="number" min="0" max="255" value="0" />)
  </div>
  
  <div id="rgb2hex">
    <svg t="1573902941567" class="icon" viewBox="0 0 1325 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="18840" width="32" height="32"> <path d="M46.501647 294.550588a45.176471 45.176471 0 1 1 0-90.352941H392.131765a45.176471 45.176471 0 0 1 0 90.352941H46.381176zM758.302118 841.788235a45.176471 45.176471 0 1 1 0-90.352941h355.689411a45.176471 45.176471 0 0 1 0 90.352941H758.362353z" fill="#1296db" p-id="18841"></path> <path d="M364.303059 273.648941a45.176471 45.176471 0 1 1 75.715765-49.332706L544.527059 384.602353a45.176471 45.176471 0 1 1-75.65553 49.392941L364.303059 273.588706z m248.95247 382.012235a45.176471 45.176471 0 1 1 75.715765-49.392941l105.773177 162.394353a45.176471 45.176471 0 0 1-75.65553 49.332706l-105.833412-162.334118z" fill="#1296db" p-id="18842"></path> <path d="M1301.684706 796.611765l-202.992941 219.557647a18.070588 18.070588 0 0 1-31.322353-12.288V589.342118a18.070588 18.070588 0 0 1 31.322353-12.288l202.992941 219.557647z" fill="#1296db" p-id="18843"></path> <path d="M46.501647 747.941647a45.176471 45.176471 0 1 0 0 90.352941H392.131765a45.176471 45.176471 0 1 0 0-90.352941H46.381176zM758.302118 200.824471a45.176471 45.176471 0 1 0 0 90.352941h355.689411a45.176471 45.176471 0 0 0 0-90.352941H758.362353z" fill="#1296db" p-id="18844"></path> <path d="M364.303059 768.903529a45.176471 45.176471 0 1 0 75.715765 49.392942l354.785882-544.406589a45.176471 45.176471 0 0 0-75.715765-49.332706l-354.785882 544.346353z" fill="#1296db" p-id="18845"></path> <path d="M1301.684706 246.000941L1098.691765 26.443294a18.070588 18.070588 0 0 0-31.322353 12.227765v414.599529a18.070588 18.070588 0 0 0 31.322353 12.227765l202.992941-219.497412z" fill="#1296db" p-id="18846"></path> </svg>
  </div>
  
  <div class="changed">
    Hex: 
    
    <div id="hex">
    </div>
    
    <div id="hexShow">
    </div>
  </div>
</div>

<div class="r-h">
  <div class="inValue">
    #<input name="hex" type="text" value="000000" maxlength="6" />
  </div>
  
  <div id="hex2rgb">
    <svg t="1573902941567" class="icon" viewBox="0 0 1325 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="18840" width="32" height="32"> <path d="M46.501647 294.550588a45.176471 45.176471 0 1 1 0-90.352941H392.131765a45.176471 45.176471 0 0 1 0 90.352941H46.381176zM758.302118 841.788235a45.176471 45.176471 0 1 1 0-90.352941h355.689411a45.176471 45.176471 0 0 1 0 90.352941H758.362353z" fill="#1296db" p-id="18841"></path> <path d="M364.303059 273.648941a45.176471 45.176471 0 1 1 75.715765-49.332706L544.527059 384.602353a45.176471 45.176471 0 1 1-75.65553 49.392941L364.303059 273.588706z m248.95247 382.012235a45.176471 45.176471 0 1 1 75.715765-49.392941l105.773177 162.394353a45.176471 45.176471 0 0 1-75.65553 49.332706l-105.833412-162.334118z" fill="#1296db" p-id="18842"></path> <path d="M1301.684706 796.611765l-202.992941 219.557647a18.070588 18.070588 0 0 1-31.322353-12.288V589.342118a18.070588 18.070588 0 0 1 31.322353-12.288l202.992941 219.557647z" fill="#1296db" p-id="18843"></path> <path d="M46.501647 747.941647a45.176471 45.176471 0 1 0 0 90.352941H392.131765a45.176471 45.176471 0 1 0 0-90.352941H46.381176zM758.302118 200.824471a45.176471 45.176471 0 1 0 0 90.352941h355.689411a45.176471 45.176471 0 0 0 0-90.352941H758.362353z" fill="#1296db" p-id="18844"></path> <path d="M364.303059 768.903529a45.176471 45.176471 0 1 0 75.715765 49.392942l354.785882-544.406589a45.176471 45.176471 0 0 0-75.715765-49.332706l-354.785882 544.346353z" fill="#1296db" p-id="18845"></path> <path d="M1301.684706 246.000941L1098.691765 26.443294a18.070588 18.070588 0 0 0-31.322353 12.227765v414.599529a18.070588 18.070588 0 0 0 31.322353 12.227765l202.992941-219.497412z" fill="#1296db" p-id="18846"></path> </svg>
  </div>
  
  <div class="changed">
    RGB: 
    
    <div id="rgb">
    </div>
    
    <div id="rgbShow">
    </div>
  </div>
</div>

## 颜色表 {#allColor}

<div class="table-head">
  <div class="daohang" style="display: flex;flex-wrap: wrap;justify-content: center;">
    <select id="chooseChart"> <option value="140">WEB标准颜色</option> <option value="342">342种WEB颜色</option> </select> 
    
    <div style="margin: 0 15px;">
      显示方式 <select id="selectShow"> <option value="6">纵向6列</option> <option value="3">纵向3列</option> <option value="1">纵向1列</option> <option value="13">横向3列</option> <option value="16">横向6列</option> </select>
    </div>
  </div>
  
  <div id="web-dao" class="daohang">
    导航标签： <a href="#blacks">黑色调(Blacks)</a> &#8211; <a href="#grays">灰色调(Grays)</a> &#8211; <a href="#blues">蓝色调(Blues)</a> &#8211; <a href="#greens">绿色调(Greens)</a> &#8211; <a href="#yellows">黄色调(Yellows)</a> &#8211; <a href="#browns">棕色调(Browns)</a> &#8211; <a href="#oranges">橙色调(Orange)</a> &#8211; <a href="#reds">红色调(Reds)</a> &#8211; <a href="#pinks">粉色调(Pinks)</a> &#8211; <a href="#purples">紫色调(Purples)</a>
  </div>
  
  <div id="it-dao" class="daohang" style="display: none;">
    导航标签： <a href="#black">黑色调(Blacks)</a> &#8211; <a href="#gray">灰色调(Grays)</a> &#8211; <a href="#blue">蓝色调(Blues)</a> &#8211; <a href="#green">绿色调(Greens)</a> &#8211; <a href="#yellow">黄色调(Yellows)</a> &#8211; <a href="#brown">棕色调(Browns)</a> &#8211; <a href="#orange">橙色调(Orange)</a> &#8211; <a href="#red">红色调(Reds)</a> &#8211; <a href="#pink">粉色调(Pinks)</a> &#8211; <a href="#purple">紫色调(Purples)</a>
  </div>
</div>

<table class="tableborder" cellspacing="5" cellpadding="5" border="0" style="width: 100%;table-layout:fixed;">
  <tr>
    <td class="tdborder" bgcolor="#000000" id="black">
      <font color="#ffffff"> 
      
      <div class="name">
        Black
      </div>
      
      <div class="name">
        黑色
      </div>
      
      <div>
        #000000
      </div>
      
      <div>
        rgb(0,0,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#2b65ec">
      <font color="#ffffff"> 
      
      <div class="name">
        OceanBlue
      </div>
      
      <div class="name">
        海洋蓝
      </div>
      
      <div>
        #2b65ec
      </div>
      
      <div>
        rgb(43,101,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#728c00">
      <font color="#ffffff"> 
      
      <div class="name">
        VenomGreen
      </div>
      
      <div class="name">
        毒液绿
      </div>
      
      <div>
        #728c00
      </div>
      
      <div>
        rgb(114,140,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f7e7ce">
      <font color="#000000"> 
      
      <div class="name">
        Champagne
      </div>
      
      <div class="name">
        香槟色
      </div>
      
      <div>
        #f7e7ce
      </div>
      
      <div>
        rgb(247,231,206)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ff7f50">
      <font color="#ffffff"> 
      
      <div class="name">
        Coral
      </div>
      
      <div class="name">
        珊瑚色
      </div>
      
      <div>
        #ff7f50
      </div>
      
      <div>
        rgb(255,127,80)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f6358a">
      <font color="#ffffff"> 
      
      <div class="name">
        VioletRed
      </div>
      
      <div class="name">
        紫红色
      </div>
      
      <div>
        #f6358a
      </div>
      
      <div>
        rgb(246,53,138)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#0c090a">
      <font color="#ffffff"> 
      
      <div class="name">
        Night
      </div>
      
      <div class="name">
        夜黑
      </div>
      
      <div>
        #0c090a
      </div>
      
      <div>
        rgb(12,9,10)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#306eff">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueRibbon
      </div>
      
      <div class="name">
        蓝丝带蓝
      </div>
      
      <div>
        #306eff
      </div>
      
      <div>
        rgb(48,110,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#667c26">
      <font color="#ffffff"> 
      
      <div class="name">
        FernGreen
      </div>
      
      <div class="name">
        蕨绿色
      </div>
      
      <div>
        #667c26
      </div>
      
      <div>
        rgb(102,124,38)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffebcd">
      <font color="#000000"> 
      
      <div class="name">
        BlanchedAlmond
      </div>
      
      <div class="name">
        杏仁白
      </div>
      
      <div>
        #ffebcd
      </div>
      
      <div>
        rgb(255,235,205)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f88158">
      <font color="#ffffff"> 
      
      <div class="name">
        BasketBallOrange
      </div>
      
      <div class="name">
        篮球橙
      </div>
      
      <div>
        #f88158
      </div>
      
      <div>
        rgb(248,129,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f52887">
      <font color="#ffffff"> 
      
      <div class="name">
        DeepPink
      </div>
      
      <div class="name">
        深粉红色
      </div>
      
      <div>
        #f52887
      </div>
      
      <div>
        rgb(245,40,135)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2c3539">
      <font color="#ffffff"> 
      
      <div class="name">
        Gunmetal
      </div>
      
      <div class="name">
        青铜色
      </div>
      
      <div>
        #2c3539
      </div>
      
      <div>
        rgb(44,53,57)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#157dec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueDress
      </div>
      
      <div class="name">
        蓝色礼服色
      </div>
      
      <div>
        #157dec
      </div>
      
      <div>
        rgb(21,125,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#254117">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkForestGreen
      </div>
      
      <div class="name">
        暗森林绿
      </div>
      
      <div>
        #254117
      </div>
      
      <div>
        rgb(37,65,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f3e5ab">
      <font color="#000000"> 
      
      <div class="name">
        Vanilla
      </div>
      
      <div class="name">
        香草绿
      </div>
      
      <div>
        #f3e5ab
      </div>
      
      <div>
        rgb(243,229,171)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f9966b">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSalmon
      </div>
      
      <div class="name">
        亮鮭紅
      </div>
      
      <div>
        #f9966b
      </div>
      
      <div>
        rgb(249,150,107)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e45e9d">
      <font color="#ffffff"> 
      
      <div class="name">
        PinkCupcake
      </div>
      
      <div class="name">
        粉红玫瑰色
      </div>
      
      <div>
        #e45e9d
      </div>
      
      <div>
        rgb(228,94,157)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2b1b17">
      <font color="#ffffff"> 
      
      <div class="name">
        Midnight
      </div>
      
      <div class="name">
        深黑
      </div>
      
      <div>
        #2b1b17
      </div>
      
      <div>
        rgb(43,27,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#1589ff">
      <font color="#ffffff"> 
      
      <div class="name">
        DodgerBlue
      </div>
      
      <div class="name">
        道奇蓝
      </div>
      
      <div>
        #1589ff
      </div>
      
      <div>
        rgb(21,137,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#306754">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumSeaGreen
      </div>
      
      <div class="name">
        中海洋绿
      </div>
      
      <div>
        #306754
      </div>
      
      <div>
        rgb(48,103,84)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ece5b6">
      <font color="#000000"> 
      
      <div class="name">
        TanBrown
      </div>
      
      <div class="name">
        棕褐色
      </div>
      
      <div>
        #ece5b6
      </div>
      
      <div>
        rgb(236,229,182)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e78a61">
      <font color="#ffffff"> 
      
      <div class="name">
        Tangerine
      </div>
      
      <div class="name">
        橘红色
      </div>
      
      <div>
        #e78a61
      </div>
      
      <div>
        rgb(231,138,97)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e4287c">
      <font color="#ffffff"> 
      
      <div class="name">
        PinkLemonade
      </div>
      
      <div class="name">
        粉柠色
      </div>
      
      <div>
        #e4287c
      </div>
      
      <div>
        rgb(228,40,124)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#34282c">
      <font color="#ffffff"> 
      
      <div class="name">
        Charcoal
      </div>
      
      <div class="name">
        炭黑
      </div>
      
      <div>
        #34282c
      </div>
      
      <div>
        rgb(52,40,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6495ed">
      <font color="#ffffff"> 
      
      <div class="name">
        CornflowerBlue
      </div>
      
      <div class="name">
        矢车菊蓝
      </div>
      
      <div>
        #6495ed
      </div>
      
      <div>
        rgb(100,149,237)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#347235">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumForestGreen
      </div>
      
      <div class="name">
        中森林绿
      </div>
      
      <div>
        #347235
      </div>
      
      <div>
        rgb(52,114,53)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffe5b4">
      <font color="#000000"> 
      
      <div class="name">
        Peach
      </div>
      
      <div class="name">
        桃色
      </div>
      
      <div>
        #ffe5b4
      </div>
      
      <div>
        rgb(255,229,180)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e18b6b">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSalmon
      </div>
      
      <div class="name">
        暗肉色
      </div>
      
      <div>
        #e18b6b
      </div>
      
      <div>
        rgb(225,139,107)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f535aa">
      <font color="#ffffff"> 
      
      <div class="name">
        NeonPink
      </div>
      
      <div class="name">
        霓虹粉
      </div>
      
      <div>
        #f535aa
      </div>
      
      <div>
        rgb(245,53,170)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#25383c">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSlateGrey
      </div>
      
      <div class="name">
        暗岩灰
      </div>
      
      <div>
        #25383c
      </div>
      
      <div>
        rgb(37,56,60)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6698ff">
      <font color="#ffffff"> 
      
      <div class="name">
        SkyBlue
      </div>
      
      <div class="name">
        天蓝色
      </div>
      
      <div>
        #6698ff
      </div>
      
      <div>
        rgb(102,152,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#437c17">
      <font color="#ffffff"> 
      
      <div class="name">
        SeaweedGreen
      </div>
      
      <div class="name">
        海藻绿
      </div>
      
      <div>
        #437c17
      </div>
      
      <div>
        rgb(67,124,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffdb58">
      <font color="#ffffff"> 
      
      <div class="name">
        Mustard
      </div>
      
      <div class="name">
        芥末黄
      </div>
      
      <div>
        #ffdb58
      </div>
      
      <div>
        rgb(255,219,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e77471">
      <font color="#ffffff"> 
      
      <div class="name">
        LightCoral
      </div>
      
      <div class="name">
        浅橘红色
      </div>
      
      <div>
        #e77471
      </div>
      
      <div>
        rgb(231,116,113)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ff00ff">
      <font color="#ffffff"> 
      
      <div class="name">
        Magenta
      </div>
      
      <div class="name">
        品红
      </div>
      
      <div>
        #ff00ff
      </div>
      
      <div>
        rgb(255,0,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#3b3131">
      <font color="#ffffff"> 
      
      <div class="name">
        Oil
      </div>
      
      <div class="name">
        油黑
      </div>
      
      <div>
        #3b3131
      </div>
      
      <div>
        rgb(59,49,49)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#38acec">
      <font color="#ffffff"> 
      
      <div class="name">
        ButterflyBlue
      </div>
      
      <div class="name">
        蝴蝶蓝
      </div>
      
      <div>
        #38acec
      </div>
      
      <div>
        rgb(56,172,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#387c44">
      <font color="#ffffff"> 
      
      <div class="name">
        PineGreen
      </div>
      
      <div class="name">
        松绿色
      </div>
      
      <div>
        #387c44
      </div>
      
      <div>
        rgb(56,124,68)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffd801">
      <font color="#ffffff"> 
      
      <div class="name">
        RubberDuckyYellow
      </div>
      
      <div class="name">
        橡胶鸭黄
      </div>
      
      <div>
        #ffd801
      </div>
      
      <div>
        rgb(255,216,1)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f75d59">
      <font color="#ffffff"> 
      
      <div class="name">
        BeanRed
      </div>
      
      <div class="name">
        豆红
      </div>
      
      <div>
        #f75d59
      </div>
      
      <div>
        rgb(247,93,89)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e3319d">
      <font color="#ffffff"> 
      
      <div class="name">
        DimorphothecaMagenta
      </div>
      
      <div class="name">
        紫红色魔芋
      </div>
      
      <div>
        #e3319d
      </div>
      
      <div>
        rgb(227,49,157)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#413839">
      <font color="#ffffff"> 
      
      <div class="name">
        BlackCat
      </div>
      
      <div class="name">
        猫黑
      </div>
      
      <div>
        #413839
      </div>
      
      <div>
        rgb(65,56,57)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#56a5ec">
      <font color="#ffffff"> 
      
      <div class="name">
        Iceberg
      </div>
      
      <div class="name">
        冰山白
      </div>
      
      <div>
        #56a5ec
      </div>
      
      <div>
        rgb(86,165,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#347c2c">
      <font color="#ffffff"> 
      
      <div class="name">
        JungleGreen
      </div>
      
      <div class="name">
        丛林绿
      </div>
      
      <div>
        #347c2c
      </div>
      
      <div>
        rgb(52,124,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fdd017">
      <font color="#ffffff"> 
      
      <div class="name">
        BrightGold
      </div>
      
      <div class="name">
        亮金
      </div>
      
      <div>
        #fdd017
      </div>
      
      <div>
        rgb(253,208,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e55451">
      <font color="#ffffff"> 
      
      <div class="name">
        ValentineRed
      </div>
      
      <div class="name">
        情人红
      </div>
      
      <div>
        #e55451
      </div>
      
      <div>
        rgb(229,84,81)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f433ff">
      <font color="#ffffff"> 
      
      <div class="name">
        BrightNeonPink
      </div>
      
      <div class="name">
        亮霓虹粉
      </div>
      
      <div>
        #f433ff
      </div>
      
      <div>
        rgb(244,51,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#3d3c3a">
      <font color="#ffffff"> 
      
      <div class="name">
        Iridium
      </div>
      
      <div class="name">
        铱白
      </div>
      
      <div>
        #3d3c3a
      </div>
      
      <div>
        rgb(61,60,58)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5cb3ff">
      <font color="#ffffff"> 
      
      <div class="name">
        CrystalBlue
      </div>
      
      <div class="name">
        水晶蓝
      </div>
      
      <div>
        #5cb3ff
      </div>
      
      <div>
        rgb(92,179,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#347c17">
      <font color="#ffffff"> 
      
      <div class="name">
        ShamrockGreen
      </div>
      
      <div class="name">
        三叶草绿色
      </div>
      
      <div>
        #347c17
      </div>
      
      <div>
        rgb(52,124,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#eac117" id="brown">
      <font color="#ffffff"> 
      
      <div class="name">
        Goldenbrown
      </div>
      
      <div class="name">
        金黄色
      </div>
      
      <div>
        #eac117
      </div>
      
      <div>
        rgb(234,193,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e55b3c">
      <font color="#ffffff"> 
      
      <div class="name">
        ShockingOrange
      </div>
      
      <div class="name">
        鲜橙色
      </div>
      
      <div>
        #e55b3c
      </div>
      
      <div>
        rgb(229,91,60)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#d16587">
      <font color="#ffffff"> 
      
      <div class="name">
        PaleVioletRed
      </div>
      
      <div class="name">
        浅紫红色
      </div>
      
      <div>
        #d16587
      </div>
      
      <div>
        rgb(209,101,135)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#463e3f">
      <font color="#ffffff"> 
      
      <div class="name">
        BlackEel
      </div>
      
      <div class="name">
        鳗黑
      </div>
      
      <div>
        #463e3f
      </div>
      
      <div>
        rgb(70,62,63)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#3bb9ff">
      <font color="#ffffff"> 
      
      <div class="name">
        DeepSkyBlue
      </div>
      
      <div class="name">
        深天蓝色
      </div>
      
      <div>
        #3bb9ff
      </div>
      
      <div>
        rgb(59,185,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#348017">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumSpringGreen
      </div>
      
      <div class="name">
        间春绿
      </div>
      
      <div>
        #348017
      </div>
      
      <div>
        rgb(52,128,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f2bb66">
      <font color="#ffffff"> 
      
      <div class="name">
        MacaroniandCheese
      </div>
      
      <div class="name">
        乳黄
      </div>
      
      <div>
        #f2bb66
      </div>
      
      <div>
        rgb(242,187,102)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ff0000" id="red">
      <font color="#ffffff"> 
      
      <div class="name">
        Red
      </div>
      
      <div class="name">
        红色
      </div>
      
      <div>
        #ff0000
      </div>
      
      <div>
        rgb(255,0,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c25a7c">
      <font color="#ffffff"> 
      
      <div class="name">
        TulipPink
      </div>
      
      <div class="name">
        郁金香粉
      </div>
      
      <div>
        #c25a7c
      </div>
      
      <div>
        rgb(194,90,124)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#4c4646">
      <font color="#ffffff"> 
      
      <div class="name">
        BlackCow
      </div>
      
      <div class="name">
        牛黑色
      </div>
      
      <div>
        #4c4646
      </div>
      
      <div>
        rgb(76,70,70)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#79baec">
      <font color="#ffffff"> 
      
      <div class="name">
        DenimBlue
      </div>
      
      <div class="name">
        牛仔蓝
      </div>
      
      <div>
        #79baec
      </div>
      
      <div>
        rgb(121,186,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4e9258">
      <font color="#ffffff"> 
      
      <div class="name">
        ForestGreen
      </div>
      
      <div class="name">
        森林绿
      </div>
      
      <div>
        #4e9258
      </div>
      
      <div>
        rgb(78,146,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fbb917">
      <font color="#ffffff"> 
      
      <div class="name">
        Saffron
      </div>
      
      <div class="name">
        藏红花色
      </div>
      
      <div>
        #fbb917
      </div>
      
      <div>
        rgb(251,185,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ff2400">
      <font color="#ffffff"> 
      
      <div class="name">
        Scarlet
      </div>
      
      <div class="name">
        猩红
      </div>
      
      <div>
        #ff2400
      </div>
      
      <div>
        rgb(255,36,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ca226b">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumVioletRed
      </div>
      
      <div class="name">
        间紫罗兰色
      </div>
      
      <div>
        #ca226b
      </div>
      
      <div>
        rgb(202,34,107)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#504a4b" id="gray">
      <font color="#ffffff"> 
      
      <div class="name">
        GrayWolf
      </div>
      
      <div class="name">
        狼灰色
      </div>
      
      <div>
        #504a4b
      </div>
      
      <div>
        rgb(80,74,75)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#82cafa">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSkyBlue
      </div>
      
      <div class="name">
        浅天蓝色
      </div>
      
      <div>
        #82cafa
      </div>
      
      <div>
        rgb(130,202,250)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6aa121">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenOnion
      </div>
      
      <div class="name">
        葱绿
      </div>
      
      <div>
        #6aa121
      </div>
      
      <div>
        rgb(106,161,33)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fbb117">
      <font color="#ffffff"> 
      
      <div class="name">
        Beer
      </div>
      
      <div class="name">
        啤酒黄
      </div>
      
      <div>
        #fbb117
      </div>
      
      <div>
        rgb(251,177,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f62217">
      <font color="#ffffff"> 
      
      <div class="name">
        RubyRed
      </div>
      
      <div class="name">
        宝石红
      </div>
      
      <div>
        #f62217
      </div>
      
      <div>
        rgb(246,34,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c12869">
      <font color="#ffffff"> 
      
      <div class="name">
        RoguePink
      </div>
      
      <div class="name">
        胭脂粉
      </div>
      
      <div>
        #c12869
      </div>
      
      <div>
        rgb(193,40,105)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#565051">
      <font color="#ffffff"> 
      
      <div class="name">
        VampireGray
      </div>
      
      <div class="name">
        死灰色
      </div>
      
      <div>
        #565051
      </div>
      
      <div>
        rgb(86,80,81)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#82caff">
      <font color="#ffffff"> 
      
      <div class="name">
        DaySkyBlue
      </div>
      
      <div class="name">
        天蓝色
      </div>
      
      <div>
        #82caff
      </div>
      
      <div>
        rgb(130,202,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4aa02c">
      <font color="#ffffff"> 
      
      <div class="name">
        SpringGreen
      </div>
      
      <div class="name">
        春绿色
      </div>
      
      <div>
        #4aa02c
      </div>
      
      <div>
        rgb(74,160,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffa62f">
      <font color="#ffffff"> 
      
      <div class="name">
        Cantaloupe
      </div>
      
      <div class="name">
        哈密​​瓜色
      </div>
      
      <div>
        #ffa62f
      </div>
      
      <div>
        rgb(255,166,47)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f70d1a">
      <font color="#ffffff"> 
      
      <div class="name">
        FerrariRed
      </div>
      
      <div class="name">
        法拉利红
      </div>
      
      <div>
        #f70d1a
      </div>
      
      <div>
        rgb(247,13,26)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c12267">
      <font color="#ffffff"> 
      
      <div class="name">
        BurntPink
      </div>
      
      <div class="name">
        暗粉红
      </div>
      
      <div>
        #c12267
      </div>
      
      <div>
        rgb(193,34,103)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#5c5858">
      <font color="#ffffff"> 
      
      <div class="name">
        GrayDolphin
      </div>
      
      <div class="name">
        海豚灰
      </div>
      
      <div>
        #5c5858
      </div>
      
      <div>
        rgb(92,88,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#a0cfec">
      <font color="#ffffff"> 
      
      <div class="name">
        JeansBlue
      </div>
      
      <div class="name">
        牛仔裤蓝
      </div>
      
      <div>
        #a0cfec
      </div>
      
      <div>
        rgb(160,207,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#41a317">
      <font color="#ffffff"> 
      
      <div class="name">
        LimeGreen
      </div>
      
      <div class="name">
        柠檬绿
      </div>
      
      <div>
        #41a317
      </div>
      
      <div>
        rgb(65,163,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e9ab17">
      <font color="#ffffff"> 
      
      <div class="name">
        BeeYellow
      </div>
      
      <div class="name">
        蜜蜂黄
      </div>
      
      <div>
        #e9ab17
      </div>
      
      <div>
        rgb(233,171,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f62817">
      <font color="#ffffff"> 
      
      <div class="name">
        FireEngineRed
      </div>
      
      <div class="name">
        消防车红
      </div>
      
      <div>
        #f62817
      </div>
      
      <div>
        rgb(246,40,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c25283">
      <font color="#ffffff"> 
      
      <div class="name">
        BashfulPink
      </div>
      
      <div class="name">
        奶粉色
      </div>
      
      <div>
        #c25283
      </div>
      
      <div>
        rgb(194,82,131)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#625d5d">
      <font color="#ffffff"> 
      
      <div class="name">
        CarbonGray
      </div>
      
      <div class="name">
        碳灰色
      </div>
      
      <div>
        #625d5d
      </div>
      
      <div>
        rgb(98,93,93)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b7ceec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueAngel
      </div>
      
      <div class="name">
        蓝天使蓝
      </div>
      
      <div>
        #b7ceec
      </div>
      
      <div>
        rgb(183,206,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#3ea055">
      <font color="#ffffff"> 
      
      <div class="name">
        CloverGreen
      </div>
      
      <div class="name">
        三叶草绿
      </div>
      
      <div>
        #3ea055
      </div>
      
      <div>
        rgb(62,160,85)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e2a76f">
      <font color="#ffffff"> 
      
      <div class="name">
        BrownSugar
      </div>
      
      <div class="name">
        糖红
      </div>
      
      <div>
        #e2a76f
      </div>
      
      <div>
        rgb(226,167,111)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e42217">
      <font color="#ffffff"> 
      
      <div class="name">
        LavaRed
      </div>
      
      <div class="name">
        熔岩红
      </div>
      
      <div>
        #e42217
      </div>
      
      <div>
        rgb(228,34,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c12283">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkCarnationPink
      </div>
      
      <div class="name">
        深康乃馨粉
      </div>
      
      <div>
        #c12283
      </div>
      
      <div>
        rgb(193,34,131)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#666362">
      <font color="#ffffff"> 
      
      <div class="name">
        AshGray
      </div>
      
      <div class="name">
        烟灰色
      </div>
      
      <div>
        #666362
      </div>
      
      <div>
        rgb(102,99,98)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b4cfec">
      <font color="#ffffff"> 
      
      <div class="name">
        PastelBlue
      </div>
      
      <div class="name">
        淡蓝色
      </div>
      
      <div>
        #b4cfec
      </div>
      
      <div>
        rgb(180,207,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6cbb3c">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenSnake
      </div>
      
      <div class="name">
        蛇青
      </div>
      
      <div>
        #6cbb3c
      </div>
      
      <div>
        rgb(108,187,60)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#deb887">
      <font color="#ffffff"> 
      
      <div class="name">
        BurlyWood
      </div>
      
      <div class="name">
        实木色
      </div>
      
      <div>
        #deb887
      </div>
      
      <div>
        rgb(222,184,135)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e41b17">
      <font color="#ffffff"> 
      
      <div class="name">
        LoveRed
      </div>
      
      <div class="name">
        爱心红
      </div>
      
      <div>
        #e41b17
      </div>
      
      <div>
        rgb(228,27,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b93b8f">
      <font color="#ffffff"> 
      
      <div class="name">
        Plum
      </div>
      
      <div class="name">
        杨李色
      </div>
      
      <div>
        #b93b8f
      </div>
      
      <div>
        rgb(185,59,143)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#6d6968">
      <font color="#ffffff"> 
      
      <div class="name">
        CloudyGray
      </div>
      
      <div class="name">
        云灰色
      </div>
      
      <div>
        #6d6968
      </div>
      
      <div>
        rgb(109,105,104)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c2dfff">
      <font color="#ffffff"> 
      
      <div class="name">
        SeaBlue
      </div>
      
      <div class="name">
        海蓝
      </div>
      
      <div>
        #c2dfff
      </div>
      
      <div>
        rgb(194,223,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6cc417">
      <font color="#ffffff"> 
      
      <div class="name">
        AlienGreen
      </div>
      
      <div class="name">
        外星绿
      </div>
      
      <div>
        #6cc417
      </div>
      
      <div>
        rgb(108,196,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffcba4">
      <font color="#ffffff"> 
      
      <div class="name">
        DeepPeach
      </div>
      
      <div class="name">
        深桃色
      </div>
      
      <div>
        #ffcba4
      </div>
      
      <div>
        rgb(255,203,164)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#dc381f">
      <font color="#ffffff"> 
      
      <div class="name">
        Grapefruit
      </div>
      
      <div class="name">
        葡萄柚色
      </div>
      
      <div>
        #dc381f
      </div>
      
      <div>
        rgb(220,56,31)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7e587e" id="purple">
      <font color="#ffffff"> 
      
      <div class="name">
        ViolaPurple
      </div>
      
      <div class="name">
        三色堇紫
      </div>
      
      <div>
        #7e587e
      </div>
      
      <div>
        rgb(126,88,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#726e6d">
      <font color="#ffffff"> 
      
      <div class="name">
        SmokeyGray
      </div>
      
      <div class="name">
        烟灰色
      </div>
      
      <div>
        #726e6d
      </div>
      
      <div>
        rgb(114,110,109)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c6deff">
      <font color="#ffffff"> 
      
      <div class="name">
        PowderBlue
      </div>
      
      <div class="name">
        粉蓝色
      </div>
      
      <div>
        #c6deff
      </div>
      
      <div>
        rgb(198,222,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4cc417">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenApple
      </div>
      
      <div class="name">
        苹果青
      </div>
      
      <div>
        #4cc417
      </div>
      
      <div>
        rgb(76,196,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c9be62">
      <font color="#ffffff"> 
      
      <div class="name">
        GingerBrown
      </div>
      
      <div class="name">
        姜棕色
      </div>
      
      <div>
        #c9be62
      </div>
      
      <div>
        rgb(201,190,98)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c34a2c">
      <font color="#ffffff"> 
      
      <div class="name">
        ChestnutRed
      </div>
      
      <div class="name">
        栗红色
      </div>
      
      <div>
        #c34a2c
      </div>
      
      <div>
        rgb(195,74,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#571b7e">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleIris
      </div>
      
      <div class="name">
        鸢尾紫
      </div>
      
      <div>
        #571b7e
      </div>
      
      <div>
        rgb(87,27,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#736f6e">
      <font color="#ffffff"> 
      
      <div class="name">
        Gray
      </div>
      
      <div class="name">
        灰色
      </div>
      
      <div>
        #736f6e
      </div>
      
      <div>
        rgb(115,111,110)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#afdcec">
      <font color="#ffffff"> 
      
      <div class="name">
        CoralBlue
      </div>
      
      <div class="name">
        珊瑚蓝
      </div>
      
      <div>
        #afdcec
      </div>
      
      <div>
        rgb(175,220,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#52d017">
      <font color="#ffffff"> 
      
      <div class="name">
        YellowGreen
      </div>
      
      <div class="name">
        黄绿色
      </div>
      
      <div>
        #52d017
      </div>
      
      <div>
        rgb(82,208,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e8a317">
      <font color="#ffffff"> 
      
      <div class="name">
        SchoolBusYellow
      </div>
      
      <div class="name">
        校车黄
      </div>
      
      <div>
        #e8a317
      </div>
      
      <div>
        rgb(232,163,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c24641">
      <font color="#ffffff"> 
      
      <div class="name">
        CherryRed
      </div>
      
      <div class="name">
        樱桃红
      </div>
      
      <div>
        #c24641
      </div>
      
      <div>
        rgb(194,70,65)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#583759">
      <font color="#ffffff"> 
      
      <div class="name">
        PlumPurple
      </div>
      
      <div class="name">
        梅紫色
      </div>
      
      <div>
        #583759
      </div>
      
      <div>
        rgb(88,55,89)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#837e7c">
      <font color="#ffffff"> 
      
      <div class="name">
        Granite
      </div>
      
      <div class="name">
        花岗岩灰
      </div>
      
      <div>
        #837e7c
      </div>
      
      <div>
        rgb(131,126,124)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#addfff">
      <font color="#ffffff"> 
      
      <div class="name">
        LightBlue
      </div>
      
      <div class="name">
        浅蓝
      </div>
      
      <div>
        #addfff
      </div>
      
      <div>
        rgb(173,223,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4cc552">
      <font color="#ffffff"> 
      
      <div class="name">
        KellyGreen
      </div>
      
      <div class="name">
        鲜黄绿色
      </div>
      
      <div>
        #4cc552
      </div>
      
      <div>
        rgb(76,197,82)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ee9a4d">
      <font color="#ffffff"> 
      
      <div class="name">
        SandyBrown
      </div>
      
      <div class="name">
        沙棕色
      </div>
      
      <div>
        #ee9a4d
      </div>
      
      <div>
        rgb(238,154,77)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c04000">
      <font color="#ffffff"> 
      
      <div class="name">
        Mahogany
      </div>
      
      <div class="name">
        桃花心木棕色
      </div>
      
      <div>
        #c04000
      </div>
      
      <div>
        rgb(192,64,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4b0082">
      <font color="#ffffff"> 
      
      <div class="name">
        Indigo
      </div>
      
      <div class="name">
        靛青
      </div>
      
      <div>
        #4b0082
      </div>
      
      <div>
        rgb(75,0,130)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#848482">
      <font color="#ffffff"> 
      
      <div class="name">
        BattleshipGray
      </div>
      
      <div class="name">
        战列舰色
      </div>
      
      <div>
        #848482
      </div>
      
      <div>
        rgb(132,132,130)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#bdedff">
      <font color="#ffffff"> 
      
      <div class="name">
        RobinEggBlue
      </div>
      
      <div class="name">
        罗宾鸟蛋蓝
      </div>
      
      <div>
        #bdedff
      </div>
      
      <div>
        rgb(189,237,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#54c571">
      <font color="#ffffff"> 
      
      <div class="name">
        ZombieGreen
      </div>
      
      <div class="name">
        僵尸绿
      </div>
      
      <div>
        #54c571
      </div>
      
      <div>
        rgb(84,197,113)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c8b560">
      <font color="#ffffff"> 
      
      <div class="name">
        FallLeafBrown
      </div>
      
      <div class="name">
        秋叶棕
      </div>
      
      <div>
        #c8b560
      </div>
      
      <div>
        rgb(200,181,96)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c11b17">
      <font color="#ffffff"> 
      
      <div class="name">
        ChilliPepper
      </div>
      
      <div class="name">
        辣椒红
      </div>
      
      <div>
        #c11b17
      </div>
      
      <div>
        rgb(193,27,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#461b7e">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleMonster
      </div>
      
      <div class="name">
        怪物紫
      </div>
      
      <div>
        #461b7e
      </div>
      
      <div>
        rgb(70,27,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#b6b6b4">
      <font color="#ffffff"> 
      
      <div class="name">
        GrayCloud
      </div>
      
      <div class="name">
        灰云灰
      </div>
      
      <div>
        #b6b6b4
      </div>
      
      <div>
        rgb(182,182,180)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#cfecec">
      <font color="#000000"> 
      
      <div class="name">
        PaleBlueLily
      </div>
      
      <div class="name">
        淡百合蓝
      </div>
      
      <div>
        #cfecec
      </div>
      
      <div>
        rgb(207,236,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#99c68e">
      <font color="#ffffff"> 
      
      <div class="name">
        FrogGreen
      </div>
      
      <div class="name">
        青蛙绿
      </div>
      
      <div>
        #99c68e
      </div>
      
      <div>
        rgb(153,198,142)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#d4a017">
      <font color="#ffffff"> 
      
      <div class="name">
        OrangeGold
      </div>
      
      <div class="name">
        橙金
      </div>
      
      <div>
        #d4a017
      </div>
      
      <div>
        rgb(212,160,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9f000f">
      <font color="#ffffff"> 
      
      <div class="name">
        Cranberry
      </div>
      
      <div class="name">
        蔓越莓红
      </div>
      
      <div>
        #9f000f
      </div>
      
      <div>
        rgb(159,0,15)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4e387e">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleHaze
      </div>
      
      <div class="name">
        浅紫色
      </div>
      
      <div>
        #4e387e
      </div>
      
      <div>
        rgb(78,56,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#d1d0ce">
      <font color="#ffffff"> 
      
      <div class="name">
        GrayGoose
      </div>
      
      <div class="name">
        鹅灰
      </div>
      
      <div>
        #d1d0ce
      </div>
      
      <div>
        rgb(209,208,206)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e0ffff">
      <font color="#000000"> 
      
      <div class="name">
        LightCyan
      </div>
      
      <div class="name">
        浅青色
      </div>
      
      <div>
        #e0ffff
      </div>
      
      <div>
        rgb(224,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#89c35c">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenPeas
      </div>
      
      <div class="name">
        豆青
      </div>
      
      <div>
        #89c35c
      </div>
      
      <div>
        rgb(137,195,92)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c2b280">
      <font color="#ffffff"> 
      
      <div class="name">
        Sand
      </div>
      
      <div class="name">
        砂色
      </div>
      
      <div>
        #c2b280
      </div>
      
      <div>
        rgb(194,178,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#990012">
      <font color="#ffffff"> 
      
      <div class="name">
        RedWine
      </div>
      
      <div class="name">
        酒红色
      </div>
      
      <div>
        #990012
      </div>
      
      <div>
        rgb(153,0,18)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#614051">
      <font color="#ffffff"> 
      
      <div class="name">
        Eggplant
      </div>
      
      <div class="name">
        茄子紫
      </div>
      
      <div>
        #614051
      </div>
      
      <div>
        rgb(97,64,81)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#e5e4e2">
      <font color="#000000"> 
      
      <div class="name">
        Platinum
      </div>
      
      <div class="name">
        铂白
      </div>
      
      <div>
        #e5e4e2
      </div>
      
      <div>
        rgb(229,228,226)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ebf4fa">
      <font color="#000000"> 
      
      <div class="name">
        Water
      </div>
      
      <div class="name">
        水白
      </div>
      
      <div>
        #ebf4fa
      </div>
      
      <div>
        rgb(235,244,250)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#85bb65">
      <font color="#ffffff"> 
      
      <div class="name">
        DollarBillGreen
      </div>
      
      <div class="name">
        美元绿
      </div>
      
      <div>
        #85bb65
      </div>
      
      <div>
        rgb(133,187,101)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c7a317">
      <font color="#ffffff"> 
      
      <div class="name">
        CookieBrown
      </div>
      
      <div class="name">
        曲奇棕
      </div>
      
      <div>
        #c7a317
      </div>
      
      <div>
        rgb(199,163,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8c001a">
      <font color="#ffffff"> 
      
      <div class="name">
        Burgundy
      </div>
      
      <div class="name">
        勃艮第酒红
      </div>
      
      <div>
        #8c001a
      </div>
      
      <div>
        rgb(140,0,26)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5e5a80">
      <font color="#ffffff"> 
      
      <div class="name">
        Grape
      </div>
      
      <div class="name">
        葡萄紫
      </div>
      
      <div>
        #5e5a80
      </div>
      
      <div>
        rgb(94,90,128)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#bcc6cc">
      <font color="#ffffff"> 
      
      <div class="name">
        MetallicSilver
      </div>
      
      <div class="name">
        金属银
      </div>
      
      <div>
        #bcc6cc
      </div>
      
      <div>
        rgb(188,198,204)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f0f8ff">
      <font color="#000000"> 
      
      <div class="name">
        AliceBlue
      </div>
      
      <div class="name">
        爱丽丝蓝
      </div>
      
      <div>
        #f0f8ff
      </div>
      
      <div>
        rgb(240,248,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8bb381">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSeaGreen
      </div>
      
      <div class="name">
        深海绿
      </div>
      
      <div>
        #8bb381
      </div>
      
      <div>
        rgb(139,179,129)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c68e17">
      <font color="#ffffff"> 
      
      <div class="name">
        Caramel
      </div>
      
      <div class="name">
        焦糖色
      </div>
      
      <div>
        #c68e17
      </div>
      
      <div>
        rgb(198,142,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#954535">
      <font color="#ffffff"> 
      
      <div class="name">
        Chestnut
      </div>
      
      <div class="name">
        栗色
      </div>
      
      <div>
        #954535
      </div>
      
      <div>
        rgb(149,69,53)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6a287e">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleJam
      </div>
      
      <div class="name">
        果酱紫
      </div>
      
      <div>
        #6a287e
      </div>
      
      <div>
        rgb(106,40,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#98afc7" id="blue">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueGray
      </div>
      
      <div class="name">
        蓝灰色
      </div>
      
      <div>
        #98afc7
      </div>
      
      <div>
        rgb(152,175,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f0ffff">
      <font color="#000000"> 
      
      <div class="name">
        Azure
      </div>
      
      <div class="name">
        蔚蓝
      </div>
      
      <div>
        #f0ffff
      </div>
      
      <div>
        rgb(240,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9cb071">
      <font color="#ffffff"> 
      
      <div class="name">
        IguanaGreen
      </div>
      
      <div class="name">
        鬣蜥绿
      </div>
      
      <div>
        #9cb071
      </div>
      
      <div>
        rgb(156,176,113)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b5a642">
      <font color="#ffffff"> 
      
      <div class="name">
        Brass
      </div>
      
      <div class="name">
        黄铜
      </div>
      
      <div>
        #b5a642
      </div>
      
      <div>
        rgb(181,166,66)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7e3517">
      <font color="#ffffff"> 
      
      <div class="name">
        BloodRed
      </div>
      
      <div class="name">
        血红
      </div>
      
      <div>
        #7e3517
      </div>
      
      <div>
        rgb(126,53,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7d1b7e">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkOrchid
      </div>
      
      <div class="name">
        暗紫色
      </div>
      
      <div>
        #7d1b7e
      </div>
      
      <div>
        rgb(125,27,126)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#6d7b8d">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSlateGray
      </div>
      
      <div class="name">
        浅板岩灰
      </div>
      
      <div>
        #6d7b8d
      </div>
      
      <div>
        rgb(109,123,141)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ccffff">
      <font color="#000000"> 
      
      <div class="name">
        LightSlate
      </div>
      
      <div class="name">
        亮岩灰
      </div>
      
      <div>
        #ccffff
      </div>
      
      <div>
        rgb(204,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b2c248">
      <font color="#ffffff"> 
      
      <div class="name">
        AvocadoGreen
      </div>
      
      <div class="name">
        鳄梨绿
      </div>
      
      <div>
        #b2c248
      </div>
      
      <div>
        rgb(178,194,72)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ada96e">
      <font color="#ffffff"> 
      
      <div class="name">
        Khaki
      </div>
      
      <div class="name">
        黄褐色
      </div>
      
      <div>
        #ada96e
      </div>
      
      <div>
        rgb(173,169,110)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8a4117">
      <font color="#ffffff"> 
      
      <div class="name">
        Sienna
      </div>
      
      <div class="name">
        土黄
      </div>
      
      <div>
        #8a4117
      </div>
      
      <div>
        rgb(138,65,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#a74ac7">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleFlower
      </div>
      
      <div class="name">
        花紫色
      </div>
      
      <div>
        #a74ac7
      </div>
      
      <div>
        rgb(167,74,199)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#657383">
      <font color="#ffffff"> 
      
      <div class="name">
        SlateGray
      </div>
      
      <div class="name">
        板岩灰
      </div>
      
      <div>
        #657383
      </div>
      
      <div>
        rgb(101,115,131)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#93ffe8">
      <font color="#000000"> 
      
      <div class="name">
        LightAquamarine
      </div>
      
      <div class="name">
        浅宝石蓝
      </div>
      
      <div>
        #93ffe8
      </div>
      
      <div>
        rgb(147,255,232)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9dc209">
      <font color="#ffffff"> 
      
      <div class="name">
        PistachioGreen
      </div>
      
      <div class="name">
        开心果绿
      </div>
      
      <div>
        #9dc209
      </div>
      
      <div>
        rgb(157,194,9)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c19a6b">
      <font color="#ffffff"> 
      
      <div class="name">
        Camelbrown
      </div>
      
      <div class="name">
        驼棕色
      </div>
      
      <div>
        #c19a6b
      </div>
      
      <div>
        rgb(193,154,107)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7e3817">
      <font color="#ffffff"> 
      
      <div class="name">
        Sangria
      </div>
      
      <div class="name">
        桑格利亚红
      </div>
      
      <div>
        #7e3817
      </div>
      
      <div>
        rgb(126,56,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b048b5">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumOrchid
      </div>
      
      <div class="name">
        间紫色
      </div>
      
      <div>
        #b048b5
      </div>
      
      <div>
        rgb(176,72,181)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#616d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        JetGray
      </div>
      
      <div class="name">
        深灰色
      </div>
      
      <div>
        #616d7e
      </div>
      
      <div>
        rgb(97,109,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9afeff">
      <font color="#000000"> 
      
      <div class="name">
        ElectricBlue
      </div>
      
      <div class="name">
        靛蓝
      </div>
      
      <div>
        #9afeff
      </div>
      
      <div>
        rgb(154,254,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#a1c935">
      <font color="#ffffff"> 
      
      <div class="name">
        SaladGreen
      </div>
      
      <div class="name">
        沙拉绿
      </div>
      
      <div>
        #a1c935
      </div>
      
      <div>
        rgb(161,201,53)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#cd7f32">
      <font color="#ffffff"> 
      
      <div class="name">
        Bronze
      </div>
      
      <div class="name">
        青铜色
      </div>
      
      <div>
        #cd7f32
      </div>
      
      <div>
        rgb(205,127,50)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#800517">
      <font color="#ffffff"> 
      
      <div class="name">
        Firebrick
      </div>
      
      <div class="name">
        火砖色
      </div>
      
      <div>
        #800517
      </div>
      
      <div>
        rgb(128,5,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6c2dc7">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleAmethyst
      </div>
      
      <div class="name">
        紫水晶紫
      </div>
      
      <div>
        #6c2dc7
      </div>
      
      <div>
        rgb(108,45,199)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#646d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        MistBlue
      </div>
      
      <div class="name">
        薄雾蓝
      </div>
      
      <div>
        #646d7e
      </div>
      
      <div>
        rgb(100,109,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7fffd4">
      <font color="#ffffff"> 
      
      <div class="name">
        Aquamarine
      </div>
      
      <div class="name">
        海蓝宝绿
      </div>
      
      <div>
        #7fffd4
      </div>
      
      <div>
        rgb(127,255,212)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7fe817">
      <font color="#ffffff"> 
      
      <div class="name">
        HummingbirdGreen
      </div>
      
      <div class="name">
        蜂鸟绿
      </div>
      
      <div>
        #7fe817
      </div>
      
      <div>
        rgb(127,232,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c88141">
      <font color="#ffffff"> 
      
      <div class="name">
        TigerOrange
      </div>
      
      <div class="name">
        虎橙色
      </div>
      
      <div>
        #c88141
      </div>
      
      <div>
        rgb(200,129,65)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#810541">
      <font color="#ffffff"> 
      
      <div class="name">
        Maroon
      </div>
      
      <div class="name">
        栗色
      </div>
      
      <div>
        #810541
      </div>
      
      <div>
        rgb(129,5,65)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#842dce">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkViolet
      </div>
      
      <div class="name">
        暗紫
      </div>
      
      <div>
        #842dce
      </div>
      
      <div>
        rgb(132,45,206)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#566d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        MarbleBlue
      </div>
      
      <div class="name">
        大理石蓝
      </div>
      
      <div>
        #566d7e
      </div>
      
      <div>
        rgb(86,109,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00ffff">
      <font color="#ffffff"> 
      
      <div class="name">
        CyanorAqua
      </div>
      
      <div class="name">
        青色
      </div>
      
      <div>
        #00ffff
      </div>
      
      <div>
        rgb(0,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#59e817">
      <font color="#ffffff"> 
      
      <div class="name">
        NebulaGreen
      </div>
      
      <div class="name">
        星云绿
      </div>
      
      <div>
        #59e817
      </div>
      
      <div>
        rgb(89,232,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c58917">
      <font color="#ffffff"> 
      
      <div class="name">
        Cinnamon
      </div>
      
      <div class="name">
        肉桂色
      </div>
      
      <div>
        #c58917
      </div>
      
      <div>
        rgb(197,137,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7d0541">
      <font color="#ffffff"> 
      
      <div class="name">
        PlumPie
      </div>
      
      <div class="name">
        梅色
      </div>
      
      <div>
        #7d0541
      </div>
      
      <div>
        rgb(125,5,65)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8d38c9">
      <font color="#ffffff"> 
      
      <div class="name">
        Violet
      </div>
      
      <div class="name">
        紫色
      </div>
      
      <div>
        #8d38c9
      </div>
      
      <div>
        rgb(141,56,201)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#737ca1">
      <font color="#ffffff"> 
      
      <div class="name">
        SlateBlue
      </div>
      
      <div class="name">
        板岩蓝
      </div>
      
      <div>
        #737ca1
      </div>
      
      <div>
        rgb(115,124,161)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7dfdfe">
      <font color="#ffffff"> 
      
      <div class="name">
        TronBlue
      </div>
      
      <div class="name">
        星际蓝
      </div>
      
      <div>
        #7dfdfe
      </div>
      
      <div>
        rgb(125,253,254)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#57e964">
      <font color="#ffffff"> 
      
      <div class="name">
        StoplightGoGreen
      </div>
      
      <div class="name">
        灯绿色
      </div>
      
      <div>
        #57e964
      </div>
      
      <div>
        rgb(87,233,100)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#af9b60">
      <font color="#ffffff"> 
      
      <div class="name">
        BulletShell
      </div>
      
      <div class="name">
        壳色
      </div>
      
      <div>
        #af9b60
      </div>
      
      <div>
        rgb(175,155,96)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7e354d">
      <font color="#ffffff"> 
      
      <div class="name">
        VelvetMaroon
      </div>
      
      <div class="name">
        天鹅绒栗色
      </div>
      
      <div>
        #7e354d
      </div>
      
      <div>
        rgb(126,53,77)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7a5dc7">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleSageBush
      </div>
      
      <div class="name">
        紫鼠尾草布什
      </div>
      
      <div>
        #7a5dc7
      </div>
      
      <div>
        rgb(122,93,199)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#4863a0">
      <font color="#ffffff"> 
      
      <div class="name">
        SteelBlue
      </div>
      
      <div class="name">
        钢蓝
      </div>
      
      <div>
        #4863a0
      </div>
      
      <div>
        rgb(72,99,160)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#57feff">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueZircon
      </div>
      
      <div class="name">
        锆石蓝
      </div>
      
      <div>
        #57feff
      </div>
      
      <div>
        rgb(87,254,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#64e986">
      <font color="#ffffff"> 
      
      <div class="name">
        AlgaeGreen
      </div>
      
      <div class="name">
        海藻绿
      </div>
      
      <div>
        #64e986
      </div>
      
      <div>
        rgb(100,233,134)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#af7817">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkGoldenrod
      </div>
      
      <div class="name">
        黑暗金
      </div>
      
      <div>
        #af7817
      </div>
      
      <div>
        rgb(175,120,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7d0552">
      <font color="#ffffff"> 
      
      <div class="name">
        PlumVelvet
      </div>
      
      <div class="name">
        天鹅绒紫
      </div>
      
      <div>
        #7d0552
      </div>
      
      <div>
        rgb(125,5,82)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f38ec">
      <font color="#ffffff"> 
      
      <div class="name">
        LovelyPurple
      </div>
      
      <div class="name">
        亮紫色
      </div>
      
      <div>
        #7f38ec
      </div>
      
      <div>
        rgb(127,56,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2b547e">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueJay
      </div>
      
      <div class="name">
        松鸦蓝
      </div>
      
      <div>
        #2b547e
      </div>
      
      <div>
        rgb(43,84,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8eebec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueLagoon
      </div>
      
      <div class="name">
        蓝色泻湖蓝
      </div>
      
      <div>
        #8eebec
      </div>
      
      <div>
        rgb(142,235,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5efb6e">
      <font color="#ffffff"> 
      
      <div class="name">
        JadeGreen
      </div>
      
      <div class="name">
        翡翠绿
      </div>
      
      <div>
        #5efb6e
      </div>
      
      <div>
        rgb(94,251,110)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b87333">
      <font color="#ffffff"> 
      
      <div class="name">
        Copper
      </div>
      
      <div class="name">
        铜
      </div>
      
      <div>
        #b87333
      </div>
      
      <div>
        rgb(184,115,51)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f4e52">
      <font color="#ffffff"> 
      
      <div class="name">
        RosyFinch
      </div>
      
      <div class="name">
        玫瑰雀
      </div>
      
      <div>
        #7f4e52
      </div>
      
      <div>
        rgb(127,78,82)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8e35ef">
      <font color="#ffffff"> 
      
      <div class="name">
        Purple
      </div>
      
      <div class="name">
        紫色
      </div>
      
      <div>
        #8e35ef
      </div>
      
      <div>
        rgb(142,53,239)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2b3856">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSlateBlue
      </div>
      
      <div class="name">
        深板岩蓝
      </div>
      
      <div>
        #2b3856
      </div>
      
      <div>
        rgb(43,56,86)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#50ebec">
      <font color="#ffffff"> 
      
      <div class="name">
        Celeste
      </div>
      
      <div class="name">
        天蓝色
      </div>
      
      <div>
        #50ebec
      </div>
      
      <div>
        rgb(80,235,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00ff00">
      <font color="#ffffff"> 
      
      <div class="name">
        Green
      </div>
      
      <div class="name">
        绿色
      </div>
      
      <div>
        #00ff00
      </div>
      
      <div>
        rgb(0,255,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#966f33">
      <font color="#ffffff"> 
      
      <div class="name">
        Wood
      </div>
      
      <div class="name">
        木色
      </div>
      
      <div>
        #966f33
      </div>
      
      <div>
        rgb(150,111,51)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f5a58">
      <font color="#ffffff"> 
      
      <div class="name">
        Puce
      </div>
      
      <div class="name">
        深褐色
      </div>
      
      <div>
        #7f5a58
      </div>
      
      <div>
        rgb(127,90,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#893bff">
      <font color="#ffffff"> 
      
      <div class="name">
        AztechPurple
      </div>
      
      <div class="name">
        Aztech紫色
      </div>
      
      <div>
        #893bff
      </div>
      
      <div>
        rgb(137,59,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#151b54">
      <font color="#ffffff"> 
      
      <div class="name">
        MidnightBlue
      </div>
      
      <div class="name">
        午夜蓝
      </div>
      
      <div>
        #151b54
      </div>
      
      <div>
        rgb(21,27,84)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4ee2ec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueDiamond
      </div>
      
      <div class="name">
        钻石蓝
      </div>
      
      <div>
        #4ee2ec
      </div>
      
      <div>
        rgb(78,226,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5ffb17">
      <font color="#ffffff"> 
      
      <div class="name">
        EmeraldGreen
      </div>
      
      <div class="name">
        翡翠绿
      </div>
      
      <div>
        #5ffb17
      </div>
      
      <div>
        rgb(95,251,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#806517">
      <font color="#ffffff"> 
      
      <div class="name">
        OakBrown
      </div>
      
      <div class="name">
        橡木棕
      </div>
      
      <div>
        #806517
      </div>
      
      <div>
        rgb(128,101,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f525d">
      <font color="#ffffff"> 
      
      <div class="name">
        DullPurple
      </div>
      
      <div class="name">
        暗紫色
      </div>
      
      <div>
        #7f525d
      </div>
      
      <div>
        rgb(127,82,93)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8467d7">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumPurple
      </div>
      
      <div class="name">
        中紫红色
      </div>
      
      <div>
        #8467d7
      </div>
      
      <div>
        rgb(132,103,215)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#000080">
      <font color="#ffffff"> 
      
      <div class="name">
        NavyBlue
      </div>
      
      <div class="name">
        海军蓝
      </div>
      
      <div>
        #000080
      </div>
      
      <div>
        rgb(0,0,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#81d8d0">
      <font color="#ffffff"> 
      
      <div class="name">
        TiffanyBlue
      </div>
      
      <div class="name">
        蒂芙尼蓝
      </div>
      
      <div>
        #81d8d0
      </div>
      
      <div>
        rgb(129,216,208)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#87f717">
      <font color="#ffffff"> 
      
      <div class="name">
        LawnGreen
      </div>
      
      <div class="name">
        草坪绿
      </div>
      
      <div>
        #87f717
      </div>
      
      <div>
        rgb(135,247,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#827839">
      <font color="#ffffff"> 
      
      <div class="name">
        Moccasin
      </div>
      
      <div class="name">
        鹿皮棕
      </div>
      
      <div>
        #827839
      </div>
      
      <div>
        rgb(130,120,57)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b38481">
      <font color="#ffffff"> 
      
      <div class="name">
        RosyBrown
      </div>
      
      <div class="name">
        玫瑰棕
      </div>
      
      <div>
        #b38481
      </div>
      
      <div>
        rgb(179,132,129)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#a23bec">
      <font color="#ffffff"> 
      
      <div class="name">
        JasminePurple
      </div>
      
      <div class="name">
        茉莉紫
      </div>
      
      <div>
        #a23bec
      </div>
      
      <div>
        rgb(162,59,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#342d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueWhale
      </div>
      
      <div class="name">
        蓝鲸蓝
      </div>
      
      <div>
        #342d7e
      </div>
      
      <div>
        rgb(52,45,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#92c7c7">
      <font color="#ffffff"> 
      
      <div class="name">
        CyanOpaque
      </div>
      
      <div class="name">
        不透明青色
      </div>
      
      <div>
        #92c7c7
      </div>
      
      <div>
        rgb(146,199,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8afb17">
      <font color="#ffffff"> 
      
      <div class="name">
        Chartreuse
      </div>
      
      <div class="name">
        淡黄色
      </div>
      
      <div>
        #8afb17
      </div>
      
      <div>
        rgb(138,251,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#827b60">
      <font color="#ffffff"> 
      
      <div class="name">
        ArmyBrown
      </div>
      
      <div class="name">
        军棕色
      </div>
      
      <div>
        #827b60
      </div>
      
      <div>
        rgb(130,123,96)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c5908e">
      <font color="#ffffff"> 
      
      <div class="name">
        KhakiRose
      </div>
      
      <div class="name">
        玫瑰卡其色
      </div>
      
      <div>
        #c5908e
      </div>
      
      <div>
        rgb(197,144,142)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b041ff">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleDaffodil
      </div>
      
      <div class="name">
        水仙紫
      </div>
      
      <div>
        #b041ff
      </div>
      
      <div>
        rgb(176,65,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#15317e">
      <font color="#ffffff"> 
      
      <div class="name">
        LapisBlue
      </div>
      
      <div class="name">
        青金石蓝
      </div>
      
      <div>
        #15317e
      </div>
      
      <div>
        rgb(21,49,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#77bfc7">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueHosta
      </div>
      
      <div class="name">
        Hosta蓝
      </div>
      
      <div>
        #77bfc7
      </div>
      
      <div>
        rgb(119,191,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6afb92">
      <font color="#ffffff"> 
      
      <div class="name">
        DragonGreen
      </div>
      
      <div class="name">
        龙绿色
      </div>
      
      <div>
        #6afb92
      </div>
      
      <div>
        rgb(106,251,146)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#786d5f">
      <font color="#ffffff"> 
      
      <div class="name">
        Sandstone
      </div>
      
      <div class="name">
        砂岩色
      </div>
      
      <div>
        #786d5f
      </div>
      
      <div>
        rgb(120,109,95)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c48189">
      <font color="#ffffff"> 
      
      <div class="name">
        PinkBow
      </div>
      
      <div class="name">
        蝴蝶结粉
      </div>
      
      <div>
        #c48189
      </div>
      
      <div>
        rgb(196,129,137)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c45aec">
      <font color="#ffffff"> 
      
      <div class="name">
        TyrianPurple
      </div>
      
      <div class="name">
        提尔红紫
      </div>
      
      <div>
        #c45aec
      </div>
      
      <div>
        rgb(196,90,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#151b8d">
      <font color="#ffffff"> 
      
      <div class="name">
        DenimDarkBlue
      </div>
      
      <div class="name">
        牛仔布深蓝色
      </div>
      
      <div>
        #151b8d
      </div>
      
      <div>
        rgb(21,27,141)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#78c7c7">
      <font color="#ffffff"> 
      
      <div class="name">
        NorthernLightsBlue
      </div>
      
      <div class="name">
        北极光蓝
      </div>
      
      <div>
        #78c7c7
      </div>
      
      <div>
        rgb(120,199,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#98ff98">
      <font color="#ffffff"> 
      
      <div class="name">
        Mintgreen
      </div>
      
      <div class="name">
        薄荷绿
      </div>
      
      <div>
        #98ff98
      </div>
      
      <div>
        rgb(152,255,152)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#493d26">
      <font color="#ffffff"> 
      
      <div class="name">
        Mocha
      </div>
      
      <div class="name">
        抹茶色
      </div>
      
      <div>
        #493d26
      </div>
      
      <div>
        rgb(73,61,38)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c48793" id="pink">
      <font color="#ffffff"> 
      
      <div class="name">
        LipstickPink
      </div>
      
      <div class="name">
        唇粉色
      </div>
      
      <div>
        #c48793
      </div>
      
      <div>
        rgb(196,135,147)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9172ec">
      <font color="#ffffff"> 
      
      <div class="name">
        CrocusPurple
      </div>
      
      <div class="name">
        番红花紫
      </div>
      
      <div>
        #9172ec
      </div>
      
      <div>
        rgb(145,114,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#0000a0">
      <font color="#ffffff"> 
      
      <div class="name">
        EarthBlue
      </div>
      
      <div class="name">
        土蓝色
      </div>
      
      <div>
        #0000a0
      </div>
      
      <div>
        rgb(0,0,160)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#48cccd">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumTurquoise
      </div>
      
      <div class="name">
        中绿松石色
      </div>
      
      <div>
        #48cccd
      </div>
      
      <div>
        rgb(72,204,205)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b5eaaa">
      <font color="#000000"> 
      
      <div class="name">
        GreenThumb
      </div>
      
      <div class="name">
        拇指绿
      </div>
      
      <div>
        #b5eaaa
      </div>
      
      <div>
        rgb(181,234,170)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#483c32">
      <font color="#ffffff"> 
      
      <div class="name">
        Taupe
      </div>
      
      <div class="name">
        灰褐色
      </div>
      
      <div>
        #483c32
      </div>
      
      <div>
        rgb(72,60,50)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e8adaa">
      <font color="#ffffff"> 
      
      <div class="name">
        Rose
      </div>
      
      <div class="name">
        玫瑰色
      </div>
      
      <div>
        #e8adaa
      </div>
      
      <div>
        rgb(232,173,170)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9e7bff">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleMimosa
      </div>
      
      <div class="name">
        含羞草紫
      </div>
      
      <div>
        #9e7bff
      </div>
      
      <div>
        rgb(158,123,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#0020c2">
      <font color="#ffffff"> 
      
      <div class="name">
        CobaltBlue
      </div>
      
      <div class="name">
        钴蓝色
      </div>
      
      <div>
        #0020c2
      </div>
      
      <div>
        rgb(0,32,194)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#43c6db">
      <font color="#ffffff"> 
      
      <div class="name">
        Turquoise
      </div>
      
      <div class="name">
        绿松石色
      </div>
      
      <div>
        #43c6db
      </div>
      
      <div>
        rgb(67,198,219)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c3fdb8">
      <font color="#000000"> 
      
      <div class="name">
        LightJade
      </div>
      
      <div class="name">
        玉色
      </div>
      
      <div>
        #c3fdb8
      </div>
      
      <div>
        rgb(195,253,184)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6f4e37">
      <font color="#ffffff"> 
      
      <div class="name">
        Coffee
      </div>
      
      <div class="name">
        咖啡色
      </div>
      
      <div>
        #6f4e37
      </div>
      
      <div>
        rgb(111,78,55)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ecc5c0">
      <font color="#ffffff"> 
      
      <div class="name">
        RoseGold
      </div>
      
      <div class="name">
        玫瑰金
      </div>
      
      <div>
        #ecc5c0
      </div>
      
      <div>
        rgb(236,197,192)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#d462ff">
      <font color="#ffffff"> 
      
      <div class="name">
        HeliotropePurple
      </div>
      
      <div class="name">
        葵花紫
      </div>
      
      <div>
        #d462ff
      </div>
      
      <div>
        rgb(212,98,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#0041c2">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueberryBlue
      </div>
      
      <div class="name">
        蓝莓蓝
      </div>
      
      <div>
        #0041c2
      </div>
      
      <div>
        rgb(0,65,194)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#46c7c7">
      <font color="#ffffff"> 
      
      <div class="name">
        Jellyfish
      </div>
      
      <div class="name">
        水母绿
      </div>
      
      <div>
        #46c7c7
      </div>
      
      <div>
        rgb(70,199,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ccfb5d">
      <font color="#000000"> 
      
      <div class="name">
        TeaGreen
      </div>
      
      <div class="name">
        茶绿
      </div>
      
      <div>
        #ccfb5d
      </div>
      
      <div>
        rgb(204,251,93)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#835c3b">
      <font color="#ffffff"> 
      
      <div class="name">
        BrownBear
      </div>
      
      <div class="name">
        熊棕色
      </div>
      
      <div>
        #835c3b
      </div>
      
      <div>
        rgb(131,92,59)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#edc9af">
      <font color="#ffffff"> 
      
      <div class="name">
        DesertSand
      </div>
      
      <div class="name">
        沙漠色
      </div>
      
      <div>
        #edc9af
      </div>
      
      <div>
        rgb(237,201,175)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e238ec">
      <font color="#ffffff"> 
      
      <div class="name">
        Crimson
      </div>
      
      <div class="name">
        赤红
      </div>
      
      <div>
        #e238ec
      </div>
      
      <div>
        rgb(226,56,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2554c7">
      <font color="#ffffff"> 
      
      <div class="name">
        SapphireBlue
      </div>
      
      <div class="name">
        宝石蓝
      </div>
      
      <div>
        #2554c7
      </div>
      
      <div>
        rgb(37,84,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7bccb5" id="green">
      <font color="#ffffff"> 
      
      <div class="name">
        Bluegreen
      </div>
      
      <div class="name">
        蓝绿
      </div>
      
      <div>
        #7bccb5
      </div>
      
      <div>
        rgb(123,204,181)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#b1fb17">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenYellow
      </div>
      
      <div class="name">
        黄绿色
      </div>
      
      <div>
        #b1fb17
      </div>
      
      <div>
        rgb(177,251,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f5217">
      <font color="#ffffff"> 
      
      <div class="name">
        RedDirt
      </div>
      
      <div class="name">
        泥红色
      </div>
      
      <div>
        #7f5217
      </div>
      
      <div>
        rgb(127,82,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fdd7e4">
      <font color="#000000"> 
      
      <div class="name">
        PigPink
      </div>
      
      <div class="name">
        猪粉色
      </div>
      
      <div>
        #fdd7e4
      </div>
      
      <div>
        rgb(253,215,228)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c38ec7">
      <font color="#ffffff"> 
      
      <div class="name">
        PurpleDragon
      </div>
      
      <div class="name">
        龙紫色
      </div>
      
      <div>
        #c38ec7
      </div>
      
      <div>
        rgb(195,142,199)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#1569c7">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueEyes
      </div>
      
      <div class="name">
        眼睛蓝
      </div>
      
      <div>
        #1569c7
      </div>
      
      <div>
        rgb(21,105,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#43bfc7">
      <font color="#ffffff"> 
      
      <div class="name">
        MacawBlueGreen
      </div>
      
      <div class="name">
        金刚鹦鹉蓝绿色
      </div>
      
      <div>
        #43bfc7
      </div>
      
      <div>
        rgb(67,191,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#bce954">
      <font color="#ffffff"> 
      
      <div class="name">
        SlimeGreen
      </div>
      
      <div class="name">
        煤泥绿
      </div>
      
      <div>
        #bce954
      </div>
      
      <div>
        rgb(188,233,84)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7f462c">
      <font color="#ffffff"> 
      
      <div class="name">
        Sepia
      </div>
      
      <div class="name">
        棕褐色
      </div>
      
      <div>
        #7f462c
      </div>
      
      <div>
        rgb(127,70,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fcdfff">
      <font color="#000000"> 
      
      <div class="name">
        CottonCandy
      </div>
      
      <div class="name">
        棉花糖粉
      </div>
      
      <div>
        #fcdfff
      </div>
      
      <div>
        rgb(252,223,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c8a2c8">
      <font color="#ffffff"> 
      
      <div class="name">
        Lilac
      </div>
      
      <div class="name">
        丁香紫
      </div>
      
      <div>
        #c8a2c8
      </div>
      
      <div>
        rgb(200,162,200)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#2b60de">
      <font color="#ffffff"> 
      
      <div class="name">
        RoyalBlue
      </div>
      
      <div class="name">
        宝蓝色
      </div>
      
      <div>
        #2b60de
      </div>
      
      <div>
        rgb(43,96,222)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#3ea99f">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSeaGreen
      </div>
      
      <div class="name">
        浅海绿色
      </div>
      
      <div>
        #3ea99f
      </div>
      
      <div>
        rgb(62,169,159)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#edda74">
      <font color="#ffffff"> 
      
      <div class="name">
        Goldenrod
      </div>
      
      <div class="name">
        金菊色
      </div>
      
      <div>
        #edda74
      </div>
      
      <div>
        rgb(237,218,116)
      </div></font>
    </td>
    
    <td id="orange" class="tdborder" bgcolor="#c47451">
      <font color="#ffffff"> 
      
      <div class="name">
        OrangeSalmon
      </div>
      
      <div class="name">
        橙肉色
      </div>
      
      <div>
        #c47451
      </div>
      
      <div>
        rgb(196,116,81)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffdfdd">
      <font color="#000000"> 
      
      <div class="name">
        PinkBubbleGum
      </div>
      
      <div class="name">
        粉红泡泡糖色
      </div>
      
      <div>
        #ffdfdd
      </div>
      
      <div>
        rgb(255,223,221)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e6a9ec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlushPink
      </div>
      
      <div class="name">
        腮红粉
      </div>
      
      <div>
        #e6a9ec
      </div>
      
      <div>
        rgb(230,169,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#1f45fc">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueOrchid
      </div>
      
      <div class="name">
        蓝白紫
      </div>
      
      <div>
        #1f45fc
      </div>
      
      <div>
        rgb(31,69,252)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#3b9c9c">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkTurquoise
      </div>
      
      <div class="name">
        深粉蓝
      </div>
      
      <div>
        #3b9c9c
      </div>
      
      <div>
        rgb(59,156,156)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ede275">
      <font color="#ffffff"> 
      
      <div class="name">
        HarvestGold
      </div>
      
      <div class="name">
        收获金
      </div>
      
      <div>
        #ede275
      </div>
      
      <div>
        rgb(237,226,117)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c36241">
      <font color="#ffffff"> 
      
      <div class="name">
        Rust
      </div>
      
      <div class="name">
        锈色
      </div>
      
      <div>
        #c36241
      </div>
      
      <div>
        rgb(195,98,65)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fbbbb9">
      <font color="#ffffff"> 
      
      <div class="name">
        MistyRose
      </div>
      
      <div class="name">
        霧玫瑰色
      </div>
      
      <div>
        #fbbbb9
      </div>
      
      <div>
        rgb(251,187,185)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e0b0ff">
      <font color="#ffffff"> 
      
      <div class="name">
        Mauve
      </div>
      
      <div class="name">
        淡紫色
      </div>
      
      <div>
        #e0b0ff
      </div>
      
      <div>
        rgb(224,176,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#6960ec">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueLotus
      </div>
      
      <div class="name">
        莲花蓝
      </div>
      
      <div>
        #6960ec
      </div>
      
      <div>
        rgb(105,96,236)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#438d80">
      <font color="#ffffff"> 
      
      <div class="name">
        SeaTurtleGreen
      </div>
      
      <div class="name">
        海龟绿
      </div>
      
      <div>
        #438d80
      </div>
      
      <div>
        rgb(67,141,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffe87c" id="yellow">
      <font color="#000000"> 
      
      <div class="name">
        SunYellow
      </div>
      
      <div class="name">
        太阳黄
      </div>
      
      <div>
        #ffe87c
      </div>
      
      <div>
        rgb(255,232,124)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c35817">
      <font color="#ffffff"> 
      
      <div class="name">
        RedFox
      </div>
      
      <div class="name">
        狐红
      </div>
      
      <div>
        #c35817
      </div>
      
      <div>
        rgb(195,88,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#faafbe">
      <font color="#ffffff"> 
      
      <div class="name">
        Pink
      </div>
      
      <div class="name">
        粉
      </div>
      
      <div>
        #faafbe
      </div>
      
      <div>
        rgb(250,175,190)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c6aec7">
      <font color="#ffffff"> 
      
      <div class="name">
        WisteriaPurple
      </div>
      
      <div class="name">
        紫藤紫
      </div>
      
      <div>
        #c6aec7
      </div>
      
      <div>
        rgb(198,174,199)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#736aff">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSlateBlue
      </div>
      
      <div class="name">
        浅板岩蓝
      </div>
      
      <div>
        #736aff
      </div>
      
      <div>
        rgb(115,106,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#348781">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumAquamarine
      </div>
      
      <div class="name">
        间海蓝宝石色
      </div>
      
      <div>
        #348781
      </div>
      
      <div>
        rgb(52,135,129)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffff00">
      <font color="#000000"> 
      
      <div class="name">
        Yellow
      </div>
      
      <div class="name">
        黄色
      </div>
      
      <div>
        #ffff00
      </div>
      
      <div>
        rgb(255,255,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#c85a17">
      <font color="#ffffff"> 
      
      <div class="name">
        Chocolate
      </div>
      
      <div class="name">
        巧克力色
      </div>
      
      <div>
        #c85a17
      </div>
      
      <div>
        rgb(200,90,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#faafba">
      <font color="#ffffff"> 
      
      <div class="name">
        LightPink
      </div>
      
      <div class="name">
        浅粉红色
      </div>
      
      <div>
        #faafba
      </div>
      
      <div>
        rgb(250,175,186)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f9b7ff">
      <font color="#ffffff"> 
      
      <div class="name">
        BlossomPink
      </div>
      
      <div class="name">
        樱花粉
      </div>
      
      <div>
        #f9b7ff
      </div>
      
      <div>
        rgb(249,183,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#357ec7">
      <font color="#ffffff"> 
      
      <div class="name">
        WindowsBlue
      </div>
      
      <div class="name">
        Windows蓝色
      </div>
      
      <div>
        #357ec7
      </div>
      
      <div>
        rgb(53,126,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#307d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenishBlue
      </div>
      
      <div class="name">
        绿蓝色
      </div>
      
      <div>
        #307d7e
      </div>
      
      <div>
        rgb(48,125,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fff380">
      <font color="#000000"> 
      
      <div class="name">
        CornYellow
      </div>
      
      <div class="name">
        玉米黄
      </div>
      
      <div>
        #fff380
      </div>
      
      <div>
        rgb(255,243,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#cc6600">
      <font color="#ffffff"> 
      
      <div class="name">
        Sedona
      </div>
      
      <div class="name">
        塞多纳
      </div>
      
      <div>
        #cc6600
      </div>
      
      <div>
        rgb(204,102,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f9a7b0">
      <font color="#ffffff"> 
      
      <div class="name">
        FlamingoPink
      </div>
      
      <div class="name">
        火烈鸟粉
      </div>
      
      <div>
        #f9a7b0
      </div>
      
      <div>
        rgb(249,167,176)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#d2b9d3">
      <font color="#ffffff"> 
      
      <div class="name">
        Thistle
      </div>
      
      <div class="name">
        蓟
      </div>
      
      <div>
        #d2b9d3
      </div>
      
      <div>
        rgb(210,185,211)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#368bc1">
      <font color="#ffffff"> 
      
      <div class="name">
        GlacialBlueIce
      </div>
      
      <div class="name">
        冰川蓝
      </div>
      
      <div>
        #368bc1
      </div>
      
      <div>
        rgb(54,139,193)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5e7d7e">
      <font color="#ffffff"> 
      
      <div class="name">
        GrayishTurquoise
      </div>
      
      <div class="name">
        灰绿色
      </div>
      
      <div>
        #5e7d7e
      </div>
      
      <div>
        rgb(94,125,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffffc2">
      <font color="#000000"> 
      
      <div class="name">
        Parchment
      </div>
      
      <div class="name">
        羊皮纸色
      </div>
      
      <div>
        #ffffc2
      </div>
      
      <div>
        rgb(255,255,194)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e56717">
      <font color="#ffffff"> 
      
      <div class="name">
        PapayaOrange
      </div>
      
      <div class="name">
        木瓜橙
      </div>
      
      <div>
        #e56717
      </div>
      
      <div>
        rgb(229,103,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e7a1b0">
      <font color="#ffffff"> 
      
      <div class="name">
        PinkRose
      </div>
      
      <div class="name">
        玫瑰粉
      </div>
      
      <div>
        #e7a1b0
      </div>
      
      <div>
        rgb(231,161,176)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#d9cfec">
      <font color="#ffffff"> 
      
      <div class="name">
        Periwinkle
      </div>
      
      <div class="name">
        长春花色
      </div>
      
      <div>
        #d9cfec
      </div>
      
      <div>
        rgb(217,207,236)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#488ac7">
      <font color="#ffffff"> 
      
      <div class="name">
        SilkBlue
      </div>
      
      <div class="name">
        真丝蓝
      </div>
      
      <div>
        #488ac7
      </div>
      
      <div>
        rgb(72,138,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4c787e">
      <font color="#ffffff"> 
      
      <div class="name">
        BeetleGreen
      </div>
      
      <div class="name">
        甲虫绿
      </div>
      
      <div>
        #4c787e
      </div>
      
      <div>
        rgb(76,120,126)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffffcc">
      <font color="#000000"> 
      
      <div class="name">
        Cream
      </div>
      
      <div class="name">
        奶油色
      </div>
      
      <div>
        #ffffcc
      </div>
      
      <div>
        rgb(255,255,204)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e66c2c">
      <font color="#ffffff"> 
      
      <div class="name">
        HalloweenOrange
      </div>
      
      <div class="name">
        万圣节橙
      </div>
      
      <div>
        #e66c2c
      </div>
      
      <div>
        rgb(230,108,44)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e799a3">
      <font color="#ffffff"> 
      
      <div class="name">
        PinkDaisy
      </div>
      
      <div class="name">
        雏菊粉
      </div>
      
      <div>
        #e799a3
      </div>
      
      <div>
        rgb(231,153,163)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ebdde2">
      <font color="#000000"> 
      
      <div class="name">
        LavenderPinocchio
      </div>
      
      <div class="name">
        紫木偶花色
      </div>
      
      <div>
        #ebdde2
      </div>
      
      <div>
        rgb(235,221,226)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#3090c7">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueIvy
      </div>
      
      <div class="name">
        常春藤蓝
      </div>
      
      <div>
        #3090c7
      </div>
      
      <div>
        rgb(48,144,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#008080">
      <font color="#ffffff"> 
      
      <div class="name">
        Teal
      </div>
      
      <div class="name">
        蓝绿色
      </div>
      
      <div>
        #008080
      </div>
      
      <div>
        rgb(0,128,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fff8c6">
      <font color="#000000"> 
      
      <div class="name">
        LemonChiffon
      </div>
      
      <div class="name">
        柠檬绸色
      </div>
      
      <div>
        #fff8c6
      </div>
      
      <div>
        rgb(255,248,198)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f87217">
      <font color="#ffffff"> 
      
      <div class="name">
        PumpkinOrange
      </div>
      
      <div class="name">
        南瓜橙
      </div>
      
      <div>
        #f87217
      </div>
      
      <div>
        rgb(248,114,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e38aae">
      <font color="#ffffff"> 
      
      <div class="name">
        CadillacPink
      </div>
      
      <div class="name">
        凯迪拉克粉红色
      </div>
      
      <div>
        #e38aae
      </div>
      
      <div>
        rgb(227,138,174)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e3e4fa">
      <font color="#000000"> 
      
      <div class="name">
        Lavenderblue
      </div>
      
      <div class="name">
        薰衣草蓝
      </div>
      
      <div>
        #e3e4fa
      </div>
      
      <div>
        rgb(227,228,250)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#659ec7">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueKoi
      </div>
      
      <div class="name">
        锦鲤蓝
      </div>
      
      <div>
        #659ec7
      </div>
      
      <div>
        rgb(101,158,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4e8975">
      <font color="#ffffff"> 
      
      <div class="name">
        SeaGreen
      </div>
      
      <div class="name">
        海绿色
      </div>
      
      <div>
        #4e8975
      </div>
      
      <div>
        rgb(78,137,117)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fff8dc">
      <font color="#000000"> 
      
      <div class="name">
        Cornsilk
      </div>
      
      <div class="name">
        玉米丝色
      </div>
      
      <div>
        #fff8dc
      </div>
      
      <div>
        rgb(255,248,220)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f87431">
      <font color="#ffffff"> 
      
      <div class="name">
        ConstructionConeOrange
      </div>
      
      <div class="name">
        建筑锥橙
      </div>
      
      <div>
        #f87431
      </div>
      
      <div>
        rgb(248,116,49)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f778a1">
      <font color="#ffffff"> 
      
      <div class="name">
        CarnationPink
      </div>
      
      <div class="name">
        康乃馨粉红色
      </div>
      
      <div>
        #f778a1
      </div>
      
      <div>
        rgb(247,120,161)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fdeef4">
      <font color="#000000"> 
      
      <div class="name">
        Pearl
      </div>
      
      <div class="name">
        珍珠白
      </div>
      
      <div>
        #fdeef4
      </div>
      
      <div>
        rgb(253,238,244)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#87afc7">
      <font color="#ffffff"> 
      
      <div class="name">
        ColumbiaBlue
      </div>
      
      <div class="name">
        哥伦比亚蓝
      </div>
      
      <div>
        #87afc7
      </div>
      
      <div>
        rgb(135,175,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#78866b">
      <font color="#ffffff"> 
      
      <div class="name">
        CamouflageGreen
      </div>
      
      <div class="name">
        迷彩绿
      </div>
      
      <div>
        #78866b
      </div>
      
      <div>
        rgb(120,134,107)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f5f5dc">
      <font color="#000000"> 
      
      <div class="name">
        Beige
      </div>
      
      <div class="name">
        米色
      </div>
      
      <div>
        #f5f5dc
      </div>
      
      <div>
        rgb(245,245,220)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e67451">
      <font color="#ffffff"> 
      
      <div class="name">
        SunriseOrange
      </div>
      
      <div class="name">
        日出橙
      </div>
      
      <div>
        #e67451
      </div>
      
      <div>
        rgb(230,116,81)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#e56e94">
      <font color="#ffffff"> 
      
      <div class="name">
        BlushRed
      </div>
      
      <div class="name">
        腮红
      </div>
      
      <div>
        #e56e94
      </div>
      
      <div>
        rgb(229,110,148)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fff5ee">
      <font color="#000000"> 
      
      <div class="name">
        SeaShell
      </div>
      
      <div class="name">
        贝壳白
      </div>
      
      <div>
        #fff5ee
      </div>
      
      <div>
        rgb(255,245,238)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#95b9c7">
      <font color="#ffffff"> 
      
      <div class="name">
        BabyBlue
      </div>
      
      <div class="name">
        淡蓝色
      </div>
      
      <div>
        #95b9c7
      </div>
      
      <div>
        rgb(149,185,199)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#848b79">
      <font color="#ffffff"> 
      
      <div class="name">
        SageGreen
      </div>
      
      <div class="name">
        鼠尾草绿
      </div>
      
      <div>
        #848b79
      </div>
      
      <div>
        rgb(132,139,121)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fbf6d9">
      <font color="#000000"> 
      
      <div class="name">
        Blonde
      </div>
      
      <div class="name">
        亚麻色
      </div>
      
      <div>
        #fbf6d9
      </div>
      
      <div>
        rgb(251,246,217)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ff8040">
      <font color="#ffffff"> 
      
      <div class="name">
        MangoOrange
      </div>
      
      <div class="name">
        芒果橙
      </div>
      
      <div>
        #ff8040
      </div>
      
      <div>
        rgb(255,128,64)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f660ab">
      <font color="#ffffff"> 
      
      <div class="name">
        HotPink
      </div>
      
      <div class="name">
        亮粉色
      </div>
      
      <div>
        #f660ab
      </div>
      
      <div>
        rgb(246,96,171)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fefcff">
      <font color="#000000"> 
      
      <div class="name">
        MilkWhite
      </div>
      
      <div class="name">
        奶白
      </div>
      
      <div>
        #fefcff
      </div>
      
      <div>
        rgb(254,252,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#728fce">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSteelBlue
      </div>
      
      <div class="name">
        浅钢蓝
      </div>
      
      <div>
        #728fce
      </div>
      
      <div>
        rgb(114,143,206)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#617c58">
      <font color="#ffffff"> 
      
      <div class="name">
        HazelGreen
      </div>
      
      <div class="name">
        淡褐色
      </div>
      
      <div>
        #617c58
      </div>
      
      <div>
        rgb(97,124,88)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#faebd7">
      <font color="#000000"> 
      
      <div class="name">
        AntiqueWhite
      </div>
      
      <div class="name">
        古董白
      </div>
      
      <div>
        #faebd7
      </div>
      
      <div>
        rgb(250,235,215)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#f88017">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkOrange
      </div>
      
      <div class="name">
        深橙色
      </div>
      
      <div>
        #f88017
      </div>
      
      <div>
        rgb(248,128,23)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#fc6c85">
      <font color="#ffffff"> 
      
      <div class="name">
        WatermelonPink
      </div>
      
      <div class="name">
        西瓜粉
      </div>
      
      <div>
        #fc6c85
      </div>
      
      <div>
        rgb(252,108,133)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ffffff">
      <font color="#000000"> 
      
      <div class="name">
        White
      </div>
      
      <div class="name">
        白色
      </div>
      
      <div>
        #ffffff
      </div>
      
      <div>
        rgb(255,255,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td id="pinks" class="tdborder" bgcolor="#FFF0F5">
      <font color="#000000"> 
      
      <div class="name">
        LavenderBlush
      </div>
      
      <div class="name">
        薰衣草红
      </div>
      
      <div>
        #FFF0F5
      </div>
      
      <div>
        rgb(255,240,245)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F0FFFF">
      <font color="#000000"> 
      
      <div class="name">
        Azure
      </div>
      
      <div class="name">
        青白色
      </div>
      
      <div>
        #F0FFFF
      </div>
      
      <div>
        rgb(240,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00FFFF">
      <font color="#ffffff"> 
      
      <div class="name">
        Cyan/Aqua
      </div>
      
      <div class="name">
        青色
      </div>
      
      <div>
        #00FFFF
      </div>
      
      <div>
        rgb(0,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7CFC00">
      <font color="#ffffff"> 
      
      <div class="name">
        LawnGreen
      </div>
      
      <div class="name">
        草坪绿
      </div>
      
      <div>
        #7CFC00
      </div>
      
      <div>
        rgb(124,252,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#B8860B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkGoldenRod
      </div>
      
      <div class="name">
        深金菊黄
      </div>
      
      <div>
        #B8860B
      </div>
      
      <div>
        rgb(184,134,11)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FF4500">
      <font color="#ffffff"> 
      
      <div class="name">
        OrangeRed
      </div>
      
      <div class="name">
        橘红
      </div>
      
      <div>
        #FF4500
      </div>
      
      <div>
        rgb(255,69,0)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#FFB6C1">
      <font color="#000000"> 
      
      <div class="name">
        LightPink
      </div>
      
      <div class="name">
        浅粉
      </div>
      
      <div>
        #FFB6C1
      </div>
      
      <div>
        rgb(255,182,193)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ADD8E6">
      <font color="#000000"> 
      
      <div class="name">
        LightBlue
      </div>
      
      <div class="name">
        浅蓝
      </div>
      
      <div>
        #ADD8E6
      </div>
      
      <div>
        rgb(173,216,230)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#2F4F4F">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSlateGray
      </div>
      
      <div class="name">
        深岩灰
      </div>
      
      <div>
        #2F4F4F
      </div>
      
      <div>
        rgb(47,79,79)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7FFF00">
      <font color="#ffffff"> 
      
      <div class="name">
        ChartReuse
      </div>
      
      <div class="name">
        查特酒绿
      </div>
      
      <div>
        #7FFF00
      </div>
      
      <div>
        rgb(127,255,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#808000">
      <font color="#ffffff"> 
      
      <div class="name">
        Olive
      </div>
      
      <div class="name">
        橄榄色
      </div>
      
      <div>
        #808000
      </div>
      
      <div>
        rgb(128,128,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FF0000">
      <font color="#ffffff"> 
      
      <div class="name">
        Red
      </div>
      
      <div class="name">
        红色
      </div>
      
      <div>
        #FF0000
      </div>
      
      <div>
        rgb(255,0,0)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#FFC0CB">
      <font color="#000000"> 
      
      <div class="name">
        Pink
      </div>
      
      <div class="name">
        粉色
      </div>
      
      <div>
        #FFC0CB
      </div>
      
      <div>
        rgb(255,192,203)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#B0E0E6">
      <font color="#000000"> 
      
      <div class="name">
        PowderBlue
      </div>
      
      <div class="name">
        粉末蓝
      </div>
      
      <div>
        #B0E0E6
      </div>
      
      <div>
        rgb(176,224,230)
      </div></font>
    </td>
    
    <td id="greens" class="tdborder" bgcolor="#008B8B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkCyan
      </div>
      
      <div class="name">
        深青
      </div>
      
      <div>
        #008B8B
      </div>
      
      <div>
        rgb(0,139,139)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#ADFF2F">
      <font color="#ffffff"> 
      
      <div class="name">
        GreenYellow
      </div>
      
      <div class="name">
        黄绿色
      </div>
      
      <div>
        #ADFF2F
      </div>
      
      <div>
        rgb(173,255,47)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6B8E23">
      <font color="#ffffff"> 
      
      <div class="name">
        OliveDrab
      </div>
      
      <div class="name">
        橄榄绿
      </div>
      
      <div>
        #6B8E23
      </div>
      
      <div>
        rgb(107,142,35)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#A52A2A">
      <font color="#ffffff"> 
      
      <div class="name">
        Brown
      </div>
      
      <div class="name">
        褐色
      </div>
      
      <div>
        #A52A2A
      </div>
      
      <div>
        rgb(165,42,42)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#FF69B4">
      <font color="#ffffff"> 
      
      <div class="name">
        HotPink
      </div>
      
      <div class="name">
        艳粉
      </div>
      
      <div>
        #FF69B4
      </div>
      
      <div>
        rgb(255,105,180)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#87CEFA">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSkyBlue
      </div>
      
      <div class="name">
        浅天蓝
      </div>
      
      <div>
        #87CEFA
      </div>
      
      <div>
        rgb(135,206,250)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#008080">
      <font color="#ffffff"> 
      
      <div class="name">
        Teal
      </div>
      
      <div class="name">
        鸭翅绿
      </div>
      
      <div>
        #008080
      </div>
      
      <div>
        rgb(0,128,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#9ACD32">
      <font color="#ffffff"> 
      
      <div class="name">
        YellowGreen
      </div>
      
      <div class="name">
        暗黄绿色
      </div>
      
      <div>
        #9ACD32
      </div>
      
      <div>
        rgb(154,205,50)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#556B2F">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkOliveGreen
      </div>
      
      <div class="name">
        深橄榄绿
      </div>
      
      <div>
        #556B2F
      </div>
      
      <div>
        rgb(85,107,47)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#B22222">
      <font color="#ffffff"> 
      
      <div class="name">
        FireBrick
      </div>
      
      <div class="name">
        火砖红
      </div>
      
      <div>
        #B22222
      </div>
      
      <div>
        rgb(178,34,34)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#D87093">
      <font color="#ffffff"> 
      
      <div class="name">
        PaleVioletRed
      </div>
      
      <div class="name">
        白紫红
      </div>
      
      <div>
        #D87093
      </div>
      
      <div>
        rgb(219,112,147)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#87CEEB">
      <font color="#ffffff"> 
      
      <div class="name">
        SkyBlue
      </div>
      
      <div class="name">
        天蓝
      </div>
      
      <div>
        #87CEEB
      </div>
      
      <div>
        rgb(135,206,235)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#AFEEEE">
      <font color="#000000"> 
      
      <div class="name">
        PaleTurquoise
      </div>
      
      <div class="name">
        白松石绿
      </div>
      
      <div>
        #AFEEEE
      </div>
      
      <div>
        rgb(175,238,238)
      </div></font>
    </td>
    
    <td id="yellows" class="tdborder" bgcolor="#FFFFE0">
      <font color="#000000"> 
      
      <div class="name">
        LightYellow
      </div>
      
      <div class="name">
        浅黄
      </div>
      
      <div>
        #FFFFE0
      </div>
      
      <div>
        rgb(255,255,224)
      </div></font>
    </td>
    
    <td id="oranges" class="tdborder" bgcolor="#FFA500">
      <font color="#ffffff"> 
      
      <div class="name">
        Orange
      </div>
      
      <div class="name">
        橙色
      </div>
      
      <div>
        #FFA500
      </div>
      
      <div>
        rgb(255,165,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8B0000">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkRed
      </div>
      
      <div class="name">
        深红
      </div>
      
      <div>
        #8B0000
      </div>
      
      <div>
        rgb(139,0,0)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#FF1493">
      <font color="#ffffff"> 
      
      <div class="name">
        DeepPink
      </div>
      
      <div class="name">
        深粉
      </div>
      
      <div>
        #FF1493
      </div>
      
      <div>
        rgb(255,20,147)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00BFFF">
      <font color="#ffffff"> 
      
      <div class="name">
        DeepSkyBlue
      </div>
      
      <div class="name">
        深天蓝
      </div>
      
      <div>
        #00BFFF
      </div>
      
      <div>
        rgb(0,191,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7FFFD4">
      <font color="#ffffff"> 
      
      <div class="name">
        AquaMarine
      </div>
      
      <div class="name">
        碧绿
      </div>
      
      <div>
        #7FFFD4
      </div>
      
      <div>
        rgb(127,255,212)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFF8DC">
      <font color="#000000"> 
      
      <div class="name">
        CornSilk
      </div>
      
      <div class="name">
        玉米穗黄
      </div>
      
      <div>
        #FFF8DC
      </div>
      
      <div>
        rgb(255,248,220)
      </div></font>
    </td>
    
    <td id="browns" class="tdborder" bgcolor="#D2B48C">
      <font color="#ffffff"> 
      
      <div class="name">
        Tan
      </div>
      
      <div class="name">
        日晒褐
      </div>
      
      <div>
        #D2B48C
      </div>
      
      <div>
        rgb(210,180,140)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#800000">
      <font color="#ffffff"> 
      
      <div class="name">
        Maroon
      </div>
      
      <div class="name">
        栗色
      </div>
      
      <div>
        #800000
      </div>
      
      <div>
        rgb(128,0,0)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#C71585">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumVioletRed
      </div>
      
      <div class="name">
        中紫红
      </div>
      
      <div>
        #C71585
      </div>
      
      <div>
        rgb(199,21,133)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6495ED">
      <font color="#ffffff"> 
      
      <div class="name">
        CornFlowerBlue
      </div>
      
      <div class="name">
        矢车菊蓝
      </div>
      
      <div>
        #6495ED
      </div>
      
      <div>
        rgb(100,149,237)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#66CDAA">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumAquaMarine
      </div>
      
      <div class="name">
        中碧绿
      </div>
      
      <div>
        #66CDAA
      </div>
      
      <div>
        rgb(102,205,170)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F5F5DC">
      <font color="#000000"> 
      
      <div class="name">
        Beige
      </div>
      
      <div class="name">
        米色
      </div>
      
      <div>
        #F5F5DC
      </div>
      
      <div>
        rgb(245,245,220)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#DEB887">
      <font color="#ffffff"> 
      
      <div class="name">
        BurlyWood
      </div>
      
      <div class="name">
        硬木褐
      </div>
      
      <div>
        #DEB887
      </div>
      
      <div>
        rgb(222,184,135)
      </div></font>
    </td>
    
    <td id="grays" class="tdborder" bgcolor="#FFFFFF">
      <font color="#000000"> 
      
      <div class="name">
        White
      </div>
      
      <div class="name">
        白色
      </div>
      
      <div>
        #FFFFFF
      </div>
      
      <div>
        rgb(255,255,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#DC143C">
      <font color="#ffffff"> 
      
      <div class="name">
        Crimson
      </div>
      
      <div class="name">
        绯红
      </div>
      
      <div>
        #DC143C
      </div>
      
      <div>
        rgb(220,20,60)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#1E90FF">
      <font color="#ffffff"> 
      
      <div class="name">
        DodgerBlue
      </div>
      
      <div class="name">
        湖蓝
      </div>
      
      <div>
        #1E90FF
      </div>
      
      <div>
        rgb(30,144,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#40E0D0">
      <font color="#ffffff"> 
      
      <div class="name">
        Turquoise
      </div>
      
      <div class="name">
        松石绿
      </div>
      
      <div>
        #40E0D0
      </div>
      
      <div>
        rgb(64,224,208)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FAFAD2">
      <font color="#000000"> 
      
      <div class="name">
        LightGoldenRodYellow
      </div>
      
      <div class="name">
        浅金菊黄
      </div>
      
      <div>
        #FAFAD2
      </div>
      
      <div>
        rgb(250,250,210)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F4A460">
      <font color="#ffffff"> 
      
      <div class="name">
        SandyBrown
      </div>
      
      <div class="name">
        沙褐
      </div>
      
      <div>
        #F4A460
      </div>
      
      <div>
        rgb(244,164,96)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFFAFA">
      <font color="#000000"> 
      
      <div class="name">
        Snow
      </div>
      
      <div class="name">
        雪白
      </div>
      
      <div>
        #FFFAFA
      </div>
      
      <div>
        rgb(255,250,250)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td id="purples" class="tdborder" bgcolor="#E6E6FA">
      <font color="#000000"> 
      
      <div class="name">
        Lavender
      </div>
      
      <div class="name">
        薰衣草紫
      </div>
      
      <div>
        #E6E6FA
      </div>
      
      <div>
        rgb(230,230,250)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4169E1">
      <font color="#ffffff"> 
      
      <div class="name">
        RoyalBlue
      </div>
      
      <div class="name">
        品蓝
      </div>
      
      <div>
        #4169E1
      </div>
      
      <div>
        rgb(65,105,225)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#48D1CC">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumTurquoise
      </div>
      
      <div class="name">
        中松石绿
      </div>
      
      <div>
        #48D1CC
      </div>
      
      <div>
        rgb(72,209,204)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FDF5E6">
      <font color="#000000"> 
      
      <div class="name">
        OldLace
      </div>
      
      <div class="name">
        旧蕾丝白
      </div>
      
      <div>
        #FDF5E6
      </div>
      
      <div>
        rgb(253,245,230)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#D2691E">
      <font color="#ffffff"> 
      
      <div class="name">
        Chocolate
      </div>
      
      <div class="name">
        巧克力色
      </div>
      
      <div>
        #D2691E
      </div>
      
      <div>
        rgb(210,105,30)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFFAF0">
      <font color="#000000"> 
      
      <div class="name">
        FloralWhite
      </div>
      
      <div class="name">
        花卉白
      </div>
      
      <div>
        #FFFAF0
      </div>
      
      <div>
        rgb(255,250,240)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#D8BFD8">
      <font color="#ffffff"> 
      
      <div class="name">
        Thistle
      </div>
      
      <div class="name">
        蓟紫
      </div>
      
      <div>
        #D8BFD8
      </div>
      
      <div>
        rgb(216,191,216)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#0C4DE">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSteelBlue
      </div>
      
      <div class="name">
        浅钢青
      </div>
      
      <div>
        #0C4DE
      </div>
      
      <div>
        rgb(176,196,222)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00CED1">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkTurquoise
      </div>
      
      <div class="name">
        深松石绿
      </div>
      
      <div>
        #00CED1
      </div>
      
      <div>
        rgb(0,206,209)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FAF0E6">
      <font color="#000000"> 
      
      <div class="name">
        Linen
      </div>
      
      <div class="name">
        亚麻色
      </div>
      
      <div>
        #FAF0E6
      </div>
      
      <div>
        rgb(250,240,230)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#CD853F">
      <font color="#ffffff"> 
      
      <div class="name">
        Peru
      </div>
      
      <div class="name">
        秘鲁红
      </div>
      
      <div>
        #CD853F
      </div>
      
      <div>
        rgb(205,133,63)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFFFF0">
      <font color="#000000"> 
      
      <div class="name">
        Ivory
      </div>
      
      <div class="name">
        象牙白
      </div>
      
      <div>
        #FFFFF0
      </div>
      
      <div>
        rgb(255,255,240)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#DDA0DD">
      <font color="#ffffff"> 
      
      <div class="name">
        Plum
      </div>
      
      <div class="name">
        李紫
      </div>
      
      <div>
        #DDA0DD
      </div>
      
      <div>
        rgb(221,160,221)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#5F9EA0">
      <font color="#ffffff"> 
      
      <div class="name">
        CadetBlue
      </div>
      
      <div class="name">
        军服蓝
      </div>
      
      <div>
        #5F9EA0
      </div>
      
      <div>
        rgb(95,158,160)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#90EE90">
      <font color="#ffffff"> 
      
      <div class="name">
        LightGreen
      </div>
      
      <div class="name">
        浅绿
      </div>
      
      <div>
        #90EE90
      </div>
      
      <div>
        rgb(144,238,144)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFFACD">
      <font color="#000000"> 
      
      <div class="name">
        LemonChiffon
      </div>
      
      <div class="name">
        柠檬绸黄
      </div>
      
      <div>
        #FFFACD
      </div>
      
      <div>
        rgb(255,250,205)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8B4513">
      <font color="#ffffff"> 
      
      <div class="name">
        SaddleBrown
      </div>
      
      <div class="name">
        鞍褐
      </div>
      
      <div>
        #8B4513
      </div>
      
      <div>
        rgb(139,69,19)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFF5EE">
      <font color="#000000"> 
      
      <div class="name">
        SeaShell
      </div>
      
      <div class="name">
        贝壳白
      </div>
      
      <div>
        #FFF5EE
      </div>
      
      <div>
        rgb(255,245,238)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#EE82EE">
      <font color="#ffffff"> 
      
      <div class="name">
        Violet
      </div>
      
      <div class="name">
        紫罗兰色
      </div>
      
      <div>
        #EE82EE
      </div>
      
      <div>
        rgb(238,130,238)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#4682B4">
      <font color="#ffffff"> 
      
      <div class="name">
        SteelBlue
      </div>
      
      <div class="name">
        钢青
      </div>
      
      <div>
        #4682B4
      </div>
      
      <div>
        rgb(70,130,180)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#98FB98">
      <font color="#ffffff"> 
      
      <div class="name">
        PaleGreen
      </div>
      
      <div class="name">
        白绿色
      </div>
      
      <div>
        #98FB98
      </div>
      
      <div>
        rgb(152,251,152)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFEFD5">
      <font color="#000000"> 
      
      <div class="name">
        PapayaWhip
      </div>
      
      <div class="name">
        番木瓜橙
      </div>
      
      <div>
        #FFEFD5
      </div>
      
      <div>
        rgb(255,239,213)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#A0522D">
      <font color="#ffffff"> 
      
      <div class="name">
        Sienna
      </div>
      
      <div class="name">
        土黄赭
      </div>
      
      <div>
        #A0522D
      </div>
      
      <div>
        rgb(160,82,45)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F5FFFA">
      <font color="#000000"> 
      
      <div class="name">
        MintCream
      </div>
      
      <div class="name">
        薄荷乳白
      </div>
      
      <div>
        #F5FFFA
      </div>
      
      <div>
        rgb(245,255,250)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#DA70D6">
      <font color="#ffffff"> 
      
      <div class="name">
        Orchid
      </div>
      
      <div class="name">
        洋兰紫
      </div>
      
      <div>
        #DA70D6
      </div>
      
      <div>
        rgb(218,112,214)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#778899">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSlateGray
      </div>
      
      <div class="name">
        浅岩灰
      </div>
      
      <div>
        #778899
      </div>
      
      <div>
        rgb(119,136,153)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00FA9A">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumSpringGreen
      </div>
      
      <div class="name">
        中嫩绿
      </div>
      
      <div>
        #00FA9A
      </div>
      
      <div>
        rgb(0,250,154)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFEBCD">
      <font color="#000000"> 
      
      <div class="name">
        BlanchedAlmond
      </div>
      
      <div class="name">
        杏仁白
      </div>
      
      <div>
        #FFEBCD
      </div>
      
      <div>
        rgb(255,235,205)
      </div></font>
    </td>
    
    <td id="reds" class="tdborder" bgcolor="#FFE4E1">
      <font color="#000000"> 
      
      <div class="name">
        MistyRose
      </div>
      
      <div class="name">
        雾玫瑰红
      </div>
      
      <div>
        #FFE4E1
      </div>
      
      <div>
        rgb(255,228,225)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F8F8FF">
      <font color="#000000"> 
      
      <div class="name">
        GhostWhite
      </div>
      
      <div class="name">
        幽灵白
      </div>
      
      <div>
        #F8F8FF
      </div>
      
      <div>
        rgb(248,248,255)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#FF00FF">
      <font color="#ffffff"> 
      
      <div class="name">
        Magenta/Fuchsia
      </div>
      
      <div class="name">
        洋红
      </div>
      
      <div>
        #FF00FF
      </div>
      
      <div>
        rgb(255,0,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#708090">
      <font color="#ffffff"> 
      
      <div class="name">
        SlateGray
      </div>
      
      <div class="name">
        岩灰
      </div>
      
      <div>
        #708090
      </div>
      
      <div>
        rgb(112,128,144)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00FF7F">
      <font color="#ffffff"> 
      
      <div class="name">
        SpringGreen
      </div>
      
      <div class="name">
        春绿
      </div>
      
      <div>
        #00FF7F
      </div>
      
      <div>
        rgb(0,255,127)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFE4C4">
      <font color="#000000"> 
      
      <div class="name">
        Bisque
      </div>
      
      <div class="name">
        陶坯黄
      </div>
      
      <div>
        #FFE4C4
      </div>
      
      <div>
        rgb(255,228,196)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFDAB9">
      <font color="#000000"> 
      
      <div class="name">
        PeachPuff
      </div>
      
      <div class="name">
        粉扑桃色
      </div>
      
      <div>
        #FFDAB9
      </div>
      
      <div>
        rgb(255,218,185)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F0FFF0">
      <font color="#000000"> 
      
      <div class="name">
        HoneyDew
      </div>
      
      <div class="name">
        蜜瓜绿
      </div>
      
      <div>
        #F0FFF0
      </div>
      
      <div>
        rgb(240,255,240)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#BA55D3">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumOrchid
      </div>
      
      <div class="name">
        中洋兰紫
      </div>
      
      <div>
        #BA55D3
      </div>
      
      <div>
        rgb(186,85,211)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#7B68EE">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumSlateBlue
      </div>
      
      <div class="name">
        中岩蓝
      </div>
      
      <div>
        #7B68EE
      </div>
      
      <div>
        rgb(123,104,238)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#20B2AA">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSeaGreen
      </div>
      
      <div class="name">
        浅海藻绿
      </div>
      
      <div>
        #20B2AA
      </div>
      
      <div>
        rgb(32,178,170)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F5DEB3">
      <font color="#000000"> 
      
      <div class="name">
        Wheat
      </div>
      
      <div class="name">
        麦色
      </div>
      
      <div>
        #F5DEB3
      </div>
      
      <div>
        rgb(245,222,179)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFA07A">
      <font color="#ffffff"> 
      
      <div class="name">
        LightSalmon
      </div>
      
      <div class="name">
        浅鲑红
      </div>
      
      <div>
        #FFA07A
      </div>
      
      <div>
        rgb(255,160,122)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F5F5F5">
      <font color="#000000"> 
      
      <div class="name">
        WhiteSmoke
      </div>
      
      <div class="name">
        烟雾白
      </div>
      
      <div>
        #F5F5F5
      </div>
      
      <div>
        rgb(245,245,245)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#9370D8">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumPurple
      </div>
      
      <div class="name">
        中紫
      </div>
      
      <div>
        #9370D8
      </div>
      
      <div>
        rgb(147,112,219)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#6A5ACD">
      <font color="#ffffff"> 
      
      <div class="name">
        SlateBlue
      </div>
      
      <div class="name">
        岩蓝
      </div>
      
      <div>
        #6A5ACD
      </div>
      
      <div>
        rgb(106,90,205)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#2E8B57">
      <font color="#ffffff"> 
      
      <div class="name">
        SeaGreen
      </div>
      
      <div class="name">
        海藻绿
      </div>
      
      <div>
        #2E8B57
      </div>
      
      <div>
        rgb(46,139,87)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFE4B5">
      <font color="#000000"> 
      
      <div class="name">
        Moccasin
      </div>
      
      <div class="name">
        鹿皮色
      </div>
      
      <div>
        #FFE4B5
      </div>
      
      <div>
        rgb(255,228,181)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FF7F50">
      <font color="#ffffff"> 
      
      <div class="name">
        Coral
      </div>
      
      <div class="name">
        珊瑚红
      </div>
      
      <div>
        #FF7F50
      </div>
      
      <div>
        rgb(255,127,80)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FAEBD7">
      <font color="#000000"> 
      
      <div class="name">
        AntiqueWhite
      </div>
      
      <div class="name">
        古董白
      </div>
      
      <div>
        #FAEBD7
      </div>
      
      <div>
        rgb(250,235,215)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#8A2BE2">
      <font color="#ffffff"> 
      
      <div class="name">
        BlueViolet
      </div>
      
      <div class="name">
        蓝紫色
      </div>
      
      <div>
        #8A2BE2
      </div>
      
      <div>
        rgb(138,43,226)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#483D8B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSlateBlue
      </div>
      
      <div class="name">
        深岩蓝
      </div>
      
      <div>
        #483D8B
      </div>
      
      <div>
        rgb(72,61,139)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#3CB371">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumSeaGreen
      </div>
      
      <div class="name">
        中海藻绿
      </div>
      
      <div>
        #3CB371
      </div>
      
      <div>
        rgb(60,179,113)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFDEAD">
      <font color="#000000"> 
      
      <div class="name">
        NavajoWhite
      </div>
      
      <div class="name">
        土著白
      </div>
      
      <div>
        #FFDEAD
      </div>
      
      <div>
        rgb(255,222,173)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FF8C00">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkOrange
      </div>
      
      <div class="name">
        深橙
      </div>
      
      <div>
        #FF8C00
      </div>
      
      <div>
        rgb(255,140,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#DCDCDC">
      <font color="#000000"> 
      
      <div class="name">
        GainsBoro
      </div>
      
      <div class="name">
        庚氏灰
      </div>
      
      <div>
        #DCDCDC
      </div>
      
      <div>
        rgb(220,220,220)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#9400d3">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkViolet
      </div>
      
      <div class="name">
        深紫
      </div>
      
      <div>
        #9400d3
      </div>
      
      <div>
        rgb(148,0,211)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#0000FF">
      <font color="#ffffff"> 
      
      <div class="name">
        Blue
      </div>
      
      <div class="name">
        蓝色
      </div>
      
      <div>
        #0000FF
      </div>
      
      <div>
        rgb(0,0,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#8FBC8F">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSeaGreen
      </div>
      
      <div class="name">
        深海藻绿
      </div>
      
      <div>
        #8FBC8F
      </div>
      
      <div>
        rgb(143,188,143)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#EEE8AA">
      <font color="#000000"> 
      
      <div class="name">
        PaleGoldenRod
      </div>
      
      <div class="name">
        白金菊黄
      </div>
      
      <div>
        #EEE8AA
      </div>
      
      <div>
        rgb(238,232,170)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F08080">
      <font color="#ffffff"> 
      
      <div class="name">
        LightCoral
      </div>
      
      <div class="name">
        浅珊瑚红
      </div>
      
      <div>
        #F08080
      </div>
      
      <div>
        rgb(240,128,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#D3D3D3">
      <font color="#ffffff"> 
      
      <div class="name">
        LightGray
      </div>
      
      <div class="name">
        亮灰
      </div>
      
      <div>
        #D3D3D3
      </div>
      
      <div>
        rgb(211,211,211)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#9932CC">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkOrchid
      </div>
      
      <div class="name">
        深洋兰紫
      </div>
      
      <div>
        #9932CC
      </div>
      
      <div>
        rgb(153,50,204)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#0000CD">
      <font color="#ffffff"> 
      
      <div class="name">
        MediumBlue
      </div>
      
      <div class="name">
        中蓝
      </div>
      
      <div>
        #0000CD
      </div>
      
      <div>
        rgb(0,0,205)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#228B22">
      <font color="#ffffff"> 
      
      <div class="name">
        ForestGreen
      </div>
      
      <div class="name">
        森林绿
      </div>
      
      <div>
        #228B22
      </div>
      
      <div>
        rgb(34,139,34)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#F0E68C">
      <font color="#ffffff"> 
      
      <div class="name">
        Khaki
      </div>
      
      <div class="name">
        卡其色
      </div>
      
      <div>
        #F0E68C
      </div>
      
      <div>
        rgb(240,230,140)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#BC8F8F">
      <font color="#ffffff"> 
      
      <div class="name">
        RosyBrown
      </div>
      
      <div class="name">
        玫瑰褐
      </div>
      
      <div>
        #BC8F8F
      </div>
      
      <div>
        rgb(188,143,143)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#C0C0C0">
      <font color="#ffffff"> 
      
      <div class="name">
        Silver
      </div>
      
      <div class="name">
        银色
      </div>
      
      <div>
        #C0C0C0
      </div>
      
      <div>
        rgb(192,192,192)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#8B008B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkMagenta
      </div>
      
      <div class="name">
        深品红
      </div>
      
      <div>
        #8B008B
      </div>
      
      <div>
        rgb(139,0,139)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#191970">
      <font color="#ffffff"> 
      
      <div class="name">
        MidNightBlue
      </div>
      
      <div class="name">
        午夜蓝
      </div>
      
      <div>
        #191970
      </div>
      
      <div>
        rgb(25,25,112)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#008000">
      <font color="#ffffff"> 
      
      <div class="name">
        Green
      </div>
      
      <div class="name">
        调和绿
      </div>
      
      <div>
        #008000
      </div>
      
      <div>
        rgb(0,128,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#BDB76B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkKhaki
      </div>
      
      <div class="name">
        深卡其色
      </div>
      
      <div>
        #BDB76B
      </div>
      
      <div>
        rgb(189,183,107)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#CD5C5C">
      <font color="#ffffff"> 
      
      <div class="name">
        IndianRed
      </div>
      
      <div class="name">
        印度红
      </div>
      
      <div>
        #CD5C5C
      </div>
      
      <div>
        rgb(205,92,92)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#A9A9A9">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkGray
      </div>
      
      <div class="name">
        暗灰
      </div>
      
      <div>
        #A9A9A9
      </div>
      
      <div>
        rgb(169,169,169)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#800080">
      <font color="#ffffff"> 
      
      <div class="name">
        Purple
      </div>
      
      <div class="name">
        紫色
      </div>
      
      <div>
        #800080
      </div>
      
      <div>
        rgb(128,0,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00008B">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkBlue
      </div>
      
      <div class="name">
        深蓝
      </div>
      
      <div>
        #00008B
      </div>
      
      <div>
        rgb(0,0,139)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#006400">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkGreen
      </div>
      
      <div class="name">
        深绿
      </div>
      
      <div>
        #006400
      </div>
      
      <div>
        rgb(0,100,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFFF00">
      <font color="#ffffff"> 
      
      <div class="name">
        Yellow
      </div>
      
      <div class="name">
        黄色
      </div>
      
      <div>
        #FFFF00
      </div>
      
      <div>
        rgb(255,255,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FA8072">
      <font color="#ffffff"> 
      
      <div class="name">
        Salmon
      </div>
      
      <div class="name">
        鲑红
      </div>
      
      <div>
        #FA8072
      </div>
      
      <div>
        rgb(250,128,114)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#808080">
      <font color="#ffffff"> 
      
      <div class="name">
        Gray
      </div>
      
      <div class="name">
        灰色
      </div>
      
      <div>
        #808080
      </div>
      
      <div>
        rgb(128,128,128)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td class="tdborder" bgcolor="#4B0082">
      <font color="#ffffff"> 
      
      <div class="name">
        Indigo
      </div>
      
      <div class="name">
        靛蓝
      </div>
      
      <div>
        #4B0082
      </div>
      
      <div>
        rgb(75,0,130)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#000080">
      <font color="#ffffff"> 
      
      <div class="name">
        Navy
      </div>
      
      <div class="name">
        藏青
      </div>
      
      <div>
        #000080
      </div>
      
      <div>
        rgb(0,0,128)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#00FF00">
      <font color="#ffffff"> 
      
      <div class="name">
        Lime
      </div>
      
      <div class="name">
        绿色
      </div>
      
      <div>
        #00FF00
      </div>
      
      <div>
        rgb(0,255,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FFD700">
      <font color="#ffffff"> 
      
      <div class="name">
        Gold
      </div>
      
      <div class="name">
        金色
      </div>
      
      <div>
        #FFD700
      </div>
      
      <div>
        rgb(255,215,0)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#E9967A">
      <font color="#ffffff"> 
      
      <div class="name">
        DarkSalmon
      </div>
      
      <div class="name">
        深鲑红
      </div>
      
      <div>
        #E9967A
      </div>
      
      <div>
        rgb(233,150,122)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#696969">
      <font color="#ffffff"> 
      
      <div class="name">
        DimGray
      </div>
      
      <div class="name">
        昏灰
      </div>
      
      <div>
        #696969
      </div>
      
      <div>
        rgb(105,105,105)
      </div></font>
    </td>
  </tr>
  
  <tr>
    <td id="blues" class="tdborder" bgcolor="#F0F8FF">
      <font color="#000000"> 
      
      <div class="name">
        AliceBlue
      </div>
      
      <div class="name">
        爱丽丝蓝
      </div>
      
      <div>
        #F0F8FF
      </div>
      
      <div>
        rgb(240,248,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#E0FFFF">
      <font color="#000000"> 
      
      <div class="name">
        LightCyan
      </div>
      
      <div class="name">
        浅青
      </div>
      
      <div>
        #E0FFFF
      </div>
      
      <div>
        rgb(224,255,255)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#32CD32">
      <font color="#ffffff"> 
      
      <div class="name">
        LimeGreen
      </div>
      
      <div class="name">
        青柠绿
      </div>
      
      <div>
        #32CD32
      </div>
      
      <div>
        rgb(50,205,50)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#DAA520">
      <font color="#ffffff"> 
      
      <div class="name">
        GoldenRod
      </div>
      
      <div class="name">
        金菊黄
      </div>
      
      <div>
        #DAA520
      </div>
      
      <div>
        rgb(218,165,32)
      </div></font>
    </td>
    
    <td class="tdborder" bgcolor="#FF6347">
      <font color="#ffffff"> 
      
      <div class="name">
        Tomato
      </div>
      
      <div class="name">
        番茄红
      </div>
      
      <div>
        #FF6347
      </div>
      
      <div>
        rgb(255,99,71)
      </div></font>
    </td>
    
    <td id="blacks" class="tdborder" bgcolor="#000000">
      <font color="#ffffff"> 
      
      <div class="name">
        Black
      </div>
      
      <div class="name">
        黑色
      </div>
      
      <div>
        #000000
      </div>
      
      <div>
        rgb(0,0,0)
      </div></font>
    </td>
  </tr>
</table>

[342色部分](#allColor)翻译可能不太准确，如有发现错漏还请留言正确的翻译，谢谢。
<article class="post-238 post type-post status-publish format-standard hentry category-wordpress tag-gutenberg tag-wordpress tag-19 tag-16">

				<div class="post-details">

						<div class="post-details-thumb">

							[![](https://secure.gravatar.com/avatar/75c83efa949a9f0a64363934cdabf889?s=200&amp;d=mm&amp;r=g)](https://www.tidnotes.ga/author/tid)

						</div><!--/.post-details-thumb-->

					<div class="post-details-day">30</div>

					<div class="post-details-month">8月</div>

					<div class="post-details-year">2019</div>

				</div>

# WordPress之Gutenberg（古腾堡）自定义块工具栏

*   [TiD](https://www.tidnotes.ga/author/tid "由TiD发布")
*   [WordPress使用技巧](https://www.tidnotes.ga/category/wordpress%e4%bd%bf%e7%94%a8%e6%8a%80%e5%b7%a7)
*   [3](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8bgutenberg%ef%bc%88%e5%8f%a4%e8%85%be%e5%a0%a1%ef%bc%89%e8%87%aa%e5%ae%9a%e4%b9%89%e5%9d%97%e5%b7%a5%e5%85%b7%e6%a0%8f.html#comments)<!--/.post-meta-->

				<div class="clear"></div>

				<div class="entry">	

> _本文内容主要参考&nbsp;_[Gutenberg 开发API](https://wordpress.org/gutenberg/handbook/designers-developers/developers/block-api/)_&nbsp;，介绍并解读新版WordPress所采用的&nbsp;Gutenberg 编辑器&nbsp;（ Block Editor/块编辑器 ）如何创建自定义编辑块，包括块的样式以及扩展工具栏等。_
> <cite> _本文适用于WordPress 5.2.2。关于WordPress Gutenberg自定义系列目录如下：_
> _1、_[WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163)
> _2、_[WordPress之Gutenberg（古腾堡）自定义块（二）](https://www.tidnotes.ga/?p=208)
> _3、_[WordPress之Gutenberg（古腾堡）自定义块扩展栏](https://www.tidnotes.ga/?p=214)
> _4、[WordPress之Gutenberg（古腾堡）自定义块工具栏](https://www.tidnotes.ga/?p=238)_ </cite>

WordPress Gutenberg（古腾堡）除了可以自定义区块、扩展栏，也可以自定义块工具栏。利用`wp<span class="token punctuation">.</span>richText<span class="token punctuation">.</span><span class="token function">registerFormatType</span><span class="token punctuation">(</span><span class="token punctuation">)</span>`可以自定义特有样式用于自定义工具栏，且可以在全部文本编辑块中以工具栏形式呈现。自定义块也可以用`wp<span class="token punctuation">.</span>editor<span class="token punctuation">.</span>BlockControls`显示特有工具栏。

<span id="more-238"></span>

<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

## 效果截图

<figure class="wp-block-image">[![Gutenberg（古腾堡）自定义块工具栏 | 小TiD笔记](https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5.png)](https://www.tidnotes.ga/wp-content/uploads/2019/08/image-5.png)</figure>

  本文效果同《[WordPress之经典区块自定义按钮](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e7%bb%8f%e5%85%b8%e5%8c%ba%e5%9d%97%e8%87%aa%e5%ae%9a%e4%b9%89%e6%8c%89%e9%92%ae.html)》一文，将选中的代码更改为选中的样式。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

##  详细教程 

基本步骤如下：

1.  在functions.php中注册相关的脚本文件
2.  编辑工具栏JS文件
3.  编辑css外观

自定义块工具栏和自定义块基本步骤一样，但在编辑块中注册并不需要引入css文件，css文件只需要引入主题css用于在文章显示。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

### 注册新格式

找到你主题的 function.php文件，在最下方添加以下代码：

<div style="position: relative;">

    <span class="token comment">//古腾堡编辑器工具栏</span>
    <span class="token keyword keyword-function">function</span> <span class="token function">my_custom_format_script_register</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">wp_register_script</span><span class="token punctuation">(</span>
            <span class="token string">'my-custom-format-js'</span><span class="token punctuation">,</span>
            <span class="token function">get_stylesheet_directory_uri</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token string">'/js/my-custom-format.js'</span><span class="token punctuation">,</span>
            <span class="token keyword keyword-array">array</span><span class="token punctuation">(</span> <span class="token string">'wp-rich-text'</span><span class="token punctuation">,</span> <span class="token string">'wp-element'</span><span class="token punctuation">,</span> <span class="token string">'wp-editor'</span><span class="token punctuation">,</span> <span class="token string">'wp-components'</span> <span class="token punctuation">)</span>
        <span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token function">add_action</span><span class="token punctuation">(</span> <span class="token string">'init'</span><span class="token punctuation">,</span> <span class="token string">'my_custom_format_script_register'</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword keyword-function">function</span> <span class="token function">my_custom_format_enqueue_assets_editor</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">wp_enqueue_script</span><span class="token punctuation">(</span> <span class="token string">'my-custom-format-js'</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token function">add_action</span><span class="token punctuation">(</span> <span class="token string">'enqueue_block_editor_assets'</span><span class="token punctuation">,</span> <span class="token string">'my_custom_format_enqueue_assets_editor'</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token comment">//Wordpress免插件实现代码高亮</span>
    <span class="token comment">//Prism.js开始</span>
    <span class="token keyword keyword-function">function</span> <span class="token function">add_prism</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token function">wp_register_style</span><span class="token punctuation">(</span>
                <span class="token string">'prismCSS'</span><span class="token punctuation">,</span> 
                <span class="token function">get_stylesheet_directory_uri</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">.</span> <span class="token string">'/css/prism.css'</span> <span class="token comment">//自定义路径</span>
             <span class="token punctuation">)</span><span class="token punctuation">;</span>
              <span class="token function">wp_register_script</span><span class="token punctuation">(</span>
                <span class="token string">'prismJS'</span><span class="token punctuation">,</span>
                <span class="token function">get_stylesheet_directory_uri</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">.</span> <span class="token string">'/js/prism.js'</span> <span class="token comment">//自定义路径</span>
             <span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token function">wp_enqueue_style</span><span class="token punctuation">(</span><span class="token string">'prismCSS'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token function">wp_enqueue_script</span><span class="token punctuation">(</span><span class="token string">'prismJS'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token function">add_action</span><span class="token punctuation">(</span><span class="token string">'wp_enqueue_scripts'</span><span class="token punctuation">,</span> <span class="token string">'add_prism'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//Prism.js结束</span><span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></span>`</pre><button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button></div>

    wp-rich-text是注册新样式必须的，wp-element、wp-editor是自定义工具栏必须的，其他的根据需要添加到PHP文件中的dependencies数组。

    <div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

    ### 编辑js文件

    在你主题的js文件夹添加my-custom-format.js（根据自己的位置添加），添加以下代码：

    <div style="position: relative;"><pre class="line-numbers language-js">`<span class="token punctuation">(</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span> wp <span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword keyword-var">var</span> el <span class="token operator">=</span> wp<span class="token punctuation">.</span>element<span class="token punctuation">.</span>createElement<span class="token punctuation">;</span>
        <span class="token keyword keyword-var">var</span> BlockControls <span class="token operator">=</span> wp<span class="token punctuation">.</span>editor<span class="token punctuation">.</span>BlockControls<span class="token punctuation">;</span>
        <span class="token keyword keyword-var">var</span> DropdownMenu <span class="token operator">=</span> wp<span class="token punctuation">.</span>components<span class="token punctuation">.</span>DropdownMenu<span class="token punctuation">;</span>
        <span class="token keyword keyword-var">var</span> richText <span class="token operator">=</span> wp<span class="token punctuation">.</span>richText<span class="token punctuation">;</span>

        <span class="token keyword keyword-const">const</span> <span class="token function-variable function">MyDropdownMenu</span> <span class="token operator">=</span> <span class="token keyword keyword-function">function</span> <span class="token punctuation">(</span>props<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword keyword-return">return</span> <span class="token function">el</span><span class="token punctuation">(</span>
                BlockControls<span class="token punctuation">,</span> 
                <span class="token keyword keyword-null">null</span><span class="token punctuation">,</span> 
                <span class="token function">el</span><span class="token punctuation">(</span>
                    <span class="token string">'div'</span><span class="token punctuation">,</span>
                    <span class="token punctuation">{</span>className<span class="token punctuation">:</span> <span class="token string">'components-toolbar'</span><span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token function">el</span><span class="token punctuation">(</span>
                        DropdownMenu<span class="token punctuation">,</span>
                        <span class="token punctuation">{</span>
                            icon<span class="token punctuation">:</span> <span class="token string">'editor-code'</span><span class="token punctuation">,</span>
                            label<span class="token punctuation">:</span> <span class="token string">'选择语言类型'</span><span class="token punctuation">,</span>
                            controls<span class="token punctuation">:</span> <span class="token punctuation">[</span>
                                <span class="token punctuation">{</span>
                                    icon<span class="token punctuation">:</span> <span class="token string">'editor-code'</span><span class="token punctuation">,</span>
                                    title<span class="token punctuation">:</span> <span class="token string">'js代码'</span><span class="token punctuation">,</span>
                                    onClick<span class="token punctuation">:</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                                        props<span class="token punctuation">.</span><span class="token function">onChange</span><span class="token punctuation">(</span> richText<span class="token punctuation">.</span><span class="token function">toggleFormat</span><span class="token punctuation">(</span>
                                            props<span class="token punctuation">.</span>value<span class="token punctuation">,</span>
                                            <span class="token punctuation">{</span> type<span class="token punctuation">:</span> <span class="token string">'core/my-code'</span> <span class="token punctuation">}</span>
                                        <span class="token punctuation">)</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>
                                    <span class="token punctuation">}</span>
                                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                                <span class="token punctuation">{</span>
                                    icon<span class="token punctuation">:</span> <span class="token string">'editor-code'</span><span class="token punctuation">,</span>
                                    title<span class="token punctuation">:</span> <span class="token string">'html代码'</span><span class="token punctuation">,</span>
                                    onClick<span class="token punctuation">:</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                                        props<span class="token punctuation">.</span><span class="token function">onChange</span><span class="token punctuation">(</span> richText<span class="token punctuation">.</span><span class="token function">toggleFormat</span><span class="token punctuation">(</span>
                                            props<span class="token punctuation">.</span>value<span class="token punctuation">,</span>                                        
                                            <span class="token punctuation">{</span>type<span class="token punctuation">:</span> <span class="token string">'code'</span><span class="token punctuation">,</span> attributes<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token keyword keyword-class">class</span><span class="token punctuation">:</span> <span class="token string">'language-markup'</span><span class="token punctuation">}</span><span class="token punctuation">}</span>
                                        <span class="token punctuation">)</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>
                                    <span class="token punctuation">}</span>
                                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                                <span class="token punctuation">{</span>
                                    icon<span class="token punctuation">:</span> <span class="token string">'editor-code'</span><span class="token punctuation">,</span>
                                    title<span class="token punctuation">:</span> <span class="token string">'css代码'</span><span class="token punctuation">,</span>
                                    onClick<span class="token punctuation">:</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                                        props<span class="token punctuation">.</span><span class="token function">onChange</span><span class="token punctuation">(</span> richText<span class="token punctuation">.</span><span class="token function">toggleFormat</span><span class="token punctuation">(</span>
                                            props<span class="token punctuation">.</span>value<span class="token punctuation">,</span>                                        
                                            <span class="token punctuation">{</span>type<span class="token punctuation">:</span> <span class="token string">'code'</span><span class="token punctuation">,</span> attributes<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token keyword keyword-class">class</span><span class="token punctuation">:</span> <span class="token string">'language-css'</span><span class="token punctuation">}</span><span class="token punctuation">}</span>
                                        <span class="token punctuation">)</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>
                                    <span class="token punctuation">}</span>
                                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                            <span class="token punctuation">]</span><span class="token punctuation">,</span>
                        <span class="token punctuation">}</span><span class="token punctuation">)</span>
                    <span class="token punctuation">)</span>
            <span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token comment">/* -------创建定义工具栏---------*/</span>
        richText<span class="token punctuation">.</span><span class="token function">registerFormatType</span><span class="token punctuation">(</span>
            <span class="token string">'core/my-code'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
                title<span class="token punctuation">:</span> <span class="token string">'code html'</span><span class="token punctuation">,</span>
                tagName<span class="token punctuation">:</span> <span class="token string">'code'</span><span class="token punctuation">,</span>
                className<span class="token punctuation">:</span> <span class="token string">'language-js'</span><span class="token punctuation">,</span>
                edit<span class="token punctuation">:</span> MyDropdownMenu<span class="token punctuation">,</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token punctuation">)</span><span class="token punctuation">(</span> window<span class="token punctuation">.</span>wp <span class="token punctuation">)</span><span class="token punctuation">;</span><span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></span>`</pre><button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button></div>

    以上是利用注册新样式来添加自定义工具栏，如果不需要注册新样式且只在特定块中显示该工具栏，只需要在所需工具栏中edit函数中添加MyDropdownMenu这一部分即可。

    如果只是需要的只是单个按钮，而不是下拉框，则可以将 MyDropdownMenu 改为以下的 MyCustomButton 。

    <div style="position: relative;"><pre class="line-numbers language-js">`<span class="token keyword keyword-var">var</span> <span class="token function-variable function">MyCustomButton</span> <span class="token operator">=</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span> props <span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword keyword-return">return</span> wp<span class="token punctuation">.</span>element<span class="token punctuation">.</span><span class="token function">createElement</span><span class="token punctuation">(</span>
            wp<span class="token punctuation">.</span>editor<span class="token punctuation">.</span>RichTextToolbarButton<span class="token punctuation">,</span> <span class="token punctuation">{</span>
                icon<span class="token punctuation">:</span> <span class="token string">'editor-code'</span><span class="token punctuation">,</span>
                title<span class="token punctuation">:</span> <span class="token string">'Sample output'</span><span class="token punctuation">,</span>
                onClick<span class="token punctuation">:</span> <span class="token keyword keyword-function">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                    <span class="token comment">//自定义函数</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></span>
<button name="copy-btn" style="position: absolute;top: 3px;right: 3px;border-radius: 5px;">点击复制</button></div>

#### 语法解析：

*   **wp.editor.BlockControls**：工具栏显示元素。
*   **wp.editor.RichTextToolbarButton**：富文本按钮，基本属性如下。

        *   icon：图标，同自定义块图标一样
    *   title：显示的附带文字
    *   label：鼠标焦点时的提示文字
    *   onClick：点击调用函数
*   **wp.components.DropdownMenu**：下拉框组件，其中controls为按钮的列表，按钮的属性与 **wp.editor.RichTextToolbarButton** 相同。
*   **wp.richText.toggleFormat()**：对选中的内容应用样式，第一个变量为内容，第二个变量为样式对象。已注册样式格式为`<span class="token punctuation">{</span> type<span class="token punctuation">:</span> <span class="token string">'样式名'</span> <span class="token punctuation">}</span>`，未注册可以用`<span class="token punctuation">{</span>type<span class="token punctuation">:</span> <span class="token string">'标签名'</span><span class="token punctuation">,</span> attributes<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token keyword keyword-class">class</span><span class="token punctuation">:</span> <span class="token string">'类名'</span><span class="token punctuation">}</span><span class="token punctuation">}</span>`。
*   **wp.richText.registerFormatType()：**注册新样式，新样式命名规则同自定义块相同。对象的属性如下。

        *   title：样式显示名
    *   tagName：标签名
    *   className：预设类名
    *   edit：同自定义块edit函数

### CSS文件部分

本文主要为实现选中代码高亮，所以同 《[WordPress之经典区块自定义按钮](https://www.tidnotes.ga/2019/08/wordpress%e4%b9%8b%e7%bb%8f%e5%85%b8%e5%8c%ba%e5%9d%97%e8%87%aa%e5%ae%9a%e4%b9%89%e6%8c%89%e9%92%ae.html)》一文的css文件一样，这部分如有问题可以去前文去看看，这里不做详细解释。

<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

_**WordPress Gutenberg其他相关自定义系列文章：**_
 _1、_[WordPress之Gutenberg（古腾堡）自定义块（一）](https://www.tidnotes.ga/?p=163)
_2、_[WordPress之Gutenberg（古腾堡）自定义块（二）](https://www.tidnotes.ga/?p=208)
_3、_[WordPress之Gutenberg（古腾堡）自定义块扩展栏](https://www.tidnotes.ga/?p=214)

					<div class="clear"></div>				

				</div><!--/.entry-->

			</article>

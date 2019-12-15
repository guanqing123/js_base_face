## 第八章 运行环境 ##
### 8-1 介绍 ###
#### 运行环境 ####
- 浏览器就可以通过访问链接来得到页面的内容
- 通过绘制和渲染，显示出页面的最终的样子
- 整个过程中，我们需要考虑什么问题？
#### 知识点 ####
- 页面加载过程
- 性能优化
- 安全性
#### 结束 ####
### 8-2 页面加载-渲染过程 ###
#### 页面加载 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 从输入url到得到html的详细过程
- window.onload 和 DOMContentLoaded 的区别
#### 知识点 ####
- 加载资源的形式
- 加载一个资源的过程
- 浏览器渲染页面的过程
#### 加载资源的形式 ####
- 输入 url (或跳转页面) 加载 html
- http://coding.m.imooc.com
- 加载 html 中的静态资源
- `<script src="/static/js/jquery.js"></script>`
#### 加载一个资源的过程 ####
- 浏览器根据 DNS 服务器得到域名的 IP 地址
- 向这个 IP 的机器发送 http 请求
- 服务器收到、处理并返回 http 请求
- 浏览器得到返回内容
#### 浏览器渲染页面的过程 ####
- 根据 HTML 结构生成 DOM Tree
- 根据 CSS 生成 CSSOM
- 将 DOM 和 CSSOM 整合形成 RenderTree
- 根据 RenderTree 开始渲染和展示
- 遇到`<script>`时，会执行并阻塞渲染
### 8-3 页面加载-几种示例 ###
#### 示例一 ####
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;Title&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;p&gt;test&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
#### 示例二 ####
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;Title&lt;/title&gt;
    &lt;link rel="stylesheet" type="text/css" href="test.css"&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div&gt;test&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
<pre>
div {
    width: 100%;
    height: 100px;
    font-size: 50px;
}
</pre>
#### 思考 ####
- 为何要把 css 放在 head 中?
#### 示例三 ####
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="container"&gt;default&lt;/div&gt;
    &lt;script src="index.js"&gt;&lt;/script&gt;
    &lt;p&gt;test&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
<pre>
document.getElementById('container').innerHTML = 'update by js'
</pre>
#### 思考 ####
- 为何要把 js 放在body最下面?
#### 示例四 ####
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;p&gt;test&lt;/p&gt;
    &lt;p&gt;&lt;img src="test.png"/&gt;&lt;/p&gt;
    &lt;p&gt;test&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
#### window.onload 和 DOMContentLoaded ####
<pre>
window.addEventListener('load', function () {
    // 页面的全部资源加载完才会执行，包括图片、视频等
})
document.addEventListener('DOMContentLoaded', function () {
    // DOM 渲染完即可执行，此时图片、视频还可能没有加载完
})
</pre>
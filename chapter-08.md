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
### 8-4 页面加载-解答 ###
#### 解答 ####
- 从输入url到得到html的详细过程
	- 浏览器根据 DNS 服务器得到域名的 IP 地址
	- 向这个 IP 的机器发送 http 请求
	- 服务器收到、处理并返回 http 请求
	- 浏览器得到返回内容
- window.onload 和 DOMContentLoaded 的区别
	- 页面的全部资源加载完才会执行，包括图片、视频等
	- DOM 渲染完即可执行，此时图片、视频还没有加载完
### 8-5 性能优化-优化策略 ###
#### 性能优化 ####
- 这本身就是一个综合性的问题
- 没有标准答案、如果要非常全面，能写一本书...
- 只要关注核心点，针对面试
#### 原则 ####
- 多使用内存、缓存或者其他方法
- 减少 CPU 计算、减少网络
#### 从哪里入手 ####
- 加载页面和静态资源
- 页面渲染
#### 加载资源优化 ####
- 静态资源的压缩合并
- 静态资源缓存
- 使用 CDN 让资源加载更快
- 使用 SSR 后端渲染，数据直接输出到 HTML 中
#### 渲染优化 ####
- CSS 放前面，JS 放后面
- 懒加载(图片懒加载、下拉加载更多)
- 减少 DOM 查询，对 DOM 查询做缓存
- 减少 DOM 操作，多个操作尽量合并在一起执行
- 事件节流
- 尽早执行操作(如 DOMContentLoaded)
### 8-6 性能优化-几个示例 ###
#### 资源合并 ####
<pre>
&lt;script src="a.js"&gt;&lt;/script&gt;
&lt;script src="b.js"&gt;&lt;/script&gt;
&lt;script src="c.js"&gt;&lt;/script&gt;
</pre>
<pre>
&lt;script src="abc.js"&gt;&lt;/script&gt;
</pre>
#### 缓存 ####
- 通过连接名称控制缓存
- `<script src="abc_1.js"></script>`
- 只有内容改变的时候，链接名称才会改变
- `<script src="abc_2.js"></script>`
#### CDN ####
`<link href="https://cdn.bootcss.com/twitter-bootstrap/4.3.1/css/bootstrap.css" rel="stylesheet">`
`<script src="https://cdn.bootcss.com/zepto/1.0rc1/zepto.min.js"></script>`
#### 使用SSR后端渲染 ####
- 现在Vue React提出了这样的概念
- 其实jsp php asp都属于后端渲染
#### 懒加载 ####
<pre>
&lt;img id="img1" src="preview.png" data-realsrc="abc.png"/&gt;
&lt;script type="text/javascript"&gt;
    var img1 = document.getElementById('img1')
    img1.src = img1.getAttribute('data-realsrc')
&lt;/script&gt;
</pre>
#### 缓存DOM查询 ####
<pre>
// 未缓存 DOM 查询
var i
for (i =0; i &lt; document.getElementsByTagName('p').length; i++) {
    // todo
}

// 缓存了 DOM 查询
var pList = document.getElementsByTagName('p')
var i
for (i =0; i &lt; pList.length; i++) {
    // todo
}
</pre>
#### 合并DOM插入 ####
<pre>
var listNode = document.getElementById('list')

// 要插入 10 个 li 标签
var frag = document.createDocumentFragment();
var x, li;
for (x = 0; x < 10; x++) {
    li = document.createElement("li");
    li.innerHTML = "List item " + x;
    frag.appendChild(li);
}

listNode.appendChild(frag);
</pre>
#### 事件节流 ####
<pre>
var textarea = document.getElementById('text')
var timeoutId
textarea.addEventListener('keyup', function () {
    if (timeoutId) {
        clearTimeout(timeoutId)
    }
    timeoutId = setTimeout(function () {
        // 触发 change 事件
    }, 100)
})
</pre>
### 8-7 安全性-XSS ###
#### 安全性 ####
- 综合性的问题：场景的前端安全问题有哪些
#### 知识点 ####
- XSS跨站请求攻击
- XSRF跨站请求伪造
#### XSS ####
- 在新浪博客写一篇文章，同时偷偷插入一段`<script>`
- 攻击代码中，获取cookie，发送自己的服务器
- 发布博客，有人查看博客内容
- 会把查看者的cookie发送到攻击者的服务器
- 前端替换关键字，例如替换 < 为 `&lt;` > 为 `&gt;`
- 后端替换
### 8-8 安全性-XSRF ###
- 你已登录一个购物网站，正在浏览商品
- 该网站付费接口是 xxx.com/pay?id=100 但是没有任何验证
- 然后你收到一封邮件，隐藏着 <img src=xxx.com/pay?id=100>
- 你查看邮件的时候，就已经悄悄的付费购买了
- 增加验证流程，如输入指纹、密码、短信验证码
### 8-9 面试技巧 ###
#### 技巧 ####
- 简历
- 过程中...
#### 简历 ####
- 简洁明了，重点突出项目经历和解决方案
- 把个人博客放在简历中，并且定期维护更新博客
- 把个人的开源项目放在简历中，并维护开源项目
- 简历千万不要造假，要保持能力和经历上的真实性
#### 面试过程中 ####
- 如何看待加班?加班就像借钱，救急不就穷
- 千万不可挑战面试官，不要反考面试官
- 学会给面试官惊喜，但不要太多
- 遇到不会回答的问题，说出你知道的也可以
- 谈谈你的缺点----说一下你最近在学什么就可以了
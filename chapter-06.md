## 第六章 JS-Web-API （下） ##
### 6-1 事件-知识点 ###
#### 事件 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 编写一个通用的事件监听函数
- 描述事件冒泡流程
- 对于一个无限下拉加载图片的页面,如何给每个图片绑定事件
#### 知识点 ####
- 通用事件绑定
- 事件冒泡
- 代理
#### 通用事件绑定 ####
<pre>
var btn = document.getElementById('btn1')
btn.addEventListener('click', function (event) {
  console.log('clicked')
})

function bindEvent(elem, type, fn) {
  elem.addEventListener(type, fn)
}
var a = document.getElementById('link1')
bindEvent(a, 'click', function(e){
  e.preventDefault() // 阻止默认行为
  alert('clicked')
})
</pre>
#### 关于IE低版本的兼容性 ####
- IE低版本使用 <b>attachEvent</b> 绑定事件,和 W3C 标准不一样
- IE低版本使用量已非常少,很多网站都早已不支持
- 建议对IE低版本的兼容性：了解即可,无需深究
- 如果遇到对IE低版本要求苛刻的面试,果断放弃
#### 事件冒泡 ####
<pre>
&lt;body&gt;
  &lt;div id="div1"&gt;
    &lt;p id="p1"&gt;激活&lt;/p&gt;
    &lt;p id="p2"&gt;取消&lt;/p&gt;
    &lt;p id="p3"&gt;取消&lt;/p&gt;
    &lt;p id="p4"&gt;取消&lt;/p&gt;
  &lt;/div&gt;
  &lt;div id="div2"&gt;
    &lt;p id="p5"&gt;取消&lt;/p&gt;
    &lt;p id="p6"&gt;取消&lt;/p&gt;
  &lt;/div&gt;
&lt;/body&gt;
</pre>
<pre>
function bindEvent(elem, type, fn) {
  elem.addEventListener(type, fn)
}
var p1 = document.getElementById('p1')
bindEvent(p1, 'click', function (e) {
  e.stopPropagation()
  alert('激活')
})
var body = document.body
bindEvent(body, 'click', function (){
  alert('取消')
})
</pre>
#### 代理 ####
<pre>
&lt;div id="div1"&gt;
  &lt;a href="#"&gt;a1&lt;/a&gt;
  &lt;a href="#"&gt;a2&lt;/a&gt;
  &lt;a href="#"&gt;a3&lt;/a&gt;
  &lt;a href="#"&gt;a4&lt;/a&gt;
  &lt;!--会随时新增更多 a 标签--&gt;
&lt;/div&gt;
</pre>
<pre>
var div1 = document.getElementById('div1')
div1.addEventListener('click', function (e) {
  var target = e.target
  if (target.nodeName === 'A'){
    alert(target.innerHTML)
  }
})
</pre>
#### 完善通用绑定事件的函数 ####
<pre>
function bindEvent(elem, type, selector, fn) {
  if (fn == null){
    fn = selector
    selector = null
  }
  elem.addEventListener(type, function(e){
    var target
    if (selector) {
      target = e.target
      if (target.matches(selector)){
        fn.call(target, e)
      }
    } else {
      fn(e)
    }
  })
}
</pre>
<pre>
// 使用代理
var div1 = document.getElementById('div1')
bindEvent(div1, 'click', a, function (e) {
  console.log(this.innerHTML)
})
// 不使用代理
var a = document.getElementById('a1')
bindEvent(div1, 'click', function (e) {
  console.log(a.innerHTML)
})
</pre>

### 6-2 事件-代码演示 ###
#### 略(同上) ####

### 6-3 事件-解答 ###
#### 解答 ####
- 编写一个通用的事件监听函数
<pre>
  function bindEvent(elem, type, selector, fn) {
    if (fn == null){
      fn = selector
      selector = null
    }
    elem.addEventListener(type, function(e){
      var target
      if (selector){
        target = e.target
        if (target.matches(selector)){
          fn.call(target, e)
        }
      } else {
        fn(e)
      }
    })
  }
</pre>
- 描述事件冒泡流程
	- DOM树形结构
	- 事件冒泡
	- 阻止冒泡
	- 冒泡应用
- 对于一个无限下拉加载图片的页面，如何给每个图片绑定事件
	- 使用代理
	- 知道代理的两个优点
#### 重点总结 ####
- 通用事件绑定
- 事件冒泡
- 代理

### 6-4 Ajax-XMLHttpRequest ###
- 题目
- 知识点
- 解答
#### 题目 ####
- 手动编写一个 ajax，不依赖第三方库
- 跨域的几种实现方式
#### 知识点 ####
- XMLHttpRequest
- 状态码说明
- 跨域
#### XMLHttpRequest ####
<pre>
var xhr = new XMLHttpRequest()
xhr.open("GET", "/api", false)
xhr.onreadystatechange = function(){
    // 这里的函数异步执行,可参与之前 JS 基础中的异步模块
    if (xhr.readyState == 4){
      if(xhr.status == 200) {
        alert(xhr.responseText)
      }
    }
}
xhr.send(null)
</pre>
#### IE兼容性问题 ####
- IE低版本使用 ActiveXObject ，和W3C标准不一样
- IE低版本使用量已非常少，很多网站都早已不支持
- 建议对IE低版本的兼容性：了解即可，无需深究
- 如果遇到对IE低版本要求苛刻的面试，果断放弃
#### 状态码说明 ####
<pre>
xhr.onreadystatechange = function(){
  if (xhr.readyState == 4){
    if (xhr.status == 200) {
       alert(xhr.responseText)
    }
  }
}
</pre>
#### readyState ####
- 0 - (未初始化)还没有调用send()方法
- 1 - (载入)已调用send()方法，正在发送请求
- 2 - (载入完成)send()方法执行完成，已经接收到全部响应内容
- 3 - (交互)正在解析响应内容
- 4 - (完成)响应内容解析完成，可以在客户端调用了
#### status ####
- 2xx - 表示成功处理请求。如 200
- 3xx - 需要重定向，浏览器直接跳转
- 4xx - 客户端请求错误，如 404
- 5xx - 服务端错误
#### 关于代码演示 ####
- 以上是ajax的实现原理，后续会使用jquery演示代码

### 6-5 Ajax-跨域和问题解答 ###
- 什么是跨域
- JSONP
- 服务器端设置 http header
#### 什么是跨域 ####
- 浏览器有同源策略，不允许 ajax 访问其他域接口
- http://www.yourname.com/page1.html
- http://m.imooc.com/course/ajaxcourserecom?cid=459
- 跨域条件：协议、域名、端口，有一个不同就算跨域<br/>
<b style="color:red">http://www.yourname.com:80/page1.html</b><br/>
<b style="color:red">http://m.imooc.com:80/course/ajaxcourserecom?cid=459</b>
#### 可以跨域的三个标签 ####
- 但是有三个标签允许跨域加载资源
- &lt;img src=xxx&gt;	防盗链(百度,知乎)
- &lt;link href=xxxx&gt;
- &lt;script src=xxx&gt;
#### 三个标签的场景 ####
- &lt;img&gt;用于打点统计，统计网站可能是其他域
- &lt;link&gt; &lt;script&gt;可以使用CDN，CDN的也是其他域，BootCDN
- &lt;script&gt; 可以用于JSONP，马上讲解
#### 跨域注意事项 ####
- 所有的跨域请求都必须经过信息提供方允许
- 如果未经允许即可获取，那是浏览器同源策略出现漏洞
#### JSONP实现原理 ####
- 加载 http://coding.m.imooc.com/classindex.html
- 不一定服务器端真正有一个 classindex.html 文件
- 服务器可以根据请求，动态生成一个文件，返回
- 同理于&lt;script src="http://coding.m.imooc.com/api.js"&gt;
- 例如你的网站要跨域访问慕课网的一个接口
- 慕课给你一个地址 http://coding.m.imooc.com/api.js
- 返回内容格式如 callback({x:100, y:200})(可动态生成)
<pre>
&lt;script&gt;
window.callback = function(data) {
	// 这是我们跨域得到信息
	console.log(data)
}
&lt;/script&gt;
&lt;script src="http://coding.m.imooc.com/api.js"&gt;&lt;/script&gt;
以上将返回 callback({x:100, y:200}),然后我们正好定义过 window.callback 函数,相当于执行了
因为script可以绕过跨越的限制
</pre>
#### 服务器端设置 http header ####
- 另外一个解决跨域的简洁方法,需要服务器端来做
- 但是作为交互方,我们必须知道这个方法
- 是将来解决跨域问题的一个趋势
<pre>
//注意 不同后端语言的写法可能不一样

// 第二个参数填写允许跨域的域名称,不建议直接写 "*"
response.setHeader("Access-Control-Allow-Origin","http://a.com,http://b.com");
response.setHeader("Access-Control-Allow-Headers","X-Requested-With");
response.setHeader("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");

// 接收跨域的cookie
response.setHeader("Access-Control-Allow-Credentials","true");
</pre>
#### 关于代码演示 ####
- 以上是JSONP的实现原理,后续会使用jquery演示代码
- 后端设置 http header 不演示代码，了解即可
#### 解答 ####
- 手动编写一个 ajax,不依赖第三方库
<pre>
var xhr = new XMLHttpRequest()
xhr.open("GET","/api",false)
xhr.onreadystatechange = function(){
  // 这里的函数异步执行,可参考之前 JS 基础中的异步模块
  if (xhr.readyState == 4) {
    if (xhr.status == 200) {
	  alert(xh.responseText)
    }
  }
}
xhr.send(null)
</pre>
- 跨域的几种实现方式
	- JSONP
	- 服务器端设置 http header
#### 重点总结 ####
- XMLHttpRequest
- 状态码说明
- 跨域

### 6-6 存储 ###
#### 题目 ####
- 请描述一下 cookie，sessionStorage 和 localStorage 的区别?
#### 知识点 ####
- cookie
- localStorage和sessionStorage
#### cookie ####
- 本身用于客户端和服务器端通信
- 但是它有本地存储的功能,于是就被“借用”
- 使用document.cookie = ....获取和修改即可
#### cookie用于存储的缺点 ####
- 存储量太小,只有4KB
- 所有http请求都带着,会影响获取资源的效率
- API简单,需要封装才能用 document.cookie= ....
#### locationStorage 和 sessionStorage ####
- HTML5 专门为存储而设计，最大容量 5M
- API简单易用:
	- localStorage.setItem(key, value); locationStorage.getItem(key);
- IOS safari 隐藏模式下
	- localStorage.getItem 会报错
	- 建议统一使用 try-catch 封装
#### 解答 ####
- 请描述一下 cookie，sessionStorage 和 localStorage 的区别?
	- 容量
	- 是否会携带到 ajax 中
	- API易用性
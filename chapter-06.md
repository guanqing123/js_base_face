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
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
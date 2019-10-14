## 第5章 JS-Web-API（上） ##
### 5-1 从基础只是到JSWebAPI ###
#### 从基础只是到JS-Web-API ####
- 回顾JS基础知识
- JS-Web-API
- 总结
#### 回顾JS基础知识 ####
- 变量类型和计算
- 原型和原型链
- 闭包和作用域
- 异步和单线程
- 其他（如日期、Math、各种常用API）
- 特点：表面看起来并不能用于工作中开发代码
- 内置函数：Object Array Boolean String ...
- 内置对象：Math JSON ...
- 我们连在网页弹出一句hello world都不能实现
#### JS-Web-API ####
- JS基础知识：ECMA262标准
- JS-Web-API：W3C标准
#### W3C标准中关于JS的规定有 ####
- DOM操作
- BOM操作
- 事件绑定
- ajax请求（包括http协议）
- 存储
#### 页面弹框是window.alert(123),浏览器需要做 ####
- 定义一个window全局变量，对象类型
- 给他定义一个alert属性，属性值是一个函数
#### 获取元素document.getElementById(id),浏览器需要 ####
- 定义一个document全局变量，对象类型
- 给它定义一个getElementById的属性，属性值是一个函数
#### 但是W3C标准没有规定任何JS基础相关的东西 ####
- 不管什么变量类型、原型、作用域和异步
- 只管定义用于浏览器中JS操作页面的API和全局变量
#### 全面考虑，JS内置的全局函数和对象有哪些？ ####
- 之前讲过的Object Array Boolean String Math JSON 等
- 刚刚提的window document
- 接下来还有继续讲到的所有未定义的全局变量，如navigator.userAgent
#### 总结 ####
#### 常说的JS（浏览器执行的JS）包含两部分 ####
- JS基础知识（ECMA262标准）
- JS-Web-API（W3C标准）

### 5-2 DOM本质 ###
#### DOM操作（Document Object Model） ####
- 题目
- 知识点
- 解答
#### 题目 ####
- DOM是哪种基本的数据结构？
- DOM操作的常用API有哪些？
- DOM节点的attr和property有何区别？
#### 知识点 ####
- DOM本质
- DOM节点操作
- DOM结构操作
#### DOM的本质 ####
<pre>
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;note&gt;
    &lt;to&gt;Tove&lt;/to&gt;
    &lt;from&gt;Jani&lt;/from&gt;
    &lt;heading&gt;Reminder&lt;/heading&gt;
    &lt;body&gt;Don't forget me this weekend!&lt;/body&gt;
    &lt;other&gt;
        &lt;a&gt;&lt;/a&gt;
        &lt;b&gt;&lt;/b&gt;
    &lt;/other&gt;
&lt;/note&gt;
</pre>
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div&gt;
    &lt;p&gt;this is p&lt;/p&gt;
  &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
<p style="color:red;font-weight:bold">
	DOM本质：浏览器拿到html代码后，DOM把html代码结构化成浏览器可识别以及js可识别的东西。
</p>
html代码就是一个字符串，但是浏览器已经把字符串结构化成树形结构了。

### 5-3 DOM节点操作 ###
#### DOM可以理解为： ####
- 浏览器把拿到的html代码，结构化成一个浏览器能识别并且js可操作的一个模型而已。
#### DOM节点操作 ####
- 获取DOM节点
- Property
- Attribute
#### 获取DOM节点 ####
<pre>
var div1 = document.getElementById('div1') // 元素
var divList = document.getElementsByTagName('div') // 集合
console.log(divList.length)
console.log(divList[0])

var containerList = document.getElementsByClassName('.container') // 集合
var pList = document.querySelectorAll('p') // 集合
</pre>
#### Property ####
<pre>
var pList = document.querySelectorAll('p')
var p = pList[0]
console.log(p.style.width) // 获取样式
p.style.width = '100px' // 修改样式
console.log(p.className) // 获取class
p.className = 'p1' // 修改class

// 获取nodeName 和 nodeType
console.log(p.nodeName)
console.log(p.nodeType)
</pre>
#### Attribute ####
<pre>
var pList = document.querySelectorAll('p')
var p = pList[0]
p.getAttribute('data-name')
p.setAttribute('data-name', 'imooc')
p.getAttribute('style')
p.setAttribute('style', 'font-size: 30px;')
</pre>

### 5-4 BOM节点操作-代码演示 ###
同上

### 5-5 DOM结构操作 ###
- 新增节点
- 获取父元素
- 获取子元素
- 删除节点
#### 新增节点 ####
<pre>
var div1 = document.getElementById('div1')
// 添加新节点
var p1 = document.createElement('p')
p1.innerHTML = 'this is p1'
div1.appendChild(p1) // 添加新创建的元素
// 移动已有节点
var p2 = document.getElementById('p2')
div1.appendChild(p2)
</pre>
#### 获取父元素和子元素 ####
<pre>
var div1 = document.getElementById('div1')
var parent = div1.parentElement

var child = div1.childNodes
div1.removeChild(child[0])
</pre>
#### 删除节点 ####
<pre>
var div1 = document.getElementById('div1')
var child = div1.childNodes
div1.removeChild(child[0])
</pre>

### 5-6BOM结构操作-代码演示 ###
同上

### 5-7BOM结构解答   ###
#### 解答 ####
- DOM 是哪种基本的数据结构?
	- 数
- DOM 操作的常用API有哪些?
	- 获取DOM节点,以及节点的property和Attribute
	- 获取父节点,获取子节点
	- 新增节点,删除节点
- DOM 节点的 Attribute 和 property 有何区别?
	- property 只是一个 JS 对象的属性的修改
	- Attribute 是对 html 标签属性的修改
	- https://segmentfault.com/a/1190000008781121
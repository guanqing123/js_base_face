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

### 5-6 BOM结构操作-代码演示 ###
同上

### 5-7 BOM结构解答   ###
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
#### Attribute（特性） ####
1. attribute特性由HTML定义，所有出现在HTML标签内的描述节点都是attribute特性。
	<pre>
	&lt;div id="test" class="button" custom-attr="1"&gt;&lt;/div&gt;
	</pre>
	<pre>
	document.getElementById('test').attributes;
	return: [custom-attr="hello", class="button",   id="test"]
	</pre>
2. attribute特性的类型总是字符串类型。
	<pre>
	document.getElementById('test').getAttribute('custom-attr') 或者
	$('#test').attr('custom-attr') 总是返回字符串类型的"1"。
	</pre>
#### Property（属性） ####
1. property属性属于DOM对象，DOM实质就是javascript中的对象。我们可以跟在js中操作普通对象一样获取、设置DOM对象的属性，并且property属性可以是任意类型。
	<pre>
    document.getElementById('test').foo = 1; // 设置属性: foo 为 number类型: 1
    document.getElementById('test').foo; // 获取属性值, return number: 1
    $('#test').prop('foo'); // 使用jquery获取属性值, return number: 1
	</pre>
	<pre>
	  $('#test').prop('foo', {
        age: 23,
        name: 'John'
      }); // 使用jquery设置一个名为foo的对象
      document.getElementById('test').foo.age; // return number类型: 23
      document.getElementById('test').foo.name; // return string类型: "John"
	</pre>
----------
<b>注1</b>：这里的property可以是任意类型指的是我们为DOM对象自定义添加的属性，对于DOM对象的原始属性，类似<b style="color:red;">name</b>属性，无论我们设置什么类型的值，最后返回的都是字符类型。<br/>

另外，我们获取HTML5定义的data属性时，获取的值也是字符串。<span style="color:red">```<div data-id="33"></div>```,ele.dataset.id // string 33</span><br/>

1. 非自定义的attribute特性与property有1:1的映射关系,比如: id,class,title等<br/>
```<div id="test" class="button" foo="1"></div>```
<pre>
document.getElementById('test').id; // return string: "test"
document.getElementById('test').className; // return string: "button"
document.getElementById('test').foo; // return undefined 因为foo是一个自定义的attr特性
</pre>
注意：当我们通过property属性进行设置或获取class时，我们需要使用<b>className</b>，因为在js中<b style="color:red">class</b>是关键字。

<b>注2</b>：第二点的意思是说当我们在html中写非自定义的attribute特性时，DOM对象会自动映射对应的property。

1. 非自定义的property（attribute）改变的时候，其对应的attribute（property）在多数情况下也会改变。
```<div id="test" class="button"></div>```
<pre>
var div = document.getElementById('test');
div.className = 'red-input';
div.getAttribute('class'); // return string: "red-input"
div.setAttribute('class','green-input');
div.className; // return string: "green-input"
</pre>
2.当对应的property改变的时候，attribute特性value的值一直未默认值，并不会随之改变。<br/>
```<input id="search" value="foo" />```
<pre>
var input = document.getElementById('search');
input.value = 'foo2';
input.getAttribute('value'); // return string: "foo"
</pre>
这条特性意味着我们平时在写业务的时候多数情况下使用property是正确的。当用户input输入更改的时候，attribute-value值不会变化，即使js更改value，也不会使attribute变化。这也验证了第三点的。

<b>最佳实践</b><br/>
在javascript中我们推荐使用<b>property</b>属性因为这个属性相对<b>attribute</b>更快，更简便。尤其是有些类型本该是布尔类型的attribute特性。比如："checked", "disabled", "selected"。浏览器会自动将这些值转变成布尔值传给property属性。<br/>
```<input id="test" class="blue" type="radio" />```

好实践：
<pre>
// get id
document.getElementById('test').id;
// set class
document.getElementById('test').className = 'red';
// get and set radio control status
document.getElementById('test').checked; // boolean 
document.getElementById('test').checked = true;
$('#test').prop('checked'); // boolean
$('#test').prop('checked', true);
</pre>

坏实践：
<pre>
// get id
document.getElementById('test').getAttribute('id');
// set class
document.getElementById('test').setAttribute('class', 'red');
document.getElementById('test').getAttribute('checked'); //  返回字符串类型 'checked'
</pre>

### 5-8 BOM操作-知识点  ###
Browser	Object Model
- 题目
- 知识点
- 解答
#### 题目 ####
- 如何检测浏览器的类型
- 拆解url的各部分
#### 知识点 ####
- navigator
- screen
- location
- history
#### navigator & screen ####
<pre>
// navigator
var ua = navigator.userAgent
var isChrome = ua.indexOf('Chrome')
console.log(isChrome)

// screen
console.log(screen.width)
console.log(screen.height)
</pre>
#### location & history ####
<pre>
// location
console.log(location.href)
console.log(location.protocol) // 'http:' 'https:'
console.log(location.pathname) // '/learn/199'
console.log(location.search)
console.log(location.hash)

// history
history.back()
history.forward()
</pre>


### 5-9 BOM操作-代码演示  ###
同上
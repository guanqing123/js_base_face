## 第3章 JS基础知识（中） ##
### 3-1 作用域和闭包-执行上下文 ###
#### 作用域和闭包 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 说一下对变量提升的理解
- 说明this几种不同的使用场景
- 创建10个`<a>`标签，点击的时候弹出来对应的序号
- 如何理解作用域
- 实际开发中闭包的应用
#### 知识点 ####
- 执行上下文
- this
- 作用域
- 作用域链
- 闭包
#### 执行上下文 ####
<pre>
console.log(a) // undefined
var a = 100	// 变量提升,会把 var a;提到执行上下文前面,var a = undefined;进行声明

fn('lilei') // "lilei" 20
function fn(name) {
    age = 20
    console.log(name, age)
    var age
}
</pre>
- 范围：一段`<script>`或者一个函数
- 全局：变量定义、函数声明
- 函数：变量定义、函数声明、this、arguments
#### PS：注意“函数声明”和“函数表达式”的区别 ####
<pre>
fn() // 不会报错,函数执行之前,会把函数提到执行上下文前面,进行声明
function fn(){
  // 函数声明
}

fn1() // 会报错,var fn1;会把fn1提到执行上下文前面,var fn1 = undefined,fn1还不是一个函数
var fn1 = function(){
  // 函数表达式
}
</pre>

### 3-2 作用域和闭包-执行上下文-代码演示 ###
<pre>
fn("zhangsan")
function fn(name){

  console.log(this)  
  console.log(arguments) 

  age = 20
  console.log(name, age)
  var age

  bar(100)
	
  function bar(num){
    console.log(num)
  }
}
// Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …}
// Arguments ["zhangsan", callee: ƒ, Symbol(Symbol.iterator): ƒ]
// zhangsan 20
// 100
</pre>

### 3-3 作用域和闭包-this ###
#### this ####
- this要在执行时才能确认值，定义时无法确认
<pre>
var a = {
    name: 'A',
    fn: function() {
        console.log(this.name)
    }
}
a.fn() // this === a
a.fn.call({ name: 'B' }) // this为{ name: 'B' }
var fn1 = a.fn
fn1() // this === window
</pre>
#### this ####
- 作为构造函数执行
- 作为对象属性执行
- 作为普通函数执行
- call apply bind

### 3-4 作用域和闭包-this-代码演示 ###
<pre>
// 构造函数
function Foo(name) {
    this.name = name
}
let f = new Foo('lilei')
f.name // "lilei"
</pre>
<pre>
// 作为一个对象的属性
let obj = {
    name: 'A',
    printName: function() {
        console.log(this.name)
    }
}
obj.printName() // "A"
</pre>
<pre>
// 普通函数
function fn() {
    console.log(this)
}
fn() // window
</pre>
<pre>
// call apply bind
function fn1(name, age) {
    console.log(name)
    console.log(this)
}
fn1.call({ x: 1 }, 'lilei', 20) // "lilei" {x: 1}
fn1.apply({ x: 200 }, ['lilei', 20]) // "lilei" {x: 200}

let fn2 = function(name, age) {
    console.log(name)
    console.log(this)
}.bind({x: 300})
fn2('lilei', 20) // "lilei" {x: 300}
</pre>

### 3-5 作用域和闭包-作用域 ###
#### 作用域 ####
- 没有块级作用域
- 只有函数和全局作用域
<pre>
// 无块级作用域
if (true) {
    var name = 'lilei'
}
console.log(name) // "lilei"

// 函数和全局作用域
var a = 100
function fn() {
    var a = 200
    console.log('fn', a)
}
console.log('global', a) // "global 100"
fn() // "fn 200"
</pre>
### 作用域链 ###
<pre>
var a = 100
function fn() {
    var b = 200
    // 当前作用域没有定义的变量，即“自由变量”
    console.log(a)	// 100
    console.log(b)	// 200
}
fn()
</pre>
<pre>
var a = 100
function F1() {
    var b = 200
    function F2() {
        var c = 300
        console.log(a) // a 是自由变量	100
        console.log(b) // b 是自由变量	200
        console.log(c)	// 300
    }
    F2()
}
F1()
</pre>

### 3-6 作用域和闭包-作用域-代码演示 ###
<pre>
// 推介这么写
var name
if (true){
  name = 'zhangsan'
}
console.log(name)
</pre>

### 3-7 补充-ES6块级作用域 ###
<pre>
// js 没有块级作用域
// ES6 有块级作用域
</pre>

### 3-8 作用域和闭包-闭包 ###
#### 闭包 ####
<pre>
function F1() {
    var a = 100
    
    // 返回一个函数（函数作为返回值）
    return function() {
        console.log(a)
    }
}
// f1 得到一个函数
var f1 = F1()
var a = 200
f1() // 100
</pre>
<pre>
var b = 100
function F2(){
  return function(){
    console.log(b)
  }
}
var f2 = F2()
var b = 500
f2()  // 500
</pre>
<pre>
var c = 100
function F3(){
  var c = 200
  return function(){
    console.log(c)
  }
}
var f3 = F3()
var c = 300
f3()  // 200
</pre>
#### 闭包的使用场景 ####
- 函数作为返回值（上一个demo）
- 函数作为参数传递（自己思考）

### 3-9 作用域和闭包-闭包-代码演示 ###
<pre>
// 闭包 1，函数作为返回值
function F1() {
    var a = 100
    return function() {
        console.log(a) // a 自由变量，向父作用域去寻找 ——函数**定义**时的父作用域
    }
}
var f1 = F1()
var a = 200
f1() // 100
</pre>
<pre>
// 闭包 2，函数作为参数传递
function F1() {
    var a = 100
    return function() {
        console.log(a)  // a 自由变量，向父作用域去寻找 ——函数**定义**时的父作用域
    }
}
var f1 = F1()
function F2(fn) {
    var a = 300
    fn()
}
F2(f1) // 100
</pre>
<pre>
var a = 100
function F1() {
    return function() {
        console.log(a)  // a 自由变量，向父作用域去寻找 ——函数**定义**时的父作用域
    }
}
var f1 = F1()
function F2(fn) {
    var a = 300
    fn()
}
F2(f1) // 100
</pre>
<pre>
var a = 100
function F1() {
    return function() {
        console.log(a)  // a 自由变量，向父作用域去寻找 ——函数**定义**时的父作用域
    }
}
var f1 = F1()
function F2(fn) {
    var a = 300
    fn()
}
a = 800
F2(f1)	// 800
</pre>

### 3-10 作用域和闭包-解题 ###
#### 解题 ####
- 说一下对变量提升的理解
- 说明this几种不同的使用场景
- 创建10个`<a>`标签，点击的时候弹出来对应的序号
- 如何理解作用域
- 实际开发中闭包的应用
#### 说一下对变量提升的理解 ####
- 变量定义
- 函数声明（注意和函数表达式的区别）
#### 说明this几种不同的使用场景 ####
- 作为构造函数执行
- 作为对象属性执行
- 作为普通函数执行
- call apply bind
#### 创建10个`<a>`标签 点击的时候弹出来对应的序号 ####
<pre>
// 这是一个错误的写法！！！
var i, a
for (i = 0; i < 10; i++) {
    a = document.createElement('a')
    a.innerHTML = i + '&#60;br&#62;'
    a.addEventListener('click', function(e) {
        e.preventDefault()
        alert(i) // 自由变量,要去父作用域获取值;等到点击的时候,i已经变成10了,所有都是10
    })
    document.body.appendChild(a)
}
</pre>
<pre>
// 这是正确的写法！！！
var i
for (i = 0; i < 100; i++) {
    (function(i) {
        // 函数作用域
        var a = document.createElement('a')
        a.innerHTML = i + '&#60;br&#62;'
        a.addEventListener('click', function(e) {
            e.preventDefault()
            alert(i)  // 自由变量,要去父作用域获取值;此时去函数作用域获取;		
        })
        document.body.appendChild(a)
    })(i)
}
</pre>
#### 如何理解作用域 ####
- 自由变量
- 作用域链，即自由变量的查找
- 闭包的两个场景
#### 实际开发中闭包的应用 ####
<pre>
// 闭包实际应用中主要用于封装变量，收敛权限
function isFirstLoad() {
    var _list = []
    return function(id) {
        if (_list.indexOf(id) >= 0) {
            return false
        } else {
            _list.push(id)
            return true
        }
    }
}

// 使用
var firstLoad = isFirstLoad()
firstLoad(10) // true
firstLoad(10) // false
firstLoad(20) // true
// 你在isFirstLoad函数外，根本不可能修改掉_list的值
</pre>

#### 3-11 作用域和闭包-解题-代码演示 ####
同上 3-10
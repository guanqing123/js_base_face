## 第2章 JS基础知识（上） ##
### 2-1 变量类型和计算-1 ###
#### 变量类型和计算 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- JS中使用typeof能得到的哪些类型
- 何时使用===何时使用==
- JS中有哪些内置函数
- JS变量按照存储方式区分为哪些类型，并描述其特点
- 如何理解JSON
#### 知识点 ####
- 变量类型
- 变量计算
#### 变量类型 ####
- 值类型 vs 引用类型
- typeof运算符
#### 值类型 ####
<pre>
let a = 100
let b = a
a = 200
console.log(b) // 100
</pre>
#### 引用类型 ####
- 对象、数组、函数
<pre>
let a = { age: 20 }
let b = a
b.age = 21
console.log(a.age) // 21
</pre>
#### typeof运算符 ####
<pre>
typeof undefined // "undefined"
typeof 'abc' // "string"
typeof 123 // "number"
typeof true // "boolean"
typeof {} // "object"
typeof [] // "object"
typeof null // "object"
typeof console.log // "function"
</pre>
#### 变量计算 - 强制类型转换 ####
- 字符串拼接
- ==运算符
- if 语句
- 逻辑运算
#### 字符串拼接 ####
<pre>
let a = 100 + 10 // 110
let b = 100 + '10' // "10010"
</pre>
#### == 运算符 ####
<pre>
100 == '100' // true
0 == '' // true
null == undefined // true
</pre>
#### if 语句 ####
<pre>
let a = true
if (a) {
    // ...
}
let b = 100
if (b) {
    // ...
}
let c = ''
if (c) {
    // ...
}
</pre>
#### 逻辑运算符 ####
<pre>
console.log(10 && 0) // 0
console.log('' || 'abc') // "abc"
console.log(!window.abc) // true

// 判断一个变量会被当做true还是false
let a = 100
console.log(!!a) // true
</pre>

### 2-2 变量类型和计算-2 ###
#### 解答 ####
#### JS中使用 typeof 能得到的类型 ####
- 问题：JS中使用typeof能得到的哪些类型
- 答案：undefined、string、number、boolean、object、function、symbol
<pre>
let sym = Symbol('commet')
console.log(typeof sym) // "symbol"
</pre>
#### 何时使用 === 何时使用 == ####
- 问题：何时使用 === 何时使用 ==
- 答案：判断对象的某个属性是否存在或为null时可以使用==;因为jquery源码这么使用;其他情况全部用===
<pre>
if (obj.a == null) {
    // 这里相当于obj.a === null || obj.a === undefined，简写形式
    // 这是jquery源码中推荐的写法
}
</pre>
#### JS中的内置函数 ####
- 问题：JS中有哪些内置函数 —— 数据封装类对象
- 答案：
<pre>
String
Number
Boolean
Object
Array
Function
Date
RegExp
Error
</pre>
#### JS按存储方式区分变量类型 ####
- 问题：JS变量按照存储方式区分为哪些类型，并描述其特点
- 答案：值类型 和 引用类型

### 2-3 变量类型和计算-3 如何理解JSON ###
#### 如何理解JSON ####
- 问题：如何理解JSON
- 答案：JSON只不过是一个JS对象而已，也是一种数据格式
<pre>
JSON.stringify({ a: 10, b: 20 })
JSON.parse('{"a":10,"b":20}')
</pre>

### 2-4 变量类型和计算-3 代码演示 ###
`if (...) {}中false的情况：false 0 NaN null undefined`<br/>
内置对象有：JSON、Math

### 2-5 typeof symbol 【ES6变量类型】 ###
<pre>
let s = Symbol()
typeof s // "symbol"
let s1 = Symbol()
s === s1 // false
let s2 = Symbol('s2s2')
console.log(s2) // Symbol(s2s2)
let s3 = s2
console.log(s3 === s2) // true
let sym1 = Symbol('111')
let sym2 = Symbol('222')
let obj = { [sym1]: 'hello world' }
obj[sym2] = 123
console.log(obj) // { Symbol(111): "hello world", Symbol(222): 123 }
console.log(obj[sym1]) // "hello world"
console.log(obj[sym2]) // 123
</pre>

### 2-6 原型和原型链 ###
#### 原型和原型链 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 如何准确判断一个变量是数组类型
- 写一个原型链继承的例子
- 描述new一个对象的过程
- zepto（或其他框架）源码中如何使用原型链
#### 知识点 ####
- 构造函数
- 构造函数 扩展
- 原型规则和示例
- 原型链
- instanceof
#### 构造函数 ####
<pre>
function Foo(name, age) {
    this.name = name
    this.age = age
    this.class = 'class-1'
    // return this // 默认有这一行
}
let f = new Foo('lilei', 18)
// let f2 = new Foo('hanmeimei', 17) // 创建多个对象
</pre>
#### 构造函数-扩展 ####
- let a = {} 其实是let a = new Object()的语法糖
- let a = [] 其实是let a = new Array()的语法糖
- function Foo(){...} 其实是let Foo = new Function(...)
- 使用instanceof判断一个函数是否是一个变量的构造函数
## 第4章JS基础知识（下） ##
### 4-1 异步和单线程-什么是异步 ###
#### 异步和单线程 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 同步和异步的区别是什么？分别举一个同步和异步的例子
- 一个关于setTimeout的笔试题
- 前端使用异步的场景有哪些
#### 知识点 ####
- 什么是异步（对比同步）
- 前端使用异步的场景
- 异步和单线程
#### 什么是异步 ####
<pre>
console.log(100)
setTimeout(function() {
    console.log(200)
}, 1000)
console.log(300)
</pre>
#### 同步阻塞后续程序代码执行，异步不会阻塞程序的的运行。 ####
#### 对比同步 ####
<pre>
console.log(100)
alert(200) // 1秒钟之后手动点击确认
console.log(300)
</pre>
#### 何时需要异步 ####
- 在可能发生等待的情况
- 等待过程中不能像alert一样阻塞程序运行
- 因此，所有的"等待的情况"都需要异步
#### ajax请求代码示例 ####
<pre>
console.log('start')
$.get('./data1.json', function(data1) {
    console.log(data1)
})
console.log('end')
</pre>
#### `<img>`加载示例 ####
<pre>
console.log('start')
var img = document.createElement('img')
img.onload = function() {
    console.log('loaded')
}
img.src = '/xxx.png'
console.log('end')
</pre>
#### 事件绑定示例 ####
<pre>
console.log('start')
document.getElementById('btn1').addEventListener('click', function() {
    alert('clicked')
})
console.log('end')
</pre>

### 4-2 异步和单线程-什么是异步-代码演示 ###
<pre>
console.log(100)
var img = document.createElement('img')
img.onload = function(){
	console.log('image has ready load')
}
img.src = "https://pics5.baidu.com/feed/caef76094b36acaf22cadf64278d1e1500e99cdd.jpeg"
console.log(200)
// 100
// 200
// image has ready load
</pre>

### 4-3 异步和单线程-单线程 ###
#### 异步和单线程 ####
<pre>
console.log(100)
setTimeout(function() {
    console.log(200)
})
console.log(300)
</pre>
- 执行第一行，打印100
- 执行setTimeout后，传入setTimeout的函数会被暂存起来，不会立即执行（单线程的特点，不能同时干两件事）
- 执行最后一行，打印300
- 待所有程序执行完，处于空闲状态时，会立马看有没有暂存起来的要执行
- 发现暂存起来的setTimeout中的函数无需等待时间，就立即过来执行
<pre>
console.log('start')
$.get('./data1.json', function(data1) {
    console.log(data1)
})
console.log('end')
</pre>
<pre>
console.log('start')
document.getElementById('btn1').addEventListener('click', function() {
    alert('clicked')
})
console.log('end')
</pre>
- js是单线程语言，即一次只能干一件事，如果同时有两件事，另一件就先上一边排队去，我先干完这件再说，如果没有异步，那就会出现阻塞现象
- 由于js是单线程，在代码执行的时候又不能因为执行需要等待的代码而造成阻塞，因此js会首先将无需等待的（同步）代码执行完成后，来处理异步代码，如果达到异步代码的执行条件的话，就会执行

### 4-4 异步和单线程-解答 ###
- 同步和异步的区别是什么？分别举一个同步和异步的例子
- 一个关于setTimeout的笔试题
- 前端使用异步的场景有哪些
#### 同步和异步的区别是什么 ####
- 同步会阻塞代码执行，而异步不会
- alert是同步，setTimeout是异步
#### 一个关于setTimeout的笔试题 ####
<pre>
console.log(1)
setTimeout(function() {
    console.log(2)
}, 0)
console.log(3)
setTimeout(function() {
    console.log(4)
}, 1000)
console.log(5)
// 1
// 3
// 5
// 2
// 4
</pre>
#### 前端使用异步的场景有哪些 ####
- 定时任务：setTimeout、setInterval
- 网络请求：ajax请求、动态加载
- 事件绑定
#### 重点总结 ####
- 异步和同步的区别
- 异步和单线程的关系
- 异步在前端的引用场景

### 4-5 其他知识点-日期和Math ###
#### 其他知识 ####
- 题目
- 知识点
- 解答
#### 题目 ####
- 获取2017-06-10格式的日期
- 获取随机数，要求是长度一致的字符串格式
- 写一个能遍历对象和数组的通用forEach函数
#### 知识点 ####
- 日期
- Math
- 数组API
- 对象API
#### 日期 ####
<pre>
Date.now() // 获取当前时间毫秒数
var dt = new Date()
dt.getTime() // 获取毫秒数
dt.getFullYear() // 年
dt.getMonth() // 月（0-11）
dt.getDate() // 日（0-31）
dt.getHours() // 小时（0-23）
dt.getMinutes() // 分钟（0-59）
dt.getSeconds() // 秒（0-59）
</pre>
#### Math ####
- 获取随机数Math.random()

### 4-6 其他知识点-数组和对象的API ###
#### 数组API ####
- forEach 遍历所有元素
- every 判断所有元素是否都符合条件
- some 判断是否有至少一个元素符合条件
- sort 排序
- map 对元素重新组装，生成新数组
- filter 过滤符合条件的元素
#### forEach ####
<pre>
var arr = [1, 2, 3]
arr.forEach(function(item, index) {
    // 遍历数组的所有元素
    console.log(index, item)
}）
</pre>
#### every ####
<pre>
var arr = [1, 2, 3]
var result = arr.every(function(item, index) {
    // 用来判断所有的数组元素，都满足条件
    if (item < 4) {
        return true
    }
})
console.log(result)
// true
</pre>
<pre>
var arr = [1, 2, 3, 4]
var result = arr.every(function(item, index) {
    // 用来判断所有的数组元素，都满足条件
    if (item < 4) {
        return true
    }
})
console.log(result)
// false
</pre>
#### some ####
<pre>
var arr = [1, 2, 3]
var result = arr.some(function(item, index) {
    // 用来判断只要有一个数组元素，满足条件
    if (item < 2) {
        return true
    }
})
console.log(result)
// true
</pre>
#### sort ####
<pre>
var arr = [1, 4, 2, 3, 5]
var arr2 = arr.sort(function(a, b) {
    // 从小到大排序
    return a - b
    
    // 从大到小排序
    return b - a
})
console.log(arr2)
</pre>
#### map ####
<pre>
var arr = [1, 2, 3, 4]
var arr2 = arr.map(function(item, index) {
    // 将元素重新组装，并返回
    return '<b>' + item + '</b>'
})
console.log(arr2)
</pre>
#### filter ####
<pre>
var arr = [1, 2, 3]
var arr2 = arr.filter(function(item, index) {
    // 通过某一个条件过滤数组
    if (item >= 2) {
        return true
    }
})
console.log(arr2)
</pre>
#### 对象API ####
<pre>
var obj = {
    x: 100,
    y: 200,
    z: 300
}
var key
for (key in obj) {
    // 注意这里的 hasOwnProperty，在讲原型链的时候讲过了
    if (obj.hasOwnProperty(key)) {
        console.log(key, obj[key])
    }
}
</pre>

### 4-7 其他知识点-知识点代码演示 ###
- 略
### 4-8 其他知识点-解答 ###
#### 解答 ####
- 获取2017-06-10格式的日期
- 获取随机数，要求是长度一致的字符串格式
- 写一个能遍历对象和数组的通用forEach函数
#### 获取2017-06-10格式的日期 ####

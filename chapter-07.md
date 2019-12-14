## 第七章 开发环境 ##
### 7-1 开发环境介绍 ###
#### 关于开发环境 ####
- 面试官想通过开发环境了解面试者的经验
- 开发环境，最能体现工作产出的效率
- 会以聊天的形式为主，而不是出具体的问题
#### 关于开发环境 ####
- IDE (写代码的效率)
- git (代码版本管理，多人协作开发)
- JS 模块化
- 打包工具
- 上线回滚的流程
### 7-2 IDE ###
#### 工具 ####
- webstorm
- sublime
- vscode
- atom
- 插件 插件 插件！！！
#### 如果 ####
- 如果你要走大牛、大咖、逼格的路线，就用webstorm
- 如果你走普通、屌丝、低调路线，就用 sublime
- 如果你走小清新、个性路线,就用 vscode 或者 atom
- 如果你面试，最好有一个用的熟悉，其他都会一点
#### 千万 ####
- 千万不要说你使用 Dreamweaver 或者 notpad++
- 不做 .net 也不要用 Visual Studio
- 不做 java 也不要用 eclipse
### 7-3 Git ###
#### Git ####
- 正式项目都需要代码版本管理
- 大型项目需要多人协作开发
- Git 和 linux 是一个作者
- 网络Git服务器如 coding.net github.com
- 一般公司代码非开源，都有自己的Git服务器
- 搭建Git服务器无需你了解太多
- Git的基本操作必须很熟练
#### 常用Git命令 ####
- git add .
- git checkout -- xxx
- git commit -m "xxx"
- git push origin master
- git pull origin master
- git branch
- git checkout -b xxx / git checkout xxx
- git merge xxx
### 7-4 代码演示 ###
<pre>
mkdir js-git-test
cd js-git-test
git init
echo "# js-git-test" >> README.md
git add README.md
git commit -m "first commit"
git remote add origin https://git.coding.net/wangfupeng/js-git-test.git
git push -u origin master
</pre>
### 7-5 代码演示-多人协作 ###
<pre>
git branch
git checkout -b dev
git diff
git push origin dev

git checkout master
git pull origin master
git merge dev 合并到master分支
git push origin master
</pre>
### 7-6 模块化-AMD ###
#### 模块化 ####
- 这本身就是一个面试的问题
#### 知识点 ####
- 不使用模块化的情况
- 使用模块化
- AMD
- CommonJS
#### 不使用模块化 ####
- util.js getFormatDate函数
- a-util.js aGetFormatDate函数 使用getFormatDate
- a.js aGetFormatDate
#### 代码 ####
<pre>
// util.js
function getFormateDate(date, type) {
  // type === 1 返回 2017-06-15
  // type === 2 返回 2017年6月15日 格式
  // ...
}

// a-util.js
function aGetFormatDate(date) {
  // 要求返回 2017年6月15日 格式
  return getFormateDate(date, 2)
}

// a.js
var dt = new Date();
console.log(aGetFormatDate(dt))
</pre>
#### 使用 ####
<pre>
&lt;script src="util.js"&gt;&lt;/script&gt;
&lt;script src="a-util.js"&gt;&lt;/script&gt;
&lt;script src="a.js"&gt;&lt;/script&gt;

1. 这些代码中的函数必须是全局变量，才能暴露给使用方。全局变量污染
2. a.js 知道要引用 a-util.js，但是他知道还需要依赖于 util.js吗？
</pre>
#### 使用模块化 ####
<pre>
// util.js
export {
  getFormatDate: function(date, type) {
    // type === 1 返回 2017-06-15
    // type === 2 返回 2017年6月15日 格式
  }
}

// a-util.js
var getFormatDate = require('util.js')
export {
  aGetFormatDate: function(date) {
    // 要求返回 2017年6月15日 格式
    return getFormatDate(date, 2)
  }
}

// a.js
var aGetFormatDate = require('a-util.js')
var dt = new Date()
console.log(aGetFormatDate(dt))

// 直接`&lt;script src="a.js"&gt;&lt;/script&gt`,其他的根据依赖关系自动引用
// 那两个函数,没必要做成全局变量,不会带来污染和覆盖
</pre>
#### AMD ####
- require.js [requirejs.org/](requirejs.org/)
	- 全局 define 函数
	- 全局 require 函数
	- 依赖 JS 会自动、异步加载
#### 使用 require.js ####
<pre>
// util.js
define(function(){
  return {
    getFormatDate: function (date, type) {
      if (type === 1) {
        return '2017-06-15'
      }
      if (type === 2) {
        return '2017年6月15日'
      }
    }
  }
})

// a-util.js
define(['./util.js'], function (util) {
  return {
    aGetFormatDate: function (date) {
      return util.getFormatDate(date, 2)
    }
  }
})

// a.js
define(['./a-util.js'], function (aUtil) {
  return {
    printDate: function (date) {
      console.log(aUtil.aGetFormatDate(date))
    }
  }
})

// main.js
require(['./a.js'], function(a) {
  var date = new Date()
  a.printDate(date)
})

&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;title&gt;Document&lt;/title&gt;  
&lt;/head&gt;
&lt;body&gt;
  &lt;p&gt;AMD test&lt;/p&gt;
  
  &lt;script src="/require.min.js" data-main="./main.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
### 7-7 AMD-代码演示 ###
同上
### 7-8 模块化-CommonJS ###
- nodejs 模块化规范，现在被大量用前端，原因：
- 前端开发依赖的插件和库，都可以从 npm 中获取
- 构建工具的高度自动化，使得使用 npm 的成本非常低
- CommonJS 不会异步加载JS，而是同步一次性加载出来
#### 使用 CommonJS ####
<pre>
// util.js
module.exports = {
  getFormatDate: function(date, type) {
    if (type === 1) {
      return '2017-06-15'
    }
    if (type === 2) {
      return '2017年6月15日'
    }
  }
}

// a-util.js
var util = require('util.js')
module.exports = {
  aGetFormatDate: function(date) {
    return util.getFormatDate(date, 2)
  }
}
</pre>
- 代码演示下一节介绍
- 需要构建工具支持
- 一般和 npm 一起使用
#### AMD 和 CommonJS 的使用场景 ####
- 需要异步加载JS，使用AMD
- 使用了 npm 之后建议使用 CommonJS
#### 重点总结 ####
- AMD
- CommonJS
- 两者区别
### 7-9 构建工具-安装nodejs ###
- grunt
- gulp
- fis fis3
- webpack
#### 操作步骤 ####
- cd 目录
- node -v
- npm -v
- mac 
	- sudo npm install http-server -g
- windows
	- npm install http-server -g 
- http-server -p 8080
### 7-10 构建工具-安装webpack ###
- npm init
	- name: (webpack) webpack-test 注：这个名字不能叫webpack
	- version: (1.0.0) 按回车
	- description: webpack test
	- entry point: (index.js) 按回车
	- test command: 
	- git repository:
	- keywords:
	- author: guanqinghz@163.com
	- license: (ISC)
	- ...
	- Is this ok? (yes) yes
- npm install webpack --save-dev
- npm install jquery --save
- npm i moment --save
- npm uninstall moment --save
### 7-11 构建工具-配置webpack ###
- 创建 webpack.config.js
<pre>
var path = require('path')
var webpack = require('webpack')

module.exports = {
  context: path.resolve(__dirname, './src'),
  entry: {
    app: './app.js'
  },
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'bundle.js'
  }
}
</pre>
- src目录下面创一个 app.js
<pre>
console.log(100)
</pre>
- package.json
	- scripts下面创建"start":"webpack"
- npm start
- 创建 html , html引入 `<script src="/dist/bundle.js"></script>` 控制台输出100
### 7-12 构建工具-使用jQuery ###
- 完善 app.js
<pre>
var $ = require('jquery')

var $root = $('#root')
$root.html('&lt;p&gt;这是 jquery 插入的文字&lt;/p&gt;')
</pre>
- npm start
- 在src目录下面创建a-util.js
<pre>
  module.exports = {
    print: function () {
      console.log(123)
    }
  }
</pre>
- 继续完善 app.js
<pre>
var aUtil = require('./a-util.js')	//相对路径引入
aUtil.print()
</pre>
- npm start
### 7-13 构建工具-压缩JS ###
- 完善 webpack.config.js
<pre>
var path = require('path')
var webpack = require('webpack')

module.exports = {
  context: path.resolve(__dirname, './src'),
  entry: {
    app: './app.js'
  },
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'bundle.js'
  },
  plugins: [
    // 压缩 bundle.js
    new webpack.optimize.UglifyJsPlugin()
  ]
}
</pre>
- npm start
### 7-14 上线回滚-上线滚回流程 ###
#### 上线和回滚 ####
- 不会有具体的问题，交流询问的方式
#### 知识点 ####
- 上线和回滚的基本流程
- linux基本命令
#### 上线回滚流程介绍 ####
- 是非常重要的开发环节
- 各个公司的具体流程不同
- 由专门的工具后者系统完成，我们无需关系细节
- 如果你没有参与过，面试时也要说出要点
- 只讲要点，具体实现无法讲解
#### 上线流程要点 ####
- 将测试完成的代码提交到git版本库的master分支
- 将当前服务器的代码全部打包并记录版本号，备份
- 将master分支的代码提交覆盖到线上服务器，生成新版本号
#### 回滚流程要点 ####
- 将当前服务器的代码打包并记录版本号，备份
- 将备份的上一个版本号解压，覆盖到线上服务器，并生成新的版本号
#### linux基本命令 ####
- 服务器使用 linux 居多，server版，只有命令行
- 测试环境要匹配线上环境，因此也是 linux
- 经常需要登录测试机来自己配置、获取数据
### 7-15 上线回滚-linux基础命令 ###
- mkdir a
- ls
- ll
- cd a
- pwd
- cd ..
- pwd
- rm -rf a
- ll
- vi a.js
- :wq
- cp a.js a1.js
- mkdir src
- mv a1.js src/a1.js
- rm a.js
- cat a.js
- head a.js
- tail a.js
- tail -n 500 -f a.js
- grep '2' a.js
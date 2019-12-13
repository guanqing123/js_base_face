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
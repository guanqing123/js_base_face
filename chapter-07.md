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
# 前端工程化

## 开发环境搭建

### 使用浏览器配合手机调试&使用Proxy劫持

*  [chrome://inspect/\#devices](chrome://inspect/#devices)
* 劫持
  * Fiddler
  * Charles

## 前端工程化

### 介绍

* 指将前端开发的流程 **规范化、标准化**，包括开发流程、技术选型、代码规范、构建发布等，用于提升开发效率及代码质量

#### 前端工程化的意义

* 各个不同的端，要求不一样（pc、移动）
  * 兼容性，样式优化
  * 移动端可能用到Js压缩

#### Webpack的功能（构建发布）

* 代码的转义
* 模块的合并
* 混淆
* 代码分割
* 自动刷新
* 资源压缩
* 代码检查
* 预处理
* 开发 - 热更新
* 等等。。

### 目前常用

#### 项目配置

* gulp
  * 资源处理
    * gulp-uglify
    * gulp-sass
    * gulp-imagemin
    * gulp-concat
  * 任务及状态管理
    * gulp-plumber
    * run-sequence
  * 代码检查
    * gulp-jshint
    * gulp-eslint
  * 热更新
    * gulp-livereload
    * browser-sync
* WebPack
* rollup
* parcel

#### 脚手架工具

* yoeman
  * generator
  * yo命令

#### 自动化测试

* framework
  * Mocha+chai
  * Jasmine
  * Jest
  * Karma
* 工具
  * 断言
    * chai
  * 快照测试
  * 覆盖率
    * Istanbul
    * Jest
    * Blaket
    * codecov\(展示\)
  * e2e
    * Cypress
    * nightwatch
    * testcafe

## NVM安装及配置

### 安装

* [nvm-windows](https://github.com/coreybutler/nvm-windows) 下载安装
* [node以往的版本](https://nodejs.org/zh-cn/download/releases/)

```text
nvm list  // 你本机中所有的node的版本列表
nvm install latest  // 安装最新版本
nvm install 4.8.4  // 安装指定版本
nvm use 10.8.0  // 当前使用版本
```

### 配置淘宝源

* nvm
  * settings.txt
    * node\_mirror: https://npm.taobao.org/mirrors/node/
    * ~~npm\_mirror: https://npm.taobao.org/mirrors/npm/~~ 使用单独方式配置
* npm
  * 临时
    * npm --registry https://registry.npm.taobao.org install express1
  * 持久
    * npm config set registry https://registry.npm.taobao.org
  * 验证是否成功

```text
$ npm config get registry
https://registry.npm.taobao.org/ //成功返回

npm config set prefix "D:\BianChengRuanJian\nodejs" //配置用npm下载包时全局安装的包路径

$ npm info express

express@4.16.4 | MIT | deps: 30 | versions: 261   //成功返回
Fast, unopinionated, minimalist web framework
http://expressjs.com/

dist
.tarball http://registry.npm.taobao.org/express/download/express-4.16.4.tgz
.shasum: fddef61926109e24c515ea97fd2f1bdbf62df12e
....
```

* cnpm
  * 注意cnpm单独安装在nvm的独立node中
  * npm install -g cnpm --registry=https://registry.npm.taobao.org
  * 配置环境变量
    * 找到 _**cnpm.cmd**_ 的位置（默认在nvm安装时的nodejs中）
    * _**cnpm.cmd**_ 所在的目录路径，添加到path中（用户全局均可）
  * 测试
    * cnpm install -g @vue/cli@版本号

## Webpack

> [webpack 中文文档 ](https://www.webpackjs.com/concepts/)

### 核心概念

#### 入口

#### 输出

#### Loader（载荷）

* 帮我们把静态的资源文件去进行一些处理
* 在需要支持的时候，提供扩展能力

#### 插件

#### 模式/兼容性

### 基础使用

* npm init -y 全部使用默认选项进行快速配置初始化
* cnpm install webpack webpack-cli -D
* yarn add webpack webpack-cli -D
* ./node\_modules/.bin/webpack --version
* npx webpack --version
* ~~npx create -react-app~~
* package.json中

```text
"scripts":{
    "build":"webpack"
}
//npm run build
```

## Vue

#### 重点记录

* 双向绑定的原理，使用Object.defineproperty
* 组件化的思想

### 组件化思想



## Vue 中的 webpack命令

### ESLint

* --fix

```text
//如：
npx vue-cli-service  lint --fix Home.vue
```



## vuex

* 保存页面上使用到的状态量
  * 状态量可以是页面上的公共数据
  * 作用：跨组件去通信的功能
* 单向数据流
  * 通过数据驱动页面上所有的dom元素
* 操作state或者公共部分存储的状态量，必须使用mutations
* vue只会去监视data中lists对象的数据变化，而不会去监视lists数组中某一个对象的属性的数据变化
  * [Vue.set](https://cn.vuejs.org/v2/api/#Vue-set)
  * 作用：
    * 更新视图
    * 更新数据内容
    * 添加数据
* computed 与 watch区别
  * computed方法监视了所有在其方法体内实例的变量变化
* computed 与 methods区别
  * computed会自动触发，响应式
    * 如果依赖不是响应式，
      * [过滤](https://www.lodashjs.com/docs/lodash.filter)
  * methods需要执行


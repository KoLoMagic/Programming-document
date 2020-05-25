# Node.js - koa

## 项目基础

### npm

* 在终端中定位到项目文件夹
* 执行init命令，初始化项目的npm配置
* 执行install命令安装koa等
* 使用npm install 可安装 package.json 下 “dependencies” 中的所有包

### NPM报错、警告、异常

* npm WARN deprecated - 弃用警告

### NodeJS 能力

* 脱离浏览器运行JS
* NodeJS Stream（前端工程化基础）
* 服务端API
* 作为中间层

### Koa

* 精简
* 定制化能力强
* Koa初始化
* [Koa帮我们做了什么](https://www.cnblogs.com/sefaultment/p/10054905.html)

```javascript
// 项目初始化命令行
npm init
// 安装koa
npm install koa
```

### 项目中使用到的包的API

> [API库、框架和中间件有什么区别？](https://zgserver.com/api-3.html) （[备用链接](https://app.gitbook.com/@3360998464/s/program/~/drafts/-M7r_WChGoGWz-tTcL-T/da-qian-duan/shou-ji-zheng-li#2020-5-21)）

* [axios - API 中文文档](http://www.axios-js.com/)（易用、简洁且高效的http库）
* [koa-router - npm](https://www.npmjs.com/package/koa-router)（ koa路由中间件）
* [require-directory - npm](https://www.npmjs.com/package/require-directory)（可实现：路由自动注册）

### JS中导入导出包的方式

* commonJS（nodeJS支持方式）

```javascript
// 导入
require
```

* ES6（目前在nodeJS中为实验特性，暂不能常规使用）

```javascript
// 导入
import from
```

* AMD

### 暂不支持的ES新特性

* ES10，import
* decorator（装饰器）
* class
  * 不能把类的属性写在类下面，必须要把类的属性写在构造函数中，通过this.的方式定义

### Ecma TC39委员会（JS新特性）

* [https://github.com/tc39](https://github.com/tc39)

### Babel

* [Babel 是什么？](https://www.babeljs.cn/docs/index.html)

### VS code中的断点调试

* F9设置断点
* F5启动断点调试
* 配置断点调试启动方式

```javascript
{
            "type": "node",
            "request": "launch",
            "name": "node当前文件",
            "program": "${file}",
            "skipFiles": [
            "<node_internals>/**"
            ]
}
```

### Node server自动重启

* 安装nodemon

```javascript
npm i nodemon -g
```

* 使用nodemon启动server
  * 如 nodemon app.js
* 非全局安装使用npx nodemon命令运行，[npx 使用教程](http://www.ruanyifeng.com/blog/2019/02/npx.html)
  * 或者转换成npm脚本（在package-json中的scripts内写入）

## ES6

### static

> [static - JavaScript \| MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes/static)
>
> [Class 的基本语法 - ECMAScript 6入门 - 静态方法](https://es6.ruanyifeng.com/?search=static&x=0&y=0#docs/class#%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95)

*  类（class）通过 **static** 关键字定义静态方法。不能在类的实例上调用静态方法，而应该通过类本身调用。这些通常是实用程序方法，例如创建或克隆对象的功能。

## REST

> [什么是**REST API**](https://blog.csdn.net/D_R_L_T/article/details/82562902) ****

### **什么是REST**

* REST是万维网软件架构**风格（**非任何**协议**,非任何**规范）**
* 用来创建网络服务
* **Re**presentational **S**tate **T**ransfer
  * Representational：数据的表现形式（JSON、XML）
  * State：当前状态或者数据
    * 强调增删改查代表数据状态
  * Transfer：数据传输
    * REST中代表数据在互联网进行传输

### REST的六个限制

#### 客户端 - 服务器（Client - Server）

* 这个限制的本质，是一种软件架构思想：**关注点分离**
  * 关注点分离：各扫门前雪，自己管好自己的事
* 服务端专注数据存储，提升了简单性
* 前端专注用户界面，提升了可移植性

#### 无状态（Stateless）

* 所有用户会话信息都保存在客户端
* 每次请求必须包括所有信息，不能依赖上下文信息
* 服务端不用保存会话信息，提升了简单性、可靠性、可见性
  * 简单性：服务端少了很多代码
  * 可靠性：指软件的稳定程度，以及从一次故障中回复正常的能力
    * 如果服务端管理用户会话信息，一旦服务端出现故障，用户会话信息就会完全丢失
  * 可见性：在软件工程中的模块、接口之间的透明程度
    * 每次请求，都必须包括所有信息

#### 缓存（Cache）

* 所有服务端响应都要被标为可缓存或不可缓存
* 减少前后端交互，提升了性能

#### 统一接口（Uniform Interface）

* 接口设计尽可能统一通用，提升了简单性、可见性
* 接口与实现解耦，使前后端可以独立开发迭代

#### 分层系统（Layered System）

* 每层只知道相邻的一层，后面隐藏的就不知道了
* 客户端不知道是和代理还是真实服务器通信
  * 客户端只知道自己最相邻的一层：接口
  * 代理，可以作为分层系统中的一层
* 其它层：安全层、负载均衡、缓存层等
  * 安全层：提前终止错误的请求或不安全的请求
  * 负载均衡：软件或网站的用户量特别大，请求特别多（双11），就需要用很多的服务器，共同分担这些流量（流量分发）
  * 缓存层：缓存静态文件

#### 按需代码（Code-On-Demand 可选）

* 客户端可以下载运行服务端传来的代码（如：JS）
* 通过减少一些功能，简化了客户端

### 统一接口的限制

> REST风格的接口，应该设计成什么样

#### 资源的标识

* 资源是任何可以命名的事物，比如用户、评论等（REST是围绕着资源展开的）
* 每个**资源**可以通过**URI**被唯一的标识
  * URI：统一资源定位符（标识符），是用来标识某一互联网资源名称的字符串
    * 常见形式 - URL：统一资源定位符
      * 例1 - 请求Github的用户列表 - 唯一标识（定位）接口：https://api.github.com/users
      * 例2 - 请求特定用户： https://api.github.com/users/hanmeimei

#### 通过表述来操作资源

* 表述（Representation），比如 JSON、XML等
* 客户端不能直接操作（比如SQL）服务端资源
* 客户端应该通过表述（比如JSON）来操作资源

#### 自描述信息

* 每个消息（请求或相应）必须提供足够的信息让接受者理解
* 媒体类型（application/json，application/xml）
  * 有了媒体类型，接收者才能知道如何解析这些信息
* HTTP方法：GET（查）、POST（增）、DELETE（删）
* 是否缓存：Cache-Control
  * Cache-Control 决定了数据是否可以被缓存

#### 超媒体作为应用状态引擎

* 超媒体：带文字的链接
* 应用状态：一个网页，或一段JSON
* 引擎：驱动、跳转
* 合起来：点击链接跳转到另一个网页

## RESTful 

> RESTful：符合REST风格的

### RESTful API 简介

> Github的API是RESTful教科书级别的设计

#### 什么是RESTful API ？

* ful 形容词形式（beautiful）
* RESTful：符合REST风格的
* API：应用编程接口

#### RESTful API 具体的样子

* 基本的URI，如 https://api.github.com/users
* 标准HTTP方法，如GET、POST、PUT、PATCH、DELETE
* 传输的数据媒体类型，如JSON、XML

#### 现实举例

* GET /users \# 获取 user 列表
* GET /user/xxx \# 查看某个具体的 user
* PUT /users/xxx \# 更新 user xxx
* DELETE /users/xxx \# 删除 user xxx

### RESTful API 设计

#### 请求设计规范

* URI使用名词，尽量用复数，如 /users
* URI使用嵌套表示关联关系，如 /users/12/repos/5（ID为12的用户的5号仓库）
* 使用正确的HTTP方法，如GET/POST/PUT/DELETE
* 不符合CRUD（增删改查）的情况：
  * POST + 动词
    * Github多使用此种方式
  * action
    * 接口查询字符串：action = xxx
    * 查询字符串：？后面的东西
  * 子资源
    * 例：喜欢某个仓库，但不想设置喜欢这个动词
      * 可以设计成：users/repos/star
      * 喜欢：增加star
      * 不喜欢：删除star

#### 响应设计规范

> 响应就是接口的返回值

* 查询
  * 每个响应都是可以被查询的、过滤的
    * 限制返回的内容必须符合查询条件
      * 加上一些限制条件，就能返回符合这些限制的返回值
* 分页
  * 本质也是一种查询
  * 列表特别长，需要加上分页信息（第几页，每页有几条信息等）
* 字段过滤
  * 限制返回的结果只能返回指定的字段
* 状态码
  * 选择正确的状态码来作为请求的响应
* 错误处理
  * 如果请求是错误的，那么应该尽量将错误信息返回并遵循照规范的格式

## Koa基本使用

> [Koa -- 基于 Node.js 平台的下一代 web 开发框架](https://koa.bootcss.com/)

### 基础

* 导入

```javascript
const Koa = require('koa')
```

* 实例化
* new 出的实例称之为 应用程序对象
  * 应用程序对象
    * 特点：在对象中包含多个中间件

```javascript
const app = new Koa()
```

* 调用 listen \( \)，启动koa框架
  * 传入端口号，注意不要使用被占用的

```javascript
app.listen(3000)
```

* 在终端中启动app.js
  * 类似卡顿的现象代表阻塞状态（监听前端发送的HTTP请求）
  * ctrl+c  结束状态

```javascript
// 终端中
node app.js
```

## Koa中使用中间件来接收HTTP请求

> 应用程序（小程序、APP、网站等）中需要发送HTTP请求到后端来获取数据库中的内容

### 要点

* 使用中间件来接收HTTP请求
* **在koa编程中重点关注的两个东西**
  * **上下文**
  * **中间件**
* **中间件中的调用返回的一定是一个 promise**

### koa中间件

* 中间件就是是一个普通函数，定义一个中间件就是定义一个函数

```javascript
// 请求发送后，再执行test
const Koa = require('koa')

const app = new Koa()

function test() {
  console.log('hello');
}

test() // 不能在这里直接执行，需要使用中间件

app.listen(3000)
```

* 中间件需要注册才能使用（一个函数需要注册到应用程序对象上，才能变为中间件）
* 中间件一定是要注册的，但不一定要开发者自己注册
  * 如在使用koa-router中
  * [get 方法的第二个参数（第二个参数是一个中间件函数），是由 koa-router内部自动注册的](https://app.gitbook.com/@3360998464/s/program/~/drafts/-M7rI3DH7-cR6zAGKQBU/da-qian-duan/node.js+koa2-cong-0-dao-1-da-zao-chao-hao-yong-web-kuang-jia-yi-bu-dao-wei-zhang-wo-koa2-fu-wu-duan#koa-router-shi-pin-3-1)

```javascript
// 使用use方法注册中间件
app.use(test) // 在前端发送HTTP请求才能触发test的调用
```

* 前端发送请求

```javascript
// 发送请求有很多种，如小程序等，但最简单的方式是从浏览器中发送
localhost:3000
127.0.0.1:3000
```

* 大多数会使用匿名函数注册中间件

```javascript
app.use(()=>{
    console.log{'hello'}
})
```

* 一个应用程序中可以注册多个中间件
* 但koa只会自动调用第一顺序的中间件
* 其他中间件需要开发者自己调用
  * koa在调用中间件时，会传入两个参数
  * ctx：上下文（koa中的一个对象）；next：下一个中间件函数；
  * 使用next\( \)即可调用下一个中间件函数

```javascript
app.use((ctx,next)=>{
    console.log{'hello2'}
    next()
})

app.use(()=>{
    console.log('hello3')
})
```

#### 访问本地服务器

* 使用node命令启动js文件
* [http://localhost:3000/](http://localhost:3000/)
* 3000为自己设定的端口号

### 中间件必须按照洋葱模型来执行

#### 为什么中间件必须按照洋葱模型来执行

```javascript
const Koa = require('koa')

const app = new Koa()

// 1
app.use((ctx, next) => {
  console.log(1)
  next()
  console.log(2)
  // 模拟情景：此处有一段逻辑代码（如计时）
  // 这段代码的执行前提是：其他三个中间件全部执行完毕，再执行
  // 问题：如何知道后面三个中间件已经执行完毕？
})
// 2
app.use((ctx, next) => {
  console.log(5)
  next()
  console.log(6)
})
})
// 3
app.use((ctx, next) => {
  console.log(5)
  next()
  console.log(6)
})
// 4
app.use((ctx, next) => {
  console.log(7)
  next()
  console.log(8)
})

app.listen(3000)

// 中间件的执行顺序，依次执行1234
```



### 什么是洋葱模型

> [koa洋葱模型原理和co原理](https://zhuanlan.zhihu.com/p/112750775)

#### 问题：以下代码的执行顺序

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx,next)=>{
    console.log(1)
    next() // 4执行完毕后，回到此处继续执行
    console.log(2)
})

app.use((ctx,next)=>{
    console.log(3)
    next() // 未知
    console.log(4)
})

app.listen(3000)

// 顺序1 3 4 2
```

### 如何保证洋葱模型

* 保证洋葱模型的先决条件：在每一个next\( \)前，都加上await
* 洋葱模型是以next \( \)为分界线的
* next \( \)之前的代码说明后续的中间件还没有开始执行
* next \( \)之后的代码表明这些所有的中间件已经执行完毕

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx,next)=>{    // 
    console.log(1)
    await next()     // 
    console.log(2)
})

app.use(async (ctx,next)=>{
    console.log(3)
    await next() 
    console.log(4)
})

app.listen(3000)

```

### 不按照洋葱模型执行会引起什么样的情况

* 模拟场景：在第二个中间件函数中把res传递到第一个中间件中

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(1)
  await next()
  console.log(2)
})

app.use((ctx, next) => {
  console.log(3)
  const axios = require('axios')
  const res = await axios.get('http://www.baidu.com')
  await next()
  console.log(4)
})

app.listen(3000)
// 场景：在第二个中间件函数中把res传递到第一个中间件中
```

* 使用return的方式，可以获得传参结果，但有局限性
  * 局限性在于
  * 所有的中间件必须能够完全掌控**调用顺序**（如：全部都是由自己编写）

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(1)
  await next()
  console.log(2)
})

app.use((ctx, next) => {
  console.log(3)
  const axios = require('axios')
  const res = await axios.get('http://www.baidu.com')
  return res  // 使用return的方式
  await next()
  console.log(4)
})

app.listen(3000)
// 场景：在第二个中间件函数中把res传递到第一个中间件中
```

* 但koa过于精简，需要用到大量的第三方中间件
* 但第三方中间件的执行顺序是不可控的
* 这种情况下就不能使用return，需要利用ctx

#### ctx：上下文的作用

* koa中的操作基本都是在操作ctx（context）
* 比如常见的操作：两个中间件或者多个中间件之间传递参数
* 每一个中间件函数在执行的时候都会被注入一个ctx
* 把获取到的res保存到ctx上
* 调用时必须在await之后，才能保证洋葱模型
* 如不保证洋葱模型，将返回undefined

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(1)
  await next()    // 使用ctx.r，就需要保证第二个中间件全部执行完毕
  const r = ctx.r // 所以ctx必须在await之后使用，才能保证上述问题
  console.log(2)
})

app.use((ctx, next) => {
  console.log(3)
  const axios = require('axios')
  const res = await axios.get('http://www.baidu.com')
  ctx.r = res // 把res保存到ctx.r上
  await next()
  console.log(4)
})

app.listen(3000)
// 场景：在第二个中间件函数中把res传递到第一个中间件中
```

* 去除无用代码

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  await next()
  const r = ctx.r  
  console.log(r);  // 打印出http://www.baidu.com的HTML
})

app.use((ctx, next) => {
  const axios = require('axios')
  const res = await axios.get('http://www.baidu.com')
  ctx.r = res
  await next()
})

app.listen(3000)
// 场景：在第二个中间件函数中把res传递到第一个中间件中
```

## \*  async await - 异步编程的终极解决方案

### 为什么不直接使用promise而使用async与await

* 如果不用await，那么next\( \)的调用结果一定是一个promise对象

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx,next)=>{     
    console.log(1)
    const a = next()     
    console.log(a)    // 返回 promise{undefined}，undefined是因为第二个函数无返回值
    console.log(2)
})

app.use((ctx,next)=>{
    console.log(3)
    next() 
    console.log(4)
})

app.listen(3000)
// 打印顺序 1 3 4 promise 2
```

* 中间件中是可以return的

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx,next)=>{     
    console.log(1)
    const a = next()     // 返回 promise{'abc'}
    console.log(a)    
    console.log(2)
})

app.use((ctx,next)=>{
    console.log(3)
    next() 
    console.log(4)
    return 'abc'
})

app.listen(3000)
// 打印顺序 1 3 4 promise 2
```

* 使用then接收promise中的具体内容

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx,next)=>{     
    console.log(1)
    const a = next()     
    a.then((res)=>{
        console.log(res)    // abc
    })
    console.log(2)
})

app.use((ctx,next)=>{
    console.log(3)
    next() 
    console.log(4)
    return 'abc'
})

app.listen(3000)
// 使用then方式，但还是不够直观
```

* 使用async和await的方式会更直观

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx,next)=>{ 
    console.log(1)     
    const a = await next() // abc
    console.log(a)
    console.log(2)
})

app.use((ctx,next)=>{
    console.log(3)
    next() 
    console.log(4)
    return 'abc'
})

app.listen(3000)
```

### await的意义

* await的第一个作用 - 求值关键字

  * 会把promise执行成功后的res返回给常量a
  * await也可对表达式进行求值，不仅仅使用在promise上

* await的第二个作用 - await会阻塞当前的线程
  * 当await后面调用的是一个异步函数时
    * 异步操作：对资源的操作一般都是异步请求，如读文件、发送http请求、操作数据库
  * 等待的意义
    * 可以把难以处理的异步函数的调用变为同步的
      * 因为当前的线程被阻塞后，必须要得到最终的返回结果，才能执行后续的代码
  * 虽然会阻塞当前的线程，但不会卡住，线程可以切换到别处去运行别的代码

#### 把上述第二个中间件函数变为异步

> [axios - API 中文文档](http://www.axios-js.com/)

* 需要在第二个函数中发送一个HTTP请求
  * 需要使用axios（易用、简洁且高效的http库）
  * get中的地址如不能正常访问，会导致报错

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(1)
  console.log(2)
})

app.use((ctx, next) => {
  console.log(3)
  const axios = require('axios') // 首先引入库
  // 模拟向一个API或者网站发送一个get请求
  const res = axios.get('http://www.baidu.com') // get()中可以直接输入一个API的地址或任意网站的网址，使用const res接收
  console.log(4)
  return 'abc'
})

app.listen(3000)
```

* 只关注await的第二个作用 —— 阻塞线程，去除无用代码
  * 只观察异步调用
  * 假设条件：此次异步请求非常耗时（网速非常慢或加载的内容非常多）
  * 若请求时长为1min，那么res的结果也将在1min后接收
    * 也就是第9行的代码需要1min后才会走到11行

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx, next) => {
  console.log(3)
  const axios = require('axios') 
  debuger
  const res = axios.get('http://www.baidu.com')  
  debuger
  console.log(4)
})

app.listen(3000)
```

* 非阻塞演示
* 在请求之前、请求之后记录当前的时间戳

```javascript
const Koa = require('koa')

const app = new Koa()

app.use((ctx, next) => {
  const axios = require('axios')
  const start = Date.now()
  const res = axios.get('http://www.baidu.com')
  const end = Date.now()
  console.log(end - start); // 耗时0，因线程不会阻塞
})

app.listen(3000)
```

* 使用await演示阻塞状态

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  const axios = require('axios')
  const start = Date.now()
  const res = await axios.get('http://www.baidu.com')
  const end = Date.now()
  console.log(end - start); // 耗时不定
})

app.listen(3000)
```

* 返回阻塞状态的调用结果

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  const axios = require('axios')
  const res = await axios.get('http://www.baidu.com')
  console.log(res); // 返回 http://www.baidu.com 的HTML
})

app.listen(3000)
```

* 直接返回html的原理
  * axios.get 会返回一个promise
  * await用求值的特性会把这个promise给计算出来，同时也会把当前的线程阻塞

#### 

* await对异步编程的意义
  * 添加await后，使本来是异步的调用变为同步的调用

## 

### async的意义

* 如果在一个函数的前面加上了async，那么这个函数任何的返回值都会被包装成一个promise
* 加不加async返回的都是一个promise
  * 之所以加是因为这个中间件函数的内部使用了await，[await关键字只能够出现在async函数之中](https://blog.csdn.net/qq_38969618/article/details/103026314)

## 

### await与异常

#### await可以释放promise中的异常

* 不用throw，也可以使用try catch捕获异常
* 如果不使用await，则会产生一个未处理的异常，抛出Unhandled promise 
  * 代表在promise中产生了一个异常，但在外部却没有处理

#### 注意

* async await是最简单的处理异步异常的方案
* 其他方案
  * 通过取到promise，使用promise catch处理

## 路由

### koa中获取url路径及HTTP动词

#### 使用ctx上的参数，来获取url路径

* 使用 [**request.path**](https://koa.bootcss.com/#request) ****获取路径
* 使用 [**request.method**](https://koa.bootcss.com/#request) ****获取HTTP动词
* 使用 ctx.body 返回内容
* 文档中的request.在真正使用时要换成ctx.
  * 将信息封装到request对象上，并可以通过别名简化访问 - [**别名**](https://koa.bootcss.com/)\*\*\*\*

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(ctx.path);
  console.log(ctx.method);
  if (ctx.path === "/classic/latest" && ctx.method === "GET") {
    ctx.body = 'classic' // 返回字符串
  }
})

app.listen(3000)
```

* 返回json对象
  * 把JS对象赋值给ctx.body
  * koa内部会自动序列化
    * 会在HTTP请求中的Response Headers下的Content-type自动设置为application/json

```javascript
const Koa = require('koa')

const app = new Koa()

app.use(async (ctx, next) => {
  console.log(ctx.path);
  console.log(ctx.method);
  if (ctx.path === "/classic/latest" && ctx.method === "GET") {
    ctx.body = { key: 'classic' }
  }
})

app.listen(3000)
```

### koa路由第三方中间件：Koa-router的使用

> #### _第三方中间件_ [_koa_-_router_ - npm](https://www.npmjs.com/package/koa-router)

#### 基本使用

* 导入 koa - router
* 实例化 router（一个router实例对象是可以编写多个路由函数的）
* 调用 router 处理HTTP动词的方法 [router.get\|put\|post\|patch\|delete\|del](https://github.com/koajs/router/blob/HEAD/API.md#routergetputpostpatchdeletedel--router)，编写路由函数
  * get 方法接收两个参数
    * 第一个参数：指明这个路由函数所对应的地址是什么
    * 第二个参数：需要传入一个函数，当 koa-router 监听到用户当前访问的 url 地址与第一个参数设置的地址一致时，会自动调用这个函数，此函数可写成匿名函数
      * 虽然第二个参数是一个函数，但实质上也是一个中间件。
        * 既然是中间件，所以可以接收 ctx 以及 next 两个参数
        * 既然是中间件，就需要注册，但此中间件是由 koa-router内部自动注册的，不需要手动的显式注册（显式注册：app.use）
* 使用router.routes\( \)来得到一个中间件
  * 因koa都是使用中间件编程
* 使用 app.use \( \) 把得到的中间件注册到 app 上面

```javascript
const Koa = require('koa')
const Router = require('koa-router') // 导入koa-router

const app = new Koa()
const router = new Router() // 实例化koa-router

router.get('/classic/latest', (ctx, next) => {  // 编写路由函数
  ctx.body = { key: 'classic' }
})

app.use(router.routes()) // 注册中间件

app.listen(3000)

```

### 改造koa-router

> 改造的目的：好的代码是可阅读性高、开发效率高、利于维护的

#### 路由的主题与模型划分

> 把不同的路由拆分到不同的文件中去

* 划分方式：可根据数据的类型（不同项目，划分方式不同）
* 主题与主题之间并不是绝对孤立的
* 对主题的划分直接影响了如何设计项目的数据库（好的主题划分，可以让数据库设计变的更简单）
* 对主题的划分是渐进式的，首先先找到核心主题

#### 概念 - API版本

* 为什么需要版本
  * 应对业务或需求变更
  * 客户端版本更新时，老版本不更新（出现异常）
  * 所以服务器的API需要兼容多个版本（v1、v2、v3...）
    * 支持的版本越多，维护成本就会越高
* 多版本如何支持
  * 客户端发送API请求时，需要携带版本号
    * 版本号携带策略
      * 加在url路径中
      * 加在查询参数中
      * 加在HTTP的header中

```javascript
const Koa = require('koa')
const Router = require('koa-router')

const app = new Koa()
const router = new Router()

// 主题：期刊
router.get('/v1/classic/latest', (ctx, next) => { // 版本号放在url路径中
  ctx.body = { key: 'classic' }
})

// 主题：书籍
router.get('/v1/book/latest', (ctx, next) => {
  ctx.body = { key: 'book' }
})

app.use(router.routes())

app.listen(3000)

```

* 多个版本API如何区分
  * 问题：多版本写在一个路由函数中，还是分开？
    * 一个路由函数
      * 会让函数的逻辑变得复杂
    * 开闭原则 [设计模式六大原则：开闭原则](https://www.cnblogs.com/az4215/p/11489712.html)
      * 在编程时，对代码的修改是关闭的
      * 对代码的扩展是开放的
  * 结论：应该对每一个版本的API都去写一个路由

## 

### 路由自动注册第三方库：require-directory的使用

> 替代模块导入require、手动注册 app.use\(\)
>
> 重要思想：动脑筋思考是否能对koa-router进行**循环**处理

#### 自动注册的原理

* 自动导入模块（相当于在指定目录中寻找所有的路由模块，并自动require）
* 自动使用use方法注册（把自动导入的模块，循环注册到APP上）
* 问题：如何加载指定目录下的所有路由模块？
  * 自己手写
  * 或使用require-Directory解决

#### require-directory的使用（高级用法）

> [require-directory](https://www.npmjs.com/package/require-directory)

* 导入requireDirectory
* 直接使用requireDirectory \( 参数1，参数2，参数3 \)，**不需要实例化（不需要new）**
  * 参数1：module（可以认为是固定参数）
  * 参数2：被导入模块的 **目录的路径**（可以是模块具体路径，但能批量导入为什么要一个一个的传入？）
  * 参数3：用于设定对每一个参数2的处理方法（循环遍历注册）
    * 参数3是一个对象，含有一个visit属性，此属性可以被赋值一个回调函数
      * 此回调函数可以在每当requireDirectory加载到模块的时候，自动调用
      * 此回调函数可以接收一个参数，在函数中判断此参数是否是一个Router
      * 如果是Router则使用routes\( \)注册

```javascript
const Koa = require('koa')
const requireDirectory = require('require-directory') // 导入
const Router = require('koa-router')

const app = new Koa()

// 参数1：module返回的是classic及book的Router
// 参数2：'./api'指加载v1和v2中所有的路由模块，'./api/v1'指只加载v1的模块
// 参数3：设定对每一个参数2的回调处理
requireDirectory(module, './api', { visit: whenLoadMoule })

// 遍历注册
function whenLoadMoule(everyModule) {
  if (everyModule instanceof Router) {  // 对应模块导出方式：module.exports = router,如果是{router}形式，需要进行兼容处理
    app.use(everyModule.routes())
  }
}

app.listen(3000)

```

#### 扩展

* 目前的whenLoadModule函数只兼容router不加{ }的导出模式
* 可以进一步加强此函数，兼容两种模式

## 

### 初始化管理器与使用Process获取绝对路径

#### Process获取绝对路径

* 为什么需要？
  * 解决路径硬编码的问题
* 如何使用？
  * [process.cwd](http://nodejs.cn/api/process.html#process_process_cwd)
* process是node.js中的全局变量

```javascript
console.log(`当前工作目录是: ${process.cwd()}`);
```

#### 代码重构

```javascript
//app.js

const Koa = require('koa')

const InitManager = require('./core/init')

const app = new Koa()
InitManager.initCore(app)

app.listen(3000)
```

```javascript
// core\init.js

const Router = require('koa-router')
const requireDirectory = require('require-directory') // 导入

class InitManager {
  // 入口方法
  static initCore(app) {
    // 把应用程序对象（app）保存在类中
    InitManager.app = app
    InitManager.initLoadRouters()
  }

  // 自动加载、注册路由
  static initLoadRouters() {
    // 获取绝对路径
    // eslint-disable-next-line
    const Apidirectory = `${process.cwd()}/app/api`

    // 参数1：module返回的是classic及book的Router
    // 参数2：'./app/api'指加载v1和v2中所有的路由模块，'./app/api/v1'指只加载v1的模块
    // 参数3：设定对每一个参数2的回调处理
    requireDirectory(module, Apidirectory, { visit: whenLoadMoule })

    // 遍历注册
    function whenLoadMoule(everyModule) {
      if (everyModule instanceof Router) {  // 对应模块导出方式：module.exports = router,如果是{router}形式，需要进行兼容处理
        InitManager.app.use(everyModule.routes())
      }
    }
  }
}

module.exports = InitManager
```

## 

### 端口测试工具：PostMan的使用

> [Postman \| The Collaboration Platform for API Development](https://www.postman.com/)

#### 为什么需要？

* post等高级请求不能直接在浏览器的url中进行发送
  * 浏览器的url只支持get请求

### koa中参数的传递

#### 常用传参模式

* url 路径中传参
* url 的?后传参（一般叫做查询参数）
* HTTP的header中传参
* HTTP的body中传参（只可使用post）
  * 使用第三方库 [koa-bodyparser](https://www.npmjs.com/package/koa-bodyparser) 来获取
  * koa-bodyparser是一个中间件，首先需要注册
    * parser\( \)需要被调用后才能返回一个中间件

#### koa中四种参数的获取方式

* 在koa中查询参数是没有必要显式的写在路由（url）中的，所有参数都可以直接获取到
* 但如果在url中想接收参数，需要使用 : 加上参数名称

```javascript
router.post('/v1:id/classic/latest?param=souhu.com', (ctx, next) => {  // url中的参数获取方式

})
```

### 参数获取第三方中间件：koa-bodyparser 的使用

> [koa-bodyparser - npm](https://www.npmjs.com/package/koa-bodyparser)

#### 为什么需要？

* 使用koa-bodyparser获取body中的参数比较便捷

#### 如何使用

* 导入 koa-bodyparser 中间件
* 注册 koa-bodyparser 中间件

## 异常处理

### 函数设计

* 函数的异常处理
  * 在函数的内部判断出异常，然后return false或者null（不推荐）
    * 有可能会丢失异常信息
  * throw 抛出异常
* 正确的异常处理
  * try catch，在catch中throw 抛出异常
* 全局异常处理
  * 机制
    * 监听任何异常
* 异步异常处理
  * try catch更适用于同步异常，有可能会捕捉不到异步异常

### 全局异常处理

* 使用koa的特色 —— 中间件，来实现全局异常处理
  * 监听错误
  * 监听到后，输出一段有意义的提示信息
* 使用到的思想
  * AOP：面向切面

### 已知错误、未知错误

* 上述全局异常处理的问题
* 在程序中捕捉到的error，不应该直接返回到客户端去
  * 因为error的信息量很大
  * 除了包含常见的error信息，如：错误的名称，错误的原因
  * 还包括一些复杂的信息，如：堆栈调用的信息
  * 所以要对error简化，返回一些清晰明了的信息到客户端
* 应该给客户端返回哪些信息
  * HTTP Status Code，[指定HTTP常见的状态码](https://koa.bootcss.com/#response)（如2XX、4XX、5XX）
    * 在koa中，如果要指定一次请求返回结果的HTTP Status Code，可以通过设置上下文ctx变量上面属性来实现
  * 开发者自定义信息
    * message：错误信息
    * error\_code：更详细的错误代码（如 10001 20003）
    * request url：访问的url

#### 已知型错误

* 用户传入的参数不符合校验规则

#### 未知型错误

* 程序潜在错误
  * 无意识错误
  * 或根本不知道错误已经发生
  * 如：连接数据库

### 定义HttpException异常基类

### 特定异常类与global全局变量

* 改善上述HttpException异常基类在使用时，每次都需要传入msg，errorCode、code
* 使用全局变量global来改善每次都需要导入异常中间件的问题
  * 但不推荐
  * 拼错单词导致的异常不明确，不容易排查

```javascript
class InitManager{
    static initCore(app){
        //入口方法
        InitManager.loadHttpException()
    }

    static loadHttpException(){
        const errors = require('./http-exception')
        global.errs = errors
    }
}

module.exports = InitManager
```

###  Lodash库的使用 - Lin-Validator获取HTTP参数

> [Lodash 中文文档](https://www.lodashjs.com/)
>
> [Lodash Documentation](https://lodash.com/docs/4.17.15)

* get方法的原理
* JS库 - lodash

  * 提供对数组、函数、日期、集合等数据结构的操作
  * 深拷贝：[cloneDeep](https://www.lodashjs.com/docs/lodash.cloneDeep)

* isInt的原理
* 第三方库 - validator.js
  * [Validator.js验证工具](http://wangchujiang.com/validator.js/)
  * [validate.js](https://validatejs.org/)
  * [validator - npm](https://www.npmjs.com/package/validator)

### 数据库 - 用户系统设计

> [XAMPP Installers and Downloads for Apache Friends](https://www.apachefriends.org/index.html)

#### 用户系统

* 通用用户系统
  * 帐号、密码
    * 附属信息：昵称、email、手机
  * 注册
    * 注册的信息提交到API中，存储到数据库中
  * 登录
* 小程序用户系统

#### 关系型数据库

* My SQL、Oracle、SQL  Server、Postgress SQL
* 本项目通过ORM操作数据库
  * 类似在对象上调用了一个方法

#### 非关系型数据库

* Redis（Key : value）
  * 更多用来做缓存使用，提高查询及获取数据的速度
  * 也可作为持久存储数据使用
* MongDB（文档型数据库）
* 相对于ORM，非关系型数据库可以使用ODM的模式操作数据库




# JavaScript 学习笔记

## 闭包

> [JavaScript 闭包 \_ 菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

#### 作用

* 可以使得函数拥有私有变量
* 闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。
* 直观的说就是形成一个不销毁的栈环境。

## JS变量、作用域

### 全局变量

* [JavaScript 关于全局对象](https://www.cnblogs.com/echo-dauntless/p/9737451.html)
*  变量声明时如果不使用 **var** 关键字，那么它就是一个全局变量，即便它在函数内定义。
* 在web页面中全局变量属于 window 对象

### 变量生命周期

* 全局变量的作用域是全局性的
* 函数内部声明的变量，只在函数内部起作用
* 函数的参数也是局部性的，只在函数内部起作用

### 深拷贝、浅拷贝

* [深拷贝和浅拷贝最根本的区别在于是否真正获取一个对象的复制实体，而不是引用。](https://www.cnblogs.com/mikeCao/p/8710837.html)

### JS中延长作用域链的方法

* [with](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/with)
* 延长作用域链，会影响查询速度
  * 只是少写了变量的名称
* **不推荐使用**

### JS解析机制 - 预解析

* JS解析过程
  * 预解析
    * 分别在全局作用域与局部作用域预解析
    * 全局
      * 查找所有的var
        * 查找后的var赋值undefined
      * 查找function
        * 拿到function后的方法名称（如：fn）
        * 预解析时就已经声明了fn
    * 局部
      * 查找所有var
        * 查找后的var赋值undefined
      * 查找参数（argument）
        * 查找后的argument赋值undefined
      * 查找function
        * 拿到function后的方法名称（如：fn） 
        * 预解析时就已经声明了fn
  * 逐行解读代码
    * 把具体数值赋值给预解析的var
      * 没有具体数值的变量会保留undefined
    * function会在此阶段跳过，继续执行下面的代码
      * 因为已经在预解析时声明过了

```javascript
var name = 'xm'
var age = 18
function fn(argument){
    console.log(name)
    var name = 'xh'
    var age = 10
}
fn()
// 输出undefined
```

#### 需要注意的问题

* argument（参数）与局部变量同等对待
* 同名冲突
  * 变量与变量冲突
    * 如声明两次同名变量，则在预解析时，都会执行一遍undefined
  * 变量与函数名冲突
    * 预解析时var会被舍弃，保留function
  * 函数与函数冲突
    * 后声明的留下
* 代码风格问题
  * 声明函数在全局、函数下声明或充当变量方法
  * 不要在判断或循环中声明
    * 老版本浏览器预解析不到
* JQuery中的window
  * 把window作为一个参数传入函数中
    * 传入后变为局部变量，执行速度会更快
    * 方便压缩代码

### 作用域问题示例

#### 问题1

```javascript
console.log(a) //a为undefined
var a = 1 // a为1

//
console.log(a) // 报错
a = 1 // 预解析时无var
```

#### 问题2

```javascript
console.log(a) 
var a = 1
console.log(a)
function a () {
    console.lgo(2)
}
console.log(a)
var a = 3
console.log(a)
function a () {
    console.log(4)
}
console.log(a)
a()

// 预解析
function a () {
    console.log(4)
}

// 逐行执行
a()
1
1
3
3
报错 // 此时a为3，非函数，不能执行，所以报错
```

#### 问题3

```markup
<script>
    console.log(a)
</script>

<script>
    var a = 1
</script>

// 报错 预解析是分标签进行的
```

```markup
<script>
    var a = 1
</script>

<script>
    console.log(a)
</script>

// 1 
```

#### 问题4

```javascript
var a = 1
function fn () {
    console.log(a) // undefined 
    var = 2
}
fn()
consolo.log(a) // 1

// 预解析 全局
a = undefined
fn()
// 预解析 局部
a = undefined
```

```javascript
var a = 1
function fn () {
    console.log(a) // 1
    a = 2          // 2
}
fn() // 1
cosole.log(a) // 2

// 预解析 全局
a = undefined
fn()
//预解析 局部
没有预解析
a 通过作用域链 寻找到a = 1

//逐行执行
a = 1
fn() // 1
a = 2
console.log(a) //2
```




# JavaScript 学习笔记

## 闭包

> [JavaScript 闭包 \_ 菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

#### 作用

* 可以使得函数拥有私有变量
* 闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。
* 直观的说就是形成一个不销毁的栈环境。

## JS变量、作用域

> 变量是保存数据的容器，要弄清变量就要弄清数据

### 变量

| 基本类型 | 引用类型 |
| :--- | :--- |
| 不可修改 | 可以修改 |
| 保存在栈内存中 | 保存在堆内存中 |
| 按值访问 | 按引用访问 |
| 比较时，值相等即相等 | 比较时，同一引用才相等 |
| 复制时，创建一个副本 | 复制的其实是指针 |
| 按值传递参数 | 按值传递参数 |
| 用typeof检测类型 | 用instanceof检测类型 |

#### 全局变量

*  变量声明时如果不使用 **var** 关键字，那么它就是一个全局变量，即便它在函数内定义。
* **不推荐使用，会造成变量的污染**

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

## 

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
function a () { // 根据函数之间的冲突规则，最后一个声明的函数存活
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

```javascript
var a = 1
function fn (a) {
    console.log(a) // undefined
    a = 2
}
fn()
console.log(a) // 1

// 预解析
var a = undefined
argument a = undefined // 参数与局部变量同等待遇
```

```javascript
var a = 1
function fn (a) {
    console.log(a)
    a = 2
}
fn(a) // 1
console.log(a) // 1
```

## 

### 垃圾收集机制

> JS中为自动收集，另有手动收集，如[_Objective_-_C_](https://www.runoob.com/w3cnote/objective-c-tutorial.html)

#### 作用

* 释放内存中的无用数据
* 回收内存

#### 原理

* 找出无用数据，并标记
* 释放内存
  * 垃圾收集器，周期性执行

#### 标识无用数据的策略

* 标记清除（绝大部分浏览器使用，区别在于回收时间间隔）
  * 标记垃圾
    * 垃圾收集器在运行时，会将存储在内存中的所有变量（数据通过变量来访问），一次性都加上标记
  * 去除标记
    * 环境中的变量，以及被这些环境变量所引用的变量
      * 环境中的变量：变量还没有离开其执行环境
        * 如：函数中的局部变量，在其函数未执行完毕之前
  * 清除

    * 销毁带标记的数据，并回收所占用的内存
* 引用计数
  * 跟踪记录每个数据被引用的次数
    * 当声明一个变量时，并将一个引用类型的值赋值给这个变量，此为引用一次
    * 当这个值又被另外一个变量所引用，此为又引用一次，共计引用两次
    * 当所引用的值是新值时，原值的引用次数减一，新值的引用次数加一
    * 当被引用的值的引用次数为0时，代表无任何引用，可回收其占用的内存
  * 引用计数带来的问题
    * 循环引用
      * 循环引用：对象A中包含一个指向对象B的指针，对象B中也有一个包含指向对象A的指针

```javascript
//循环引用1
function fn () {
    var xm = {} //别名{}A，此为{}A被引用一次
    var xh = {} //别名{}B，此为{}B被引用一次
}
fn() // 执行完毕后解除引用，解除引用会使 xm xh 均默认赋值为null，导致{}A与{}B的引用次数各减一
     // 现{}A与{}B的引用次数均为0

//循环引用2
function fn () {
    var xm = {} //别名{}A
    var xh = {} // 别名{}B
    xm.wife = xh // xm.wife 及 xh 引用了同一个{}B，此时{}B的引用次数为2
    xh.husband = xm // xh.husband 及 xm 也引用了同一个{}A，此时{}A的引用次数也为2
}
fn() // 当解除引用并默认赋值为null时，{}A与{}B的引用次数均减一，均为引用一次
     // 引用不为0会导致永远不会被回收，此函数调用几次，就会产生几次的废数据

```

* IE浏览器的特殊问题
  * IE9之前的版本中的DOM与BOM中的对象并不是原生的
    * 是通过C++在COM对象的基础上来实现的
  * COM对象的实现采用了引用计数的方式来进行垃圾回收
  * 所以循环引用的问题依然存在于IE9之前的版本

```javascript
// IE中循环引用的问题
var obj = {}
var elem = document.getElementById('box') // DOM
elem.someAttr = obj
obj.someProperty = elem

// 解决方法，手动解除引用
elem.someAttr = null
obj.someProperty = null
```




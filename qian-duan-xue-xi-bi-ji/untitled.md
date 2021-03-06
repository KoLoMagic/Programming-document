# JavaScript

## JS 变量、作用域

### 变量

> 变量是保存数据的容器，要弄清变量就要弄清数据

| 基本类型 | 引用类型 |
| :--- | :--- |
| 不可修改 | 可以修改 |
| 保存在栈内存中 | 保存在堆内存中 |
| 按值访问 | 按引用访问 |
| 比较时，值相等即相等 | 比较时，同一引用地址才相等 |
| 赋值时，创建一个新的栈空间 | 赋值的是内存地址 |
| 按值传递参数 | 按值传递参数 |
| 用typeof检测类型 | 用instanceof检测类型 |

#### 要点

*  变量声明时如果不使用 **var** 关键字，那么它就是一个全局变量，即便它在函数内定义。
  * **不推荐使用，会造成变量的污染**

### 作用域

> [作用域是可访问变量的集合](https://www.runoob.com/js/js-scope.html)，JS中有全局作用域和局部作用域之分

* 全局作用域中的变量，为全局变量
* 局部作用域中的变量，为局部变量
* 局部作用域在JS中主要指函数作用域，JS中无块级作用域
  * 函数内部声明的变量，只在函数内部起作用
  * 函数的参数也是局部性的，只在函数内部起作用

### 作用域链

> 作用域链是用来查询变量的

#### 要点

* 全局作用域中的全局对象 与 不同局部作用域的局部对象所链接构成
* 作用域链由内层向外层进行查询，直至查询到全局对象为止
  * 如到全局对象仍未查询到，会报错
  * 如在某一作用域中查询到，就不会继续向外查找
* 全局对象：浏览器中为wiondow，node.js中为global

#### 深拷贝、浅拷贝

* [深拷贝和浅拷贝最根本的区别在于是否真正获取一个对象的复制实体，而不是引用。](https://www.cnblogs.com/mikeCao/p/8710837.html)

#### JS中延长作用域链的方法

* [with](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/with)
* 延长作用域链，会影响查询速度
* 优点为少写了变量的名称
* **不推荐使用**

### JS解析机制

#### 要点

* 预解析时，argument（参数）与局部变量同等对待
* 同名冲突
  * 变量与变量冲突
    * 如声明两次同名变量，则在预解析时，都会执行一遍undefined
  * 变量与函数名冲突
    * 预解析时var会被舍弃，保留function
  * 函数与函数冲突
    * 后声明的留下
* 代码风格问题
  * **声明函数尽量在全局、函数下声明或充当变量方法**
  * **不要在判断或循环中声明函数**
    * 老版本浏览器可能预解析不到
* JQuery中的window
  * 把window作为一个参数传入函数中
    * 传入后变为局部变量，执行速度会更快
    * 方便压缩代码
* 多个&lt;script&gt;标签中的规则
  * 按顺序进行解析

#### JS解析过程

* 预解析
  * 分别在全局作用域与局部作用域预解析
  * 全局
    * 查找所有的var
      * 查找后的var赋值undefined
    * 查找function
      * 拿到function后的方法名称（如：fn）
      * 预解析时会声明fn
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
//输出undefined
```

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
    console.log(4) // 根据函数之间的冲突规则，最后一个声明的函数存活
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
// 预解析 局部
没有预解析
a 通过作用域链 寻找到a = 1

// 逐行执行
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

## 

### 内存管理

#### 需要内存管理的主要原因

* 分配给 Web浏览器的内存 **少于** 其他桌面应用程序
  * 出于安全性的考虑：防止运行JS的网页耗尽全部系统内存导致系统崩溃

#### 释放内存的方式

* 解除引用：将其设置为null
  * 适用于大多的全局变量
    * 局部变量离开作用域时，会被自动的解除引用

## JS 函数

### JS 对象简介

> [JS中的对象，就是任意值的集合](https://www.runoob.com/js/js-obj-intro.html)
>
> [JavaScript 对象 - MDN](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects)

#### 要点

* 在 JavaScript中，几乎所有的事物都是对象，如 var car = "Fiat"
* 对象也是一个变量，但对象可以包含多个值
  * 包含多个值的特性使JavaScript 对象也被称为键值对的容器
  *  键值对在 JavaScript 对象通常称为 **对象属性**
* [对象属性名不加引号与加引号的区别](https://www.cnblogs.com/swwag/p/7474649.html)
* 对象的创建方式，[JavaScript创建对象的七种方式](https://xxxgitone.github.io/2017/06/10/JavaScript%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1%E7%9A%84%E4%B8%83%E7%A7%8D%E6%96%B9%E5%BC%8F/)
  * 字面量
    * 简单，直接，一目了然
  * 构造方法
  * 使用ES5中的Object.create\( \)
    * 老版本浏览器可能会存在兼容性问题

```javascript
{
    'name' : 'tom'
    'age' : 4
}

// 对象需要通过赋值给变量来使用
// 字面量的创建方式
var cat {
    'name' : 'tom'
    'age' : 4
    'family' : ['father','mom']
    'speak' : function () {
        console.log('(>^ω^<)')
    },
    'friend' : {
        'name' : 'Jerry'
        'age' : 4
    }
}

// 构造方法的创建方式
var cat = new Object() 
// 相当于
var cat = {}



```

#### 对象的使用

* 赋值

```javascript
cat.name = 'Tim'
cat['name'] = 'Tim'

// 创建新的属性并赋值
cat.type = '加菲猫'
```

* 读取

```javascript
console.log(cat.name)
console.log(cat['name'])
```

* 删除
  * [delete 操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)

```javascript
delete cat.type
delete cat['type']
```

* 检测
  * [in 运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in)

```javascript
console.log('name' in cat)
```

* 枚举
  * [ `for...in`语句](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)

```javascript
for (var p in cat) {
    console.log(p) // 遍历属性名
    console.log(cat[p]) // 遍历属性值：会将p的值计算出，然后到cat对象中查找
}
```

### 函数介绍

> [函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块](https://www.runoob.com/js/js-functions.html)
>
> [JavaScript 函数定义 - 菜鸟教程](https://www.runoob.com/js/js-function-definition.html)
>
> [函数 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/function)
>
> [JavaScript函数的属性和方法](https://baijiahao.baidu.com/s?id=1627803653383833202&wfr=spider&for=pc)

#### 要点

* 一次封装（定义），四处使用
* 只有将函数作为对象，才能发挥全部特性
* return 的两种含义
  * 1.停止执行
  * 2.返回后面的值
* 函数的定义与调用
  * 定义
    * 封装代码
      * 什么都没有发生
  * 调用
    * 创建作用域
      * 传参
      * 执行代码
    * 销毁作用域
      * 销毁所有局部变量
* 对象中的函数被称为方法

#### 函数的二象性

1. 可以调用
2. 函数是对象

## 

### **函数与对象**

* 相同的定义方式
  * 定义对象的两种方式
    * 字面量 ｛｝
    * 构造函数 new Object\( \)
  * 定义函数的两种方式
    * 字面量 function add\(num1,num2\){ }
    * 构造函数 new Function\('num1','num2','...'\)
* 都可以添加属性和方法
  * 对象添加属性和方法
    * var person ={ }
    * person.name = 'xm'
    * person.setName = function \(name\) { this.name =name }
  * 函数添加属性和方法
    * function add \(num1,num2\) { return num1+num2 }
    * add.sex = 'male'
    * add.setSex = function \(sex\) { this.sex = sex }

```javascript
function add (num1,num2) { 
    return num1+num2 
}

add.sex = 'male'

add.setSex = function (sex) {
    this.sex = sex
}

console.log(add.sex) // male
console.log(add.setSex('female')) // undefined 因为没有return
console.log(add.sex) // female 因为被上面的setSex更改了
console.log(add(1,2))
```

* 都可以作为数据值使用
  * 对象与函数归根结底都是数据值
  * 数据保存在内存中，对象与函数都保存在堆内存中（大小不固定）
  * 对象与函数都需要一个变量来找到并引用\(调用\)它

```javascript
var person = {}
var add = function () { // 在此声明的函数名在局部作用域中，如在内部不使用，可以用匿名函数声明
    return 1
}
console.log(add()) // 1
console.log(add) // function () 函数本体


// 数组
[{},function () { // 可以命名，也可以通过数组下标来访问

}]

// 对象
{
    family:{},
    setName:fucntion (argument){
    
    }
}
```

* 都可以作为参数使用

```javascript
// 定时函数，第一个参数为函数，第二个参数为定时的毫秒数
setTimeout(function(){
    console.log(1)
},1000)

setTimeout(fn,1000) //不加（），传递的是函数本体，加（）是执行函数
function fn () {
    console.log(1)
}
```

* 都可以作为返回值

```javascript
function fn () {
    return function () { // 如增加函数名，因其在局部作用域中，所以只能在内部调用
        console.log(1)
    }
}

var newFn = fn() // 没有调用，只是把fn()的返回结果赋值给了newFn，所以无值输出
newFn() // 输出1
fn()() // 输出1
```

## 

### 函数的定义方式及区别

> 定义方式：字面量、构造函数

#### 要点

* 使用 function声明 要注意 **声明提前** 的问题
  * 声明提前：在预解析时，使用function关键字声明的函数会被提前声明
  * 声明提前有什么用？
    * 先执行，后声明的方式可以正常解读

#### 字面量的定义方式

* function 声明

```javascript
// 声明
function add () {

}
// 调用
add()
```

* var 赋值表达式

```javascript
// 声明
var add = function () {

}
// 调用
add()
```

#### 构造函数的定义方式

* new

```javascript
// 声明
// 参数及函数体都必须以字符串的形式传入
var add = new Function('num1','num2','return num1 + num2')

// 调用
add()
```

#### 区别

|  | function声明 | var 赋值表达式 | new |
| :--- | :--- | :--- | :--- |
| 声明方式 | 字面量 | 字面量 | 构造函数 |
| 参数 | 使用变量传递 | 使用变量传递 | 使用字符串传递 |
| 预解析 | 可先执行 | 不可先执行 | 只能后执行 |
| 使用优先级 | 高 | 高 | 低 |

* 声明方式
  * 字面量声明的方式更直观、简洁、方便书写
* 参数
  * 使用字符串传递时，首先要解析字符串，然后实例化构造函数，要比使用变量传递的效率低
* 预解析
  * 使用function声明方式，先执行与后执行的结果一致（声明提前）
  * 使用var 赋值表达式方式，不能先执行

```javascript
// 先声明，后定义
function add () {
    return 1
}
console.log(add()) // 1

// 先执行，再声明

console.log(add()) // 1
function add () {
    return 1
}                  

```

```javascript
// 先赋值，后调用
var add = function () {
    return 1
}
console.log(add()) // 1 

// 先调用，后赋值 
console.log(add()) // 报错, not a function
var add = function () { //在预解析时，由于是赋值语句，只会执行var赋值，不会提前定义function
    return 1
}


// 预解析
// 1.先寻找var 及 function
// 2.var赋值undefined，function提前定义
```

### 函数定义的位置

#### 全局作用域中定义

* 可以访问区域
  * 任何位置

```javascript
//全局作用域可访问
add()            // 声明前可访问
function add () {
    add()        // 内部可访问
}
add()            // 声明后可访问

// 局部作用域可访问
function subtract(argument){
    add()        // 局部作用域可访问
}


```

#### 局部作用域（函数作用域）中定义

* 仅作用域链的同层、外层可以访问

```javascript
fn() // 访问不到

function add () {
    fn()            // 可以访问
    function fn () {
        fn()        // 可以访问
        function fn3 () {
            fn()    // 可以访问
        }
    }
    function fn2 () {
        fn()        // 可以访问
    }
}


```

#### 代码块中的定义

* JS中无块级作用域
* 尽量不在if代码块中声明函数，无实际if，else效果

```javascript
// 相当于在全局作用域中解析，不管是true还是false，add()与 subtract()都会提前声明
if (true) {
    function add () {    // 可以执行
    
    }
}else{
    function subtract () {    // 可以执行
    
    }
}

// 在全局作用域中预解析，var赋值undefined，逐行解读代码时，因为条件是true，else中的代码不会执行
if (true) {
    var add = function () {    // 可以执行
    
    }
}else{
    var subtract = function () {    // 不会执行，此时subtract为undefined
    
    }
}
```

#### 对象中的函数定义

* 对象中的函数被称为方法

```javascript
var person = {
    name:'xm'
    setSex:function (sex) {
        this.sex = sex
    }
}

person.setName= function (name) {
    this.name = name
}

setSex()   // 报错，setSex不在全局作用域中，必须要提现其拥有对象
person.setSex() // 正确调用

```

## 

### 函数的调用 - 普通函数

> 匿名函数从定义到调用，称为匿名函数的自执行

* 命名函数的调用
* 匿名函数的调用
  * 变量赋值调用
    * 函数名代表函数本体,\(\)为调用执行
  * 直接调用
    * 调用方式与变量赋值原理一致，但使用function关键字开头会引起解析器只认为是函数的声明，不会执行，所以需要将执行之后的结果赋值给一个变量，或使用\(\)、增加操作符、在函数中调用
      * 核心思维为规避function关键字开头

```javascript
// 一般情况的调用
add(1,2) 

// 普通函数的调用
// 命名函数
function add () {

}
add() // 调用

// 匿名函数
// 1.赋值给变量调用
var add = funciton () {

}
add() // 调用

// 2.1 直接调用
var add = function () {
    console.log(1)
}() // 调用，这种方式会使函数在定义时就直接执行，称之为自我执行的匿名函数

// 2.2.1 直接调用
(function () {
    console.log(1)
})() // 函数也是一个对象or数据值，所以可以使用()

// 2.2.2 直接调用
(function () {
    console.log(1)
}()) // 与2.2.1的区别为执行完毕再包装上()，效果一致

// 2.2.3 直接调用
！+-~function () { // 均为合法操作符，可以正确执行
    console.log(1)
}() 

// 2.2.4 直接调用
console.log(function () {
    return 1
}())

```

#### 递归调用

> [什么是递归?先了解什么是递归](https://www.cnblogs.com/Pushy/p/8455862.html)

```javascript
//递归函数
function factorial (num) {
    if (num <= 1) return 1
    return num * factorial(num-1)
}
console.log(factorial(5))
```

## 

### 函数的调用 - 方法的调用

#### 方法如何调用

```javascript
var operation = {
    add:funtion (num1,num2) {
        return num1 + num2
    },
    subtract:funtion (num1,num2) {
        return num1 - num2
    }
}

operation.add(1,1)


doucment.onclick = function () {
    console.log('你点击了文档！')    // 浏览器自动调用
}
doncment.onclick()    // 手动调用执行，可以用来模拟鼠标点击
```

#### 方法定义规则

* 引号的使用
  * 合法的标识符可以不加引号（子母、数字、下划线、$，并且不以数字开头）

```javascript
var operation = {
    // 合法
    add:funtion (num1,num2) {
        return num1 + num2
    },
    // 合法
    subtract:funtion (num1,num2) {
        return num1 - num2
    },
    // 不合法
    @:funtion () {
        console.log('@') // 报错
    },
    // 更改为
    '@':funtion () {
        console.log('@') // 正常输出
    },    
}
```

#### 方法的一般调用

```javascript
var operation = {
    // 合法
    add:funtion (num1,num2) {
        return num1 + num2
    },
    // 合法
    subtract:funtion (num1,num2) {
        return num1 - num2
    },
    // 不合法
    @:funtion () {
        console.log('@') // 报错
    },
    // 更改为
    '@':funtion () {
        console.log('@') // 正常输出
    },    
}

// 合法命名调用
console.log(operation.add(1,2))

// 非法命名调用
console.log(operation['@'](1,2))

// 变量调用
var key = 'add'
console.log(operation.key(1,2)) // 报错
console.log(operation[key](1,2))
```

#### 方法的链式调用

* 方法可以链式调用
  * 原理：前面的函数调用之后，返回对象本身
* **需要注意使用场景**

```javascript
$('p').html('段落').css('background-color','red')......    // 方法的链式操作
// 优势：简洁，直观
```

```javascript
var operation = {
    // 合法
    add:funtion (num1,num2) {
        console.log(num1 + num2)
        return this    // 指代operation
    },
    // 合法
    subtract:funtion (num1,num2) {
        console.log(num1 - num2)
        return this
    },
    // 不合法
    @:funtion () {
        console.log('@') // 报错
    },
    // 更改为
    '@':funtion () {
        console.log('@') // 正常输出
    },    
}

// 链式调用
operation.add(1,2).subtract(2,1) 
```

## 

### 函数的调用 - 构造函数的调用

#### 构造函数

> [通过构造函数来实例化对象的意义是什么？](https://www.zhihu.com/question/333812657)

* 构造函数与普通函数的区别
  * 调用
    * add\( \)
    * new Person\( \)
  * 返回值
    * 普通函数调用后有返回值，如没有return，返回undefined
    * 构造函数返回的是对象

```javascript
// 普通函数
add()

// 构造函数
new Person()
```

* js中的内置构造函数
  * Object\( \)
  * Array\( \)
* 构造函数一般会首字母大写，以区分一般函数

### 函数的调用 - 间接调用

> 普通函数、方法、构造函数的调用均为直接调用

* 间接调用：通过call\( \)、apply\( \)
  * 每一个函数下面都有call\( \)及apply\( \)
* 为什么需要call\( \)、apply\( \)
  * 可以继承父类的一些属性及方法
  * **可以借用其他对象的一些方法**
  * 可以判断数据类型
    * 在typeof、instanceof不足以应对的场景
      * typeof只能判断基本类型
      * instanceof返回的是布尔值
      * call\( \)、apply\( \)可以明确返回数据类型的名称
* call\( \)的参数
  * 第一个参数，改变this指向
  * 后续参数，传递的数据
* apply\( \)的参数

  * 第一个参数，改变this指向
  * 后续参数，传递的数据\(数组形式\)

```javascript
function add () {

}j
add()    // 直接调用

var name = 'xm'
var person = {}
person.name = 'xh'
person.getName = function () {
    return this.name
}
cosole.log(person.getName())    // 直接调用，输出xh
cosole.log(person.getName.call(window)) // 间接调用，改变this指向后，输出xm
cosole.log(person.getName.apply(window)) // 一个参数时，作用与call()一致

// call()，apply()区别
function add (num1,num2) {
    return num1 + num2
}
console.log(add(1,2))
console.log(add.call(window,1,2))
console.log(add.apply(window,[1,2]))

// 改变this指向,应用场景
function add (num1,num2) {
    return num1 + num2
}
var datas = [1,2]    // 返回值是数组时，可避免循环遍历取出传递
console.log(add.apply(window,datas))
```

## 

### 参数的类型

* 形参（形式参数）：在函数定义时，所期望接收的参数
  * 形参是一个占位符，等待被真正传入的参数所替换，无实际意义
* 实参（实际参数）：实际传递时的参数
  * 替换形参进行真正的逻辑处理

```javascript
function add(num1,num2){    // 形参
    return num1 + num2
}
add(1,2)    // 实参
```

* 参数传递的本质
  * ​将实参赋值给形参
    * 基本数据类型，赋值相当于拷贝副本
      * 修改实参，形参不会受到影响
    * 引用数据类型，赋值是堆内存中的地址
      * 修改实参，形参会受到影响

```javascript
var person = {}
function setPerson (obj) {
    obj.name = 'xm'
}
setPerson(person)
```

### 参数的个数

* 实参个数与形参个数相等时
* 实参个数小于形参个数时
  * 场景：参数传递错误；可选参数
* 实参个数大于形参格式时
  * 场景：参数传递错误；不限制参数
  * 使用arguments对象
    * argunments实际是一个类数组，保存着实参的值

```javascript
// 实参个数与形参个数相等时
function add(num1,num2){    // 形参
    return num1 + num2
}
add(1,2)    // 实参

// 实参个数小于形参个数时
add(1) // num1 =1 num2 =undefined 遵循预解析规则

// 可选参数，原始场景
function pow (base,power) {
    return Math.pow(base,power)
}
console.log(pow(3,2))

// 可选参数，更改场景，使幂数在未传递时默认为2，传递时为实际参数
function pow (base,power) {
    //if (!power) power = 2 // 简写
    power = power || 2    // 短路操作
    return Math.pow(base,power)
}
console.log(pow(3))


// 实参个数大于形参格式时，原始场景
function add(num1,num2){    // 形参
    return num1 + num2
}
add(1,2,3,4,5)    // 实参

// 实参个数大于形参格式时，更改场景，使参数的个数不受限制，函数可以接收任意多的值
function add(){    // 形参
    if(arguments.length == 0) return
    var sum = 0
    for (var i = 0; i < arguments.length; i++){
        sum += arguments[i]
    }
    return sum
}
console.log(add(1,2,3,4,5))    // 实参
```

### arguments

> [ **`arguments`** 是一个对应于传递给函数的参数的类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)

* 每一个函数都有
* 存在于局部作用域中
* arguments是一个类数组
  * 类数组：不是真正的数组，类似数组
  * 类数组是一个对象

```javascript
// arguments 内部结构
{
    '0':1,
    '1':2,
    '2':3,
    '3':4,
    lenght:4
}
```

* arguments中的每一个数据与形式参数一一对应
  * arguments与形参均指向同一个值（非拷贝数据副本，而是使用别名）

```javascript
// 原始
function fn (name) {
    console.log(name)
}
fn('xm')    // 返回xm

// 修改
function fn (name) {
    arguments[0] = ''
    console.log(name)
}
fn('xm')    // 返回''
```

* arguments是每一个函数中所独有的，存在于独立的局部作用域中，并且不可以垮函数

```javascript
function fn () {
    console.log(arguments)    // 1
    function fn2 () {
        console.log(arguments)    // 2
    }
    fn2(2)
}
fn(1)
```

* arguments.callee属性
  * 作用：指代函数本身
  * **严格模式下不允许使用**

```javascript
function add(num1,num2){    // 形参
    console.log(arguments.callee)    // add(num1,num2)
    return num1 + num2
}
add(1,2)    // 实参

// 在递归中的应用
// 原始
function factorial (num) {
    if (num <= 1) return 1
    return num * factorial(num - 1)
}

// 更改
function factorial (num) {
    if (num <= 1) return 1
    return num * arguments.callee(num - 1)
}

// 严格模式下
var factorial = function fn(num) {    // 更改var的名称不会受到影响
    if (num <= 1) return 1
    return num * fn(num - 1)
}

//控制实参的个数与形参一致
function add(num1,num2){
    if(arguments.length != add.length)        // add.length属性可以获取形参的个数
    throw new Error('请传入' + add.length + '个参数') // 主动抛出异常
    return num1 + num2                 
}
add(1,2) 
```

## 

### 什么可以作为参数

> 参数就是数据值

* 无参数
* 基本数据类型作为参数
  * 注意布尔值作为参数的问题
  * undefined作为参数
    * 场景：未传入；设计不合理
  * null作为参数
* 引用数据类型作为参数
  * 数组作为参数
  * 对象作为参数
  * 函数作为参数

```javascript
// 1.1无参数
function fn () {

}

// 1.2无参数
function fn2 () {
    var num = 1
    function fn2 () {    // 通过作用域链，可以找到fn()下的变量
        console.log(num)
    }
}

// 2.传入数字
function add (num1,num2) {
    return num1 + num2
}
add(1,1)

// 3.传入字符串
$('p') // JQuery 选择DOM节点

// 4.传入布尔值 （不推荐），函数应该专属于解决一件事，下述函数可分成两个函数
function fn (boon) {
    if (bool) {
    
    }else{
    
    }
}

// 5.1 传入undefined（未传入）
function add (num1,num2) {
    return num1 + num2
}
add(1)    // 未传入值，则在预解析时赋值undefined

// 5.2 传入undefined（设计不合理）
function pow (power,base) {
    power = power || 2
    return Math.pow(base,power)
}
cosole.log(undefined,3) // 此时要么传入2，要么传入undefined

// 6.传入null
add(a,null)

// 7.传入数组
$.each([1,2,3],function (index,item) {
    console.log(index)
    console.log(item)
})

// 8.传入对象
$.each({name:'xm',sex:'male'},function (index,item) {
    console.log(index)
    console.log(item)
})

// 9.传入函数
$.each({name:'xm',sex:'male'},function (index,item) {
    console.log(index)
    console.log(item)
})
```

#### 函数设计技巧 - 使用对象作为参数

* 参数数量在3个及3个以上时，可以考虑使用对象作为参数
* 更改需求
  * 场景：参数过多时，传入参数的顺序及传入的内容
  * 解决方案：使用对象

```javascript
// 原始
function setPerson (name,sex) {
    var persion = {}
    person.name = name
    person.sex = sex
}
setPerson('xm','male')

// 更改需求
function setPerson (name,sex,age,tel,addr) {
    var persion = {}
    person.name = name
    person.sex = sex
    person.age = age
    person.tel = tel
    person.addr = addr 
}
setPerson('xm','male',18,'182...','中国China')

// 使用对象
function setPerson (obj) {
    var persion = {}
    person.name = obj.name || 'xh'
    person.sex = obj.sex || 'male'
    person.age = obj.age || '18'
    person.tel = obj.tel || '110'
    person.addr = obj.addr  || 'China'
}
setPerson({
    name:'xm',
    age:'18',
    addr:'China'
    sex:'male'
})
```

## 

### return、continue、break

#### return

* 在函数中使用
* 表示在函数中返回值

#### continue

* 用在循环中
* 表示跳出本次循环
  * 接着下一次循环，并非跳出整个循环

```javascript
for (var i = 0; i < 10; i ++) {
    if (i == 4) continue
}
```

#### break

* 用在循环中
* 表示跳出整个循环
  * 执行循环外的语句

```javascript
for (var i = 0; i < 10; i ++) {
    if (i == 4) break
}
```

### 什么可以作为返回值

* 无返回值
  * 1.1与1.2在返回值层面作用是一致的
  * 1.1中，return还表示函数到此终止，可以用于提前退出函数
* 返回undefined
  * 1.1与1.2相当于返回undefined
* 数字作为返回值
* 字符串作为返回值
* 布尔值作为返回值
  * 应用场景：表单验证
* null作为返回值
* 数组作为返回值
* 对象作为返回值
* 函数作为返回值

```javascript
// 1.1无返回值
function fn () {
    return
}

// 1.2无返回值
function fn () {

}

// 2.返回undefined
function fn () {
    return undefined
}

// 3.数字作为返回值
function add () {
    return 1
}

// 4.字符串作为返回值
return '1'
alert('1,2,3')
alert([1,2,3]) // 默认执行toString() 强制转换为字符串

// 5.布尔值作为返回值
return true/false

// 6.null作为返回值
return null

// 7.数组作为返回值
// 原始
function add (num1,num2) {
    return num1 + num2
}

// 更改
function add (num1,num2) {
    return [num1 + num2, num1, num2] // 返回结果、相加的具体数值
}

// 8.对象作为返回值
function getPerson () {
    return {    // 如果左花括号写在下一行，JS解析器会默认在此处添加一个;
        name:'xm',
        age:18
    }
}

// 9.函数作为返回值
function fn () {
    return function fn2 () {
    
    }
}
// 直接调用
fn()()
// 赋值调用
var newFn = fn()
newFn()
```

## 面向对象（OOP）

> 面向对象是对代码的一种抽象，对外统一提供调用接口的编程思想
>
> 基于原型的面向对象方式中，对象（Object）是依靠构造器（constructor）构造出来的

### 面向对象概述

* 属性：事物的特性
  * 自身所拥有的东西，如：人拥有名字、年龄、性别
* 方法：事物的功能
  * 如：人会学习、玩耍、唱歌
* 对象：事物的一个实例
  * 如：众多人中的一个人
* 原型：JS函数中由prototype属性引用了一个对象，既原型对象（原型）
* Object：JavaScript中所有的自定义函数及面向对象都继承于它

```javascript
alert(F.prototype)    // prototpye是一个原型，在内存中它指向一个地址，地址中存储了一个对象
alert(F.prototype instanceof Object)    // Objects是javaScript中的父对象
```

#### 对象的创建方式

* 使用函数构造器，构造出一个对象
  * 构造器构造的对象，效率较低
  * 传递给函数构造器的数据，都会被当做生成函数的变量的参数
    * 作为参数的数据，不能改变其顺序

```javascript
// 构造函数对象
var obj = new Function(var1,var2...,functionBody()) // 自定义函数可以使用前面的变量值
```

* 以函数的方式调用函数构造器，定义的对象，首先执行的是自定义函数，再执行创建对象

```javascript
var obj = new Function('a','b','return a + b')
var s = obj(2,5)
console.log(s)    // 7
```

* 对象分为函数对象及普通对象，凡是通过new Function\(\)创建的对象，都是函数对象，其他的都是普通对象

### 闭包

> 闭包是一个拥有许多变量和绑定了这些变量的环境的表达式（通常是一个函数）
>
> [JavaScript 闭包 \_ 菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

#### 要点

* javascript中，函数内部可以直接读取全局变量

#### 闭包的作用

* 可以使得函数拥有私有变量
* 闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。
* 直观的说就是形成一个不销毁的栈环境。

#### 闭包的实际应用

* 读取函数内部变量
* 让内部变量的值保留在内存中

```javascript
function a () {
    var i = 0
    function () {
        alert (++i) // 让i的值保留在内存中
    }
    return b
}

var c = a()
c() // 1
```

```javascript
function f1 () {
    var n = 999
    nAdd = function () {
        n = n + 1
    }
    function f2 () {
        alert(n)
    }
    return f2
}
var rs = f1()
rs() // 999
nAdd() // 执行
rs() // 1000
```

#### 闭包的优点

* 有利于封装
  * 当闭包函数作为另一个函数的调用时，封装性会比较强
* 可以访问局部变量

#### 闭包的缺点

> 闭包需谨慎使用

* 内存占用严重，容易产生内存泄漏
  * 局部变量一直存在于内存中

## 

### 声明对象的方式

> [JavaScript创建对象的七种方式](https://xxxgitone.github.io/2017/06/10/JavaScript%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1%E7%9A%84%E4%B8%83%E7%A7%8D%E6%96%B9%E5%BC%8F/)
>
> [JavaScript 创建对象的 7 种方法](https://juejin.im/entry/58291447128fe1005cd41c52)

* 字面量

```javascript
var person = {
    name : 'zhangsan',
    age : 26,
    sex : 'man',
    eat : function (fds) {
        console.log('我在吃' + fds)
    }
}
```

* new Object\(\)
  * Object是所有对象的基类、根，所有javascript对象都是由Object延伸的

```javascript
var box = new Object()
box.name = 'zhangsan'
box.age = 100
box.infos = fucntion (str) {
    return this.name + "---" + this.age + "---" + str    // this 代表当前对象
}
```

* 构造方法声明对象
  * 函数内部只能使用this访问内部属性或方法

```javascript
function person (name,sex,age) {
    this.name = name    // this.name是属性，name是参数
    this.sex = sex
    this.age = age
    this.show = function () {
        console.log(this.name)
    }
}

var obj1 = new person('zhangsan','nan',18)
console.log(obj1.name)
```

* 工厂模式
  *  按照某种模式，不断的创造对象
  * 工厂模式在调用时，不需要使用new，因其内部已经使用new Object\( \)
  * 工程模式下（任何模式下），同种模式中的创造出来的对象都是独立存在的

```javascript
function createObject (name,age) {
    var obj = new Object()
    obj.name = name // obj.name是属性，name是参数
    obj.age = age
    obj.run = function () { // 在obj对象中，调用其属性及方法必须使用this
        return this.name + "---" + this.age
    }
    obj.say = function () {
        return "今天天气不错"
    }
    return obj    // *** 必须返回Object本身
}

var box = crerteObject('张三',18)
console.log(box.name)    // 调用属性
console.log(box.run())    //调用方法 
```

#### 构造方法模式与工厂模式的区别

* 构造方法模式不会显示创建对象，需要将属性直接赋值给this，不需要return对象
* 工厂模式必须在内部创建Object对象，并且需要返回Object对象，属性及方法均赋值给Object对象

## 

### 对象的遍历

* 有些对象或集合可以当做数组处理

```javascript
var ren = {}
ren.name = 'zhangsan'
ren.age = '18'
ren.len = '180'
ren.demo = function () {
    console.log(this.name)
}
```

* [for in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)

```javascript
// 在遍历对象时，i的取值是对象所有的属性名称和方法名称
for (var i in ren) {
    console.log(i)
}

// 利用上面一点，可以循环遍历出属性的数值、方法定义的代码
for (var i in ren) {
    console.log(ren[i])
}
```

* 使用构造函数声明的对象要实例化以后才可以进行遍历

```javascript
function ren () {    // 此时的ren是一个方法的名称
    this.name = 'zhangsan'
    this.age = '18'
    this.len = '180'
    this.demo = function () {
        alert(this.name)
    }
}

var r = new ren()
for (var i in r){
    alert(ren[i])
}
```

## 

### 对象的存储

> 对象在内存中的分布

* 栈内存
* 堆内存
* 代码段
* 静态段（数据段）
* 对象都是一个引用
  * 引到的是一个16进制的地址
  * 地址上描述的是对象中的属性和方法
  * 方法中的内容定义在代码段中
* 在调用或创建对象时
  * 寻找属性 → 堆内存
  * 调用方法 → 先在堆内存中找到方法名称 → 再到代码段中寻找方法中的数据

## 

### 封装

> 封装（Encapsulation）：把对象内部数据和操作细节进行隐藏
>
> 大多面向对象的语言都支持封装的特性，提供了private关键字来隐藏某些属性或方法，用来限制被封装的数据或者内容的访问，只对外提供一个对象的专门访问的接口
>
> 接口一般为调用方法
>
> JS中没有提供专门封装的关键字，但可以使用闭包来实现封装

* 函数内部声明的变量，外部是访问不到的
* 共有与私有内存的区别是：能否在对象外部被访问

```javascript
// 封装1.
function demo () {
    var n = 1    // 局部变量，在方法外部不能直接访问
    function test () {    // 外部调用的出口
        n ++
    }
    test()
    return n
}

demo() // 2

// 封装 完整版
function demo () {
    var n = 1
    function test () {
        return n ++
    }
    return test
}
alert(demo()) // 返回test()

var at = demo()
alert(at())

// test()的另一种写法
this.test = function () {
    return ++ n
}
```

* 函数的作用域在内部无法被外部直接访问，但是在函数方法作用域内，如果有其他的function（上述代码中的test），可以访问到其局部变量（上述代码中的n），用test可以当做中转站，使n可以在外部访问到，因此test\( \)也被称为特权方法，使用这种方法在面向对象中创建的内容具有真正的封装的意义

```javascript
// 封装2.
function A(){
    function _xx(){
        alert(11)
    }
    this.xx = function () {
            return _xx 
    }
}

A.prototype = {    // 原型的方式
    oth : function () {
        console.log('普通方法')
    }
}

var a = new A()
console.log(a.xx())

var b = a.xx()    // a.xx() = function _xx
b()
```

* 封装2.与封装1.的区别
  * 封装2.为构造加原型的混合方式
  * 封装2.在每次生成新的对象时（上述 var a），对象内部每次都要通过this.xx来创建其属性和方法，通过调用的步骤要比封装1.多一步，这种情况不利于继承，而且每次调用都会占用内存

### 原型继承

> 通过原型和原型链引出继承的概念
>
> [显式原型和隐式原型的联系](https://www.cnblogs.com/liubinghaoJavaScript/p/7478432.html)

#### 要点

* prototype是对象
* \_proto\_是属性

#### 原型

* 是利用prototype对象添加属性和方法

#### 原型链

* JS在创建对象（不论是普通对象还是函数对象）的时候
* 都有一个叫做\_\_proto\_\_的内置属性
* 用于指向创建它的函数对象的原型对象prototype

```javascript
// 原型：用prototype对象来添加属性和方法
var person = function () {}
var p = new person()    // 实例化，可以拆分为三个阶段来实现
console.log(person.prorotype instanceof Object) // true 证明person.prototype是object
console.log(p.__proto__ instanceof Object) // true
console.log(p.__proto__ instanceof person.prototype) // true

// 阶段1.
var p = {} // 创建对象
// 阶段2.
p.__proto__ = person.prototype    // __proto__是对象自带的一个属性
// 阶段3. 初始化对象(p)
person.call(p)
```

```javascript
var person = function () {
    this.name = 'zhangsan'
}
var p = new person()   

p.name // 当p中不存在此属性，就会去链式查找
       // 先到person.__proto__中查找，相当于p.__proto__
       // 因p.__proto__ == Object == person.prototype,每个Object都有_proto__属性
       // 如p.__proto__中找不到就会继续向外查找，p.__proto__.__proto__

// 对象的隐式原型指向构造该对象的构造函数的显式原型 
// 对象的隐式原型：p.__proto__
// 构造该对象的构造函数：var person = function (){}      
// 显式原型：prototype
// 也就是p.__proto__ →  person.prototype
```

```javascript
var person = function () {
    
}
person.prototype.say = function () {
    console.log('天气很好')
}

var p = new person() // p.__proto__ = person.prototype
p.say() 
```

```javascript
var person = function () {
    
}
person.prototype.say = function () {
    console.log('天气很好')
}
person.prototype.gonzi = 500


var programmer = function () {}
programmer.prototype = new person() 
programmer.prototype.wcd = function () { 
    console.log('明天天气也不错') 
}
programmer.prototype.gongzi = 1000 // 同名方法，子方法会覆盖父方法


var p = new programmer() // p.__proto__ = programmer.prototype = new person()
p.say() // 天气很好

// 原型链的实现过程
// programmer.prototype = new person() 
// 相当于 
// 1. var p1 = new person()
// 2. programmer.prototype = p1
// p.say()时 
// p.__proto__ → programmer.prototype == p1 → 
// → p1.__proto__ == person.prototype.say()
```

```javascript
// 原型继承
function person (name,age) {
    this.name = name
    this.age = age
}
person.prototype.sayhello = function () {
    console.log('属性name值' + this.name)
}

var per = new person('zhangsan',20)
per.sayhello()

function studene () {}
student.prototype = new person('李四',18) // 原型继承
student.prototype.grade = 3
student.prototype.test = function () {
    console.log(this.grade)
}
var s = new student()
s.sayhello()

// 过程分析
// s.sayhello() → s下无sayhello()方法 → s.__proto__ = student.prototype
// student.prototype = p1 → p1.__proto__ = person.prototype
```

### 构造继承

> 在子类内部构造父类的对象，实现继承

* 构造函数的继承是在对象内部创建父对象的对象
  * 父对象被子对象继承后，所有的属性和方法，都将传递到子对象中去

```javascript
function parents (name) {
    this.name = name
    this.say = function () {
        console.log('父亲的名字：' + this.name)
    }
}

function child (name,age) { // 继承parents
    //this.pObj = parents(name) // 方式1. 子对象的参数name传递到父对象中
    this.pObj = parents()    // 方式2. 子对象的参数name传递到父对象中
    this.pObj(name)
    this.age = age 
    this.sayC = function () {
        console.log('child：' + this.name)
    }
    
}
// 调用父对象
var p = new parents('zhangsan')
p.say()

// 调用子对象
var c = new child('李四',20)
c.sayC()
// 子对象执行流程
// this.pObj(name) → parents(name) → this.name = name // 李四
// this.sayC → this.name → parents/this.name    // 李四
```

### call和apply的用法

* call：调用一个对象的方法，以另一个对象替换当前对象
  * obj.call\(方法,var1,var2,var3...\)
* apply：应用某一对象的一个方法，用另一个对象替换当前对象
  * obj.apply\(方法,\[var1,var2,var3...\]\)

```javascript
function person (name,age,len) {
    this.name = name
    this.age = age
    this.len = len
    this.say = function () {
        console.log(this.name + ':' + this.age + ':' + this.len)
    }
}

// call继承
function student (name,age) {
    person.call(this,name,age)
}

// 父对象
var per = new person('张三',25,'170')
per.say
// 子对象
var stu = new student('李四',18)
stu.stu
```

```javascript
function person (name,age,len) {
    this.name = name
    this.age = age
    this.len = len
    this.say = function () {
        console.log(this.name + ':' + this.age + ':' + this.len)
    }
}

// apply继承
function teacher(name,age,len) {
    person.apply(this,[name,age,len])
}

// 父对象
var tea = new teacher('王五',20,'180')
tea.say()
```

### 对象冒充

> 将父类的属性和方法一起传给子类作为特权属性和特权方法

```javascript
function person(name,age){
    this.name = name
    this.age = age
    this.sayHi = function () {
        alert('hi')
    }
}

person.prototype.walk = function () {
    console.log('walk.....')
}

// 对象冒充
function sudent (name,age,grade) {
    this.newMethod = person // 冒充person对象,传递特权属性和特权方法给子类
    this.newMethod(name,age)
    this.grade = grade
}

var s1 = new student('张三',15,5)

console.log(s1.name)
```

### 关键字

* instanceof：变量是否是对象的实例
* delete：删除对象的属性
  * 不能删除方法
  * 不能删除变量
  * 不能删除原型链中的属性
* call、apply

```javascript
function add (a,b) {
    console.log(a + b)
}
function subs (a,b) {
    console.lgo(a - b)
}
add.call(subs,5,3) // 8 subs 替换成了 add，此处只能引用已经存在的对象

add.apply(subs,[5,3])
```

* callee：返回正在执行的function对象
* arguments：引用函数的参数，如果是表示参数，可以使用for in 遍历




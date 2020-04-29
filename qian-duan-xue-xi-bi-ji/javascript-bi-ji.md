# JavaScript 笔记

## 闭包

> [JavaScript 闭包 \_ 菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

### 闭包

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
//输出undefined
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

### JQuery中的window

* 把window作为一个参数传入函数中
  * 传入后变为局部变量，执行速度会更快
  * 方便压缩代码


# JavaScript 笔记



### Js内置对象

#### Array

1.构造函数 2.字面量 3.数组的栈方法 - push - unshift - pop - shift ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-05-25-39-973_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-05-31-57-178_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-05-34-08-263_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-05-34-17-691_com.baidu.netdisk.jpg)

4.数组的转换方法 - join ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-05-37-47-365_com.baidu.netdisk.jpg)

5.数组重排序方法 - reverse - sort sort默认对数组先转换成String，后进行排序， 并且默认比较首位字符。

6.数组的连接方法 - concat ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-30-11-617_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-33-30-677_com.baidu.netdisk.jpg)

7.数组的截取方法 - slice ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-35-02-154_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-36-32-598_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-38-53-661_com.baidu.netdisk.jpg)

面试题 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-47-32-188_com.baidu.netdisk.jpg)

8.数组的自定义位置删除、插入的方法 - splice 删除的index包含被删除的index 插入时的index为插入后所在的index ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-49-26-894_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-06-52-26-300_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-23-12-05-715_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-23-03-03-797_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-23-03-20-776_com.baidu.netdisk.jpg)![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-23-14-02-681_com.baidu.netdisk.jpg)![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-09-23-14-09-590_com.baidu.netdisk.jpg)

9.数组的查找方法 - indexOf 从数组开头向后查找（只检测第一个被查找到的） - lastIndexOf 从数组末尾向前查找（只检测第一个被查找到的） ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-15-30-08-758_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-15-11-773_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-28-03-282_com.baidu.netdisk.jpg)

封装一个方法实现indexOf的功能 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-25-42-577_com.baidu.netdisk.jpg)

#### String

1.字符串的检索方法 -charAt 返回字符本身，找不到会返回空 -chatCodeAt 返回字符编码，找不到会返回空 -indexOf 从头开始检测，返回字符下标，未检测到返 回-1，可用于检测字符串中是否存在某字符或 **字符串** -lastIndexOf 与indexOf功能一致，区别于是从末尾检测 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-47-24-121_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-48-12-927_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-48-30-881_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-10-17-55-56-486_com.baidu.netdisk.jpg)

2.字符串的截取方法 -slice 截取范围需注意end不在范围之内（即不包含），省略end则截取至末尾 -substring 参数为负数时，自动转换为0 -substr len为截取的总数，负数时返回空 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-09-38-04-728_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-09-44-06-832_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-14-24-53-904_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-14-24-46-138_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-14-25-32-577_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-15-33-10-272_com.baidu.netdisk.jpg)

3.字符串的转换方法 -split 转换为数组,参数为分割符，必须填写 -replace 替换字符，只替换第一个所选字符，返回为被替换后的字符 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-15-49-33-308_com.baidu.netdisk.jpg) ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-16-02-10-192_com.baidu.netdisk.jpg)

4.字符串的大小写转换方法 -toUpperCase 返回值为更改后的字符串，不更改原字符串 -toLowerCase 封装一个转换大小的组件 ![](/storage/emulated/0/DCIM/Screenshots/Screenshot_2020-03-11-16-38-05-516_com.baidu.netdisk.jpg)

#### Math对象

1.求最小值最大值 -min 求一组数据中的最小值，如数据中有非数字则返回NaN -max 求一组数据中的最大值，如数据中有非数字则返回NaN 2.取整方法 -ceil 向上取整，返回大于数值的最小整数 -floor 只取整数部分，不比较大小 -round 四舍五入取整 3.求绝对值方法 -abs 常应用于移动端像素坐标 4.random随机数方法 生成的最小值为0，最大数为1

#### Date对象

1.获取方法

2.设置方法 -set方法有自动容错能力 -创建日期对象时，年月日必须设定

### Js错误处理

1.语法错误 

2.运行时错误 

3.语法错误与运行时错误的区别 

4.逻辑错误

## 闭包

> [JavaScript 闭包 \_ 菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

### 闭包

* 可以使得函数拥有私有变量
* 闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。
* 直观的说就是形成一个不销毁的栈环境。

### 全局变量

> [JavaScript 关于全局对象](https://www.cnblogs.com/echo-dauntless/p/9737451.html)

*  变量声明时如果不使用 **var** 关键字，那么它就是一个全局变量，即便它在函数内定义。
* 在web页面中全局变量属于 window 对象

### 变量生命周期

* 全局变量的作用域是全局性的
* 函数内部声明的变量，只在函数内部起作用
* 函数的参数也是局部性的，只在函数内部起作用

### JavaScript 内嵌函数

* 嵌套函数可以访问上一层的函数变量

## JS变量、作用域

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


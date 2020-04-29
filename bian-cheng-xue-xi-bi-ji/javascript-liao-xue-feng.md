---
description: 学习笔记
---

# JavaScript - 廖雪峰

## JavaScript基础

> 变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。
>
> 静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。
>
> 例如Java是静态语言

### **数据类型和变量**

#### [JS中null与undefined的区别](https://blog.csdn.net/weixin_39713762/article/details/93807832)

#### [JS中null与undefined的区别 - 阮一峰](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)

* 相同点
  * if 判断语句中，两者都会被转换为false
* 不同点
  * Number转换的值不同，Number\(null\)输出为0, Number\(undefined\)输出为NaN
* 总结
  * null表示一个值被定义了，但是这个值是空值 作为函数的参数，表示函数的参数不是对象
  * 作为对象原型链的终点（Object.getPrototypeOf\(Object.prototype\)）
  * 定义一个值为null是合理的
  * 但定义为undefined不合理
    * （var name = null） 
    * undefined表示缺少值，即此处应该有值，但是还没有定义变量被声明了还没有赋值，就为undefined
  * 调用函数时应该提供的参数还没有提供，该参数就等于undefined
  * 对象没有赋值的属性，该属性的值就等于undefined
  * 函数没有返回值，默认返回undefined

#### strict模式

*  JavaScript在设计之初，为了方便初学者学习，并不强制要求用`var`申明变量
* 这个设计错误带来了严重的后果
*  如果一个变量没有通过`var`申明就被使用，那么该变量就自动被申明为全局变量

```text
i = 10; // i现在是全局变量
```

* 在同一个页面的不同的JavaScript文件中
  * 如果都不用`var`申明，恰好都使用了变量`i`
  * 将造成变量`i`互相影响，产生难以调试的错误结果。
* 使用`var`申明的变量则不是全局变量
* 它的范围被限制在该变量被申明的函数体内
* 同名变量在不同的函数体内互不冲突。
* 为了修补JavaScript这一严重设计缺陷，ECMA在后续规范中推出了strict模式
* 在strict模式下运行的JavaScript代码，强制通过`var`申明变量
* 未使用`var`申明变量就使用的，将导致运行错误。
* 启用strict模式的方法是在JavaScript代码的第一行写上：

```text
'use strict';

//这是一个字符串

//不支持strict模式的浏览器会把它当做一个字符串语句执行

//支持strict模式的浏览器将开启strict模式运行JavaScript。
```

#### 比较运算符

> 由于JavaScript这个设计缺陷，_不要_使用`==`比较，始终坚持使用`===`比较。

* JavaScript允许对任意数据类型做比较

```text
false == 0; // true
false === 0; // false
```

*  `==`比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果
*  `===`比较，它不会自动转换数据类型，如果数据类型不一致，返回`false`，如果一致，再比较。
*  `NaN`这个特殊的Number与所有其他值都不相等，包括它自己

```text
NaN === NaN; // false
```

* 浮点数的相等比较
  * 这不是JavaScript的设计缺陷。浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小数。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值：

```text
1 / 3 === (1 - 2 / 3); // false
```

**对象**

* JavaScript的对象是一组由键-值组成的无序集合
* JavaScript对象的键都是字符串类型，值可以是任意数据类型

```text
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

*  上述`person`对象一共定义了6个键值对，其中每个键又称为对象的属性，例如，`person`的`name`属性为`'Bob'`
*  要获取一个对象的属性，我们用`对象变量.属性名`的方式

```text
person.name; // 'Bob'
person.zipcode; // null
```

#### 变量

> 变量名也可以用中文，但是，请不要给自己找麻烦。
>
>  同一变量只能用`var`申明一次

* 变量的概念基本上和初中代数的方程变量是一致的
* 只是在计算机程序中，变量不仅可以是数字，还可以是任意数据类型
* 变量在JavaScript中就是用一个变量名表示
  *  变量名是大小写英文、数字、`$`和`_`的组合但不能用数字开头
  *  变量名也不能是JavaScript的关键字，如`if`、`while`
  *  申明一个变量用`var`语句
*  使用等号`=`对变量进行赋值。可以把任意数据类型赋值给变量
  * 同一个变量可以反复赋值
  * 而且可以是不同类型的变量
  *  但是要注意只能用`var`申明一次


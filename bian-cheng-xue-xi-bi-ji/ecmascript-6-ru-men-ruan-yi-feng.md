---
description: 学习笔记
---

# ECMAScript 6 入门 - 阮一峰



##  [let 和 const 命令](https://es6.ruanyifeng.com/#docs/let)

> 1. [let 命令](https://es6.ruanyifeng.com/#docs/let#let%20%E5%91%BD%E4%BB%A4)
> 2. [块级作用域](https://es6.ruanyifeng.com/#docs/let#%E5%9D%97%E7%BA%A7%E4%BD%9C%E7%94%A8%E5%9F%9F)
> 3. [const 命令](https://es6.ruanyifeng.com/#docs/let#const%20%E5%91%BD%E4%BB%A4)
> 4. [顶层对象的属性](https://es6.ruanyifeng.com/#docs/let#%E9%A1%B6%E5%B1%82%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%B1%9E%E6%80%A7)
> 5. [globalThis 对象](https://es6.ruanyifeng.com/#docs/let#globalThis%20%E5%AF%B9%E8%B1%A1)\`\`

### 1.变量提升

*  即变量可以在声明之前使用，值为`undefined`

### 2.暂时性死区

*  只要块级作用域内存在`let`命令
* 它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

```text
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

*  上面代码中，存在全局变量`tmp`
* 但是块级作用域内`let`又声明了一个局部变量`tmp`
* 导致后者绑定这个块级作用域
* 所以在`let`声明变量前，对`tmp`赋值会报错。
*  ES6 明确规定，如果区块中存在`let`和`const`命令
  * 这个区块对这些命令声明的变量，从一开始就形成了封闭作用域
  * 凡是在声明之前就使用这些变量，就会报错。
*  总之，在代码块内，使用`let`命令声明变量之前
* 该变量都是不可用的
* 这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）
  *  “暂时性死区”也意味着`typeof`不再是一个百分之百安全的操作
    *  变量`x`使用`let`命令声明，所以在声明之前
    *  `typeof`运行时就会抛出一个`ReferenceError`
    *  在没有`let`之前，`typeof`运算符是百分之百安全的，永远不会报错
* 这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。
* [了解更多](https://es6.ruanyifeng.com/#docs/let#%E6%9A%82%E6%97%B6%E6%80%A7%E6%AD%BB%E5%8C%BA)

### 3.[为什么需要块级作用域？](https://es6.ruanyifeng.com/#docs/let#%E4%B8%BA%E4%BB%80%E4%B9%88%E9%9C%80%E8%A6%81%E5%9D%97%E7%BA%A7%E4%BD%9C%E7%94%A8%E5%9F%9F%EF%BC%9F)

* 内层变量可能会覆盖外层变量

### 4.[函数能不能在块级作用域之中声明？](https://es6.ruanyifeng.com/#docs/let#%E5%9D%97%E7%BA%A7%E4%BD%9C%E7%94%A8%E5%9F%9F%E4%B8%8E%E5%87%BD%E6%95%B0%E5%A3%B0%E6%98%8E)

### 5.ES6 声明变量的六种方法

* `var`命令
* `function`命令
* `let`命令
* `const`命令
* `import`命令
* `class`命令

### 6.[顶层对象的属性](https://es6.ruanyifeng.com/#docs/let#%E9%A1%B6%E5%B1%82%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%B1%9E%E6%80%A7)

### 7.[globalThis 对象](https://es6.ruanyifeng.com/#docs/let#globalThis-%E5%AF%B9%E8%B1%A1)

* 顶层对象，在浏览器环境指的是`window`对象
* 在 Node 指的是`global`对象
* ES5 之中，顶层对象的属性与全局变量是等价的。

### **重点**

* `let`声明的变量只在它所在的代码块有效
  * `for`循环的计数器，就很合适使用`let`命令
*  `var`命令会发生“变量提升”现象
  *  为了纠正这种现象，`let`命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。
*  `let`不允许在相同作用域内，重复声明同一个变量。
  * 因此，不能在函数内部重新声明参数。
*  `const`声明一个只读的常量。一旦声明，常量的值就不能改变。
  *  这意味着，`const`一旦声明变量，就必须立即初始化，不能留到以后赋值。
*  `const`的作用域与`let`命令相同：只在声明所在的块级作用域内有效。
*  `const`声明的常量，也与`let`一样不可重复声明。
* [const的本质](https://es6.ruanyifeng.com/#docs/let#%E6%9C%AC%E8%B4%A8)

## [变量的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring) <a id="-"></a>

> 1. [数组的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring#%E6%95%B0%E7%BB%84%E7%9A%84%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
> 2. [对象的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring#%E5%AF%B9%E8%B1%A1%E7%9A%84%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
> 3. [字符串的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
> 4. [数值和布尔值的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring#%E6%95%B0%E5%80%BC%E5%92%8C%E5%B8%83%E5%B0%94%E5%80%BC%E7%9A%84%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
> 5. [函数参数的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring#%E5%87%BD%E6%95%B0%E5%8F%82%E6%95%B0%E7%9A%84%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
> 6. [圆括号问题](https://es6.ruanyifeng.com/#docs/destructuring#%E5%9C%86%E6%8B%AC%E5%8F%B7%E9%97%AE%E9%A2%98)
> 7. [用途](https://es6.ruanyifeng.com/#docs/destructuring#%E7%94%A8%E9%80%94)

### [不可遍历的结构](https://es6.ruanyifeng.com/#docs/iterator)

### 解构赋值的用途

*  **交换变量的值**
*  **从函数返回多个值**
*  **函数参数的定义**
*  **提取 JSON 数据**
*  **函数参数的默认值**
*  **遍历 Map 结构**
*  **输入模块的指定方法**

### 重点

* 对象的解构赋值的内部机制
  * 是先找到同名属性
  * 然后再赋给对应的变量
  * 真正被赋值的是后者
  * 而不是前者。
* 如果解构失败，变量的值等于`undefined`
* 对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。
* 与数组一样，解构也可以用于嵌套结构的对象

```javascript
let obj = {
  p: [
    'Hello',
    { y: 'World' }
  ]
};

let { p: [x, { y }] } = obj;
x // "Hello"
y // "World"

// 注意，这时p是模式，不是变量，因此不会被赋值

// 如果p也要作为变量赋值，可以写成下面这样。
```

```javascript
let obj = {
  p: [
    'Hello',
    { y: 'World' }
  ]
};

let { p, p: [x, { y }] } = obj;
x // "Hello"
y // "World"
p // ["Hello", {y: "World"}]

//下面是另一个例子。
```

```javascript
const node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

let { loc, loc: { start }, loc: { start: { line }} } = node;
line // 1
loc  // Object {start: Object}
start // Object {line: 1, column: 5}

// 上面代码有三次解构赋值
// 分别是对loc、start、line三个属性的解构赋值
// 注意，最后一次对line属性的解构赋值之中
// 只有line是变量
// loc和start都是模式，不是变量。
```

```javascript
// 下面是嵌套赋值的例子。

let obj = {};
let arr = [];

({ foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true });

obj // {prop:123}
arr // [true]
```

```javascript
// 如果解构模式是嵌套的对象
// 而且子对象所在的父属性不存在
// 那么将会报错

// 报错
let {foo: {bar}} = {baz: 'baz'};

// 上面代码中，等号左边对象的foo属性，对应一个子对象
// 该子对象的bar属性，解构时会报错
// 原因很简单，因为foo这时等于undefined，再取子属性就会报错。
```

```javascript
// 注意，对象的解构赋值可以取到继承的属性。
const obj1 = {};
const obj2 = { foo: 'bar' };
Object.setPrototypeOf(obj1, obj2);

const { foo } = obj1;
foo // "bar"
// 上面代码中，对象obj1的原型对象是obj2
// foo属性不是obj1自身的属性
// 而是继承自obj2的属性
// 解构赋值可以取到这个属性。
```

* 对象的解构与数组有一个重要的不同。
  * 数组的元素是按次序排列的
    * 变量的取值由它的位置决定
  * 而对象的属性没有次序
    * 变量必须与属性同名，才能取到正确的值。
    * 如果变量名与属性名不一致，必须写成下面这样。

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```

* [对象的解构也可以指定默认值。](https://es6.ruanyifeng.com/#docs/destructuring#%E9%BB%98%E8%AE%A4%E5%80%BC)
  *  默认值生效的条件是，对象的属性值严格等于`undefined`。

```javascript
var {x = 3} = {x: undefined};
x // 3

var {x = 3} = {x: null};
x // null

// 上面代码中，属性x等于null
// 因为null与undefined不严格相等
// 所以是个有效的赋值
// 导致默认值3不会生效。
```

* 字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
* 类似数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值。
* 解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。


# 微信小程序

## 小程序基础

### 数据

* setData
  * setData必须传递的是Js对象，不能是数组等其他
  * setData会引起一次新的数据绑定，导致重新渲染页面，所以不做数据绑定就不要使用setData
  * this.data.变量 与 setData 变量的区别
* Data
  * -数据绑定中的名字必须为Date中的对象名称，不能为函数中的临时变量名称
  * data中的数据均可以在调试器AppData选项中查看
  * data中初始化数据，不可以使用type，如number初始化只能使用0，string初始化则为null或 ' '，原因为number、string在JS中初始化是个函数
  * 如果data中不存在某变量，那么其变量对应的setData会首先在data创建一个该变量然后再去改变该变量的值，但建议所有需要使用的变量都在data中以默认值声明

### 事件

* catch 会阻止事件向上冒泡，[事件 \| 微信开放文档 - 绑定并阻止事件冒泡](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html#%E4%BA%8B%E4%BB%B6%E8%AF%A6%E8%A7%A3)
* 事件触发时，会产生相应的事件对象
* 事件触发时，监听函数都会接收一个event参数
* 自定义事件

### 报错问题

1. thirdScriptError（第三方脚本错误），由自己所写的JS代码错误导致

### **wx : if  条件渲染**

* hidden会阻止出发detached生命周期函数，wx : if则不会，但wx : if会重新执行一次完整的生命周期，会增耗资源



### **wx : for 列表渲染**

* 在wxxm中使用wx : for最好在其标签外层嵌套一层,并在上使用wx : for,并在其需要循环的标签上使用 " ****"
* wx:for-item 可以指定数组当前元素的变量名
* wx:for-index 可以指定数组当前下标的变量名
* block没有实际意义，可以理解为 \( \) ，可以在使用wx : for时不嵌套block，增加block只为提高可读性
* wx:key的意义：为wx:for循环中每个元素提供唯一标识
* 如果循环中的元素是Object，在wx:key数据绑定时，直接使用元素的属性即可
* 如果循环中的元素是数字或者字符串，在wx:key数据绑定时，使用\*this

## **小程序特性**

### behavior行为

> [behaviors \| 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/behaviors.html)

* 小程序可使用behavior来定义组件共同的行为
* behavior是一个构造器，用来构造行为

#### 行为与继承的区别

行为是一种设计模式，继承是编程语言的特性

**继承**：感觉更像物种的进化，物种的扩展，生成新的物种，这些新的物种又具有不同的特性。

也就是说，我必须生成新的具有某种特性或者功能的物种去实现我想要的。

**行为**：想要实现某种功能的时候需要借助别的工具，我想用笔记本电脑画画，那我就买一个触控板，接上就可以。

但是前提是我的笔记本要预留跟触控板链接的接口，behavior就相当于这个预留的接口。

**区别**：从实现方式上讲，继承要实现新的属性功能就必须生成一个新的对象。

## 

### **slot插槽组件模板和样式**

* 可以使标签从组件外部传入内部并替换solt的位置 -插槽没有数量限制，但要区分命名 -基本使用

  * ①.在被替换的位置声明slot标签并命名
  * ②.要使用的替换标签需要被其组件标签使用双标签包裹，并声明被替换的slot标签名称
  * ③.启用slot，在其组件的js文件中Component下增加options对象
  * ④.options对象中定义multipleSlots参数并在指定为true - multipleSlots默认是启用多插槽，但貌似有bug，待查明
  * ⑤.传递时，插槽自身的css有效

  \*\*\*\*

### **WXS语法**

> [WXS（WeiXin Script）是小程序的一套脚本语言](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxs/)

* 增强wxml
  * 过滤器

## 组件

### 组件的基本使用

1. 在wxml中构建组件
2. 在json中引用组件
3. 在页面中使用组件以及数据绑定
4. js中写入数据处理逻辑，model中封装调用API的逻辑

### 微信提供的**内置组件**

* /n换行以及回车换行在内置组件中可自动编译，可使用 / 来转义

### 自定义组件

* 自定义组件理论上是不能使用自定义css样式
* why?自定义组件相当于内置组件的封装，相当于自定义组件是不存在的，只是一组内置组件的总称

### 组件的自定义事件

####  [触发事件](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/events.html#%E8%A7%A6%E5%8F%91%E4%BA%8B%E4%BB%B6)

* triggerEvent\('1',{2},{3}\)
  * 1.自定义事件的名称
  * 2.自定义属性，用来设置监听函数（如onLike）中[detail属性](https://developers.weixin.qq.com/community/develop/doc/000608124a80683cede99b4f85ec00)
  * 3.一般不需要使用，只能使用文档中定义好的可选项

### 外部样式 externalClasses 

> [外部样式 - externalClasses 微信开发文档](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/wxml-wxss.html#%E5%A4%96%E9%83%A8%E6%A0%B7%E5%BC%8F%E7%B1%BB)

* 好处，不违反小程序组件的封装原则
* 外部样式区分于普同样式，普同样式即组件内部的默认样式
* 基本使用
  * ①.在组件的js文件的Component中定义 externalClasses参数，此参数为数组
  * ②.在数组中定义样式名称（如tag-class），可定义多个名称以提供多个样式类
  * ③.在组件wxml中的标签上的class类中，使用样式名称
  * ④.class类中靠后的样式可以覆盖前面的样式，但不一定成功。[在同一个节点上使用普通样式类和外部样式类时，两个类的优先级是未定义的，因此最好避免这种情况](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/wxml-wxss.html#%E5%A4%96%E9%83%A8%E6%A0%B7%E5%BC%8F%E7%B1%BB)。
* 外部样式传递
  * ⑤在组件所在的页面wxss中定义新的样式（如ex-tag
  * ⑥在页面wxml中的组件标签上使用步骤
  * ⑦定义的名称，以及新样式的名称（如tag-class="ex-tag"）
* 解决④中不能覆盖样式的问题
  * ①.问题来源于优先级是未定义的
  * ②.解决优先级的方法：在ex-tag中使用 ! important 来提升新样式的优先级
* 外部样式类的优势
* * 与properties属性传递的区别，css会写在js中

## 性能

### 缓存

* 思路：
  * 获取期刊 → 先到缓存中寻找 → 能找到则读取
  * 找不到 → 向服务器发送请求获取数据 → 并写入到缓存中
* 缓存中的key，是动态的，所以需要确定key

### 异步处理

#### Promise 可以解决的问题：

1. 异步嵌套、回调地狱
2. 被剥夺return的能力时[回调函数真正的问题在于他剥夺了我们使用 return 和 throw 这些关键字的能力。而 Promise 很好地解决了这一切](https://www.jianshu.com/p/063f7e490e9a)。
3. 多个异步等待合并 

#### promise是什么

* promise是一个对象（具体意义上的对象，非JS中一切都是对象）
* 面向对象中，对象可以保存状态，但函数不可以，函数一但被调用之后，必须马上返回结果，不能把结果状态保存在函数内部（但闭包函数可以）
* 总结：
  * promise使用对象的方式，来保存了异步调用的结果，并赋值给一个变量
  * 从而在代码中到处传递，而且不需要附带任何的回调函数，只在取异步调用结果的时候需附加回调函数

#### promise的基本使用

* new promise\(参数\)，参数是一个函数，这个函数又可以接收两个参数，resolve,reject。
* 把需要处理的异步代码，写入promise的函数中

#### promise的三种状态 

* pengding（进行中），new promise的阶段处于此状态中，通过resolve或者reject可以更改状态为fulfilled或者rejected
* fulfilled（已成功），通过resolve更改，可在小程序的success中调用，并返回结果
* rejected（已失败），通过reject更改，可在小程序的fail中调用，并返回异常信息

#### promise的凝固 

* 在fulfilled或者rejected状态修改后，则变为凝固状态 -凝固后不可再次更改状态，这时就称为 resolved（已定型）
* new promise后的作用
* 可使用promise.then方法随时通过接收的变量拿到异步调用的结果
* promise.then\(\[回调函数1\]，\[回调函数2\]\)，`[回调函数1]与[回调函数2]均不是必选项`
* 回调函数1，需要传入当promise已成功时候的回调函数，可在此函数中接收调用的结果
* 回调函数2，用来指定当primise变为失败时候的回调函数 

#### 使用promise解决回调地狱 

* 场景 条件1：多次调用服务器API，存在链式调用 
  * 链式调用：互相调用存在一定的顺序关系
* 条件1，使用回调函数解决的写法

#### promise.all

* promise.all可以把promise的多个实例合并为一个，
* 合并过程为异步，等待时间为最长耗时的子promise
* 基本使用
  * promise.all \( \[ ①,②,③ \] \)
* promise.all合并后实例后，将返回一个新的promise
  * 使用promise.then接收新的promise的返回结果
  * then在promise.all的所有子promise完成后，才会触发
    * 可以利用此特性，使用[wx.hideLoading](https://developers.weixin.qq.com/miniprogram/dev/api/ui/interaction/wx.hideLoading.html)

#### promise.race（竞争）

* 区别于promise.all
* 使用promise.race将不会等待所有子promise完成后再触发then
* 任何子promise率先完成，马上就会触发回调函数
* 返回的回调函数将只包含竞争成功的promise结果

#### 其他处理异步的办法

async（es2017）await（es2017）

## 

### 锁

#### 锁的作用

* 解决重复加载数据的问题
  * 重复加载数据，可能会引起数据在前端重复展示
* 提高服务器性能
  * 禁止向服务器发送无效请求



#### 解决问题1

解决重复加载数据的问题

#### 思路

* 使用户在数据返回前，只能发送一个请求

#### 具体步骤

* data中命名一个变量loading，默认值为false，表示没有发送请求
* 在进入数据加载前，加入判断
* 在开始执行加载数据前，把loading设置为true
* 数据加载完成后，把loading设置为false

注意事项

* 在操作data时，this.data.loading 与 setData（｛ loading ｝），效果一致
* 区别在于，wxml中是否数据绑定loading

## 

#### 解决问题2

提高服务器性能，禁止向服务器发送无效请求

#### 思路

* 在当前的搜索代码中，需要知道对于此次搜索来说，是不是已经把全部的数据加载完毕
* 如果服务器已经返回所有的数据，后续就不会继续向服务器发送请求
* 使用Behavior封装（加载更多）行为，提高复用性 （[behaviors \| 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/behaviors.html)）
  * 组件应用场景：列表数据加载更多

#### 具体步骤

* 封装分页行为
  * 函数1：合并获取完毕的数组
  * 函数2：返回获取所需的起始记录数
  * 函数3：是否还有更多的数据需要加载

    * 可以解决向服务器不断发送无效请求的问题
    * 难点：如何知道服务器是否还有数据返回



    * 解决方案1：total参数表明一次搜索总的记录数，如果dataArray中的总数量已经超过或者等于total，那么就可以认为没有更多的数据加载
    * 方案1缺陷：如果API中没有返回 total，那么setMoreData就无法实现
    * 注意：数据状态默认不清空，如不清空，再次请求的时候还会出现数据重复的问题





    * 解决方案2：通过setMoreData传入的dataArray来判断
      * 假如服务器有60条数据
      * 第一次setMoreData时，dataArray \[ \]中有20条数据
      * 第二次setMoreData时，取的是中间20条
      * 第三次setMoreData时，取的是最后20条
      * 第四次setMoreData时，由于服务器已经没有数据可以返回，dataArray是一个空数组
    * 所以可以在setMoreData中加入判断，一旦监听到dataArray传入的是一个空数组时，那么就代表没有更多数据可以返回
    * 方案2缺陷：判断条件过于绝对，不够准确。假如某次请求出现错误，而服务器返回了空数组，就会导致判断错误

### 死锁

> 场景：断网后发送请求，连接网络后，继续发送请求会得不到响应

#### 死锁的原因

* 请求成功，才会解锁

## 临时记录

### 注意

1. 不要在template上面以及block上面监听事件，可以使用view
2. 扩展运算符...的用法
3. 跳转至tabBar页面，需使用wx.switchTab
4. flexble box 弹性盒子（弹性布局），flex container 弹性容器，flex item容器下的子元素
5. flex布局下的布局会消除block属性
6. 小程序中的request请求均为异步，异步函数的调用结果需要使用回调函数接收，当做参数传入异步函数中，并由异步函数再次接收处理
7. [箭头函数完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj](https://www.liaoxuefeng.com/wiki/1022910821149312/1031549578462080)
8. wx.request中，调用接口返回400序列异常时，返回的是success回调函数（只要是服务器返回的都使用success），在当前网络中断时返回fail回调函数
9. [wx.request基本使用方法](https://developers.weixin.qq.com/miniprogram/dev/api/network/request/wx.request.html)
10. 开发时使用wx.request需要在微信开发者工具中，更改设置-项目设置-不校验合法域名选项
11. 小程序会将properties及data合并为一个JS对象，所以访问任意一个都会访问到同一个合集，所以properties和data中不能出现同名变量，否则会出现覆盖的现象
12. 三元表达式不仅可以用在数据绑定中，还可以用在组件的属性中
13. 使用浏览器network进行数据调试，如点击事件
14. 写业务，写组件


# CSS

## [CSS 关键概念](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

* 语言语法和形式（The syntax and forms of the language）
* 特殊性（另译优先级）、继承和级联（Specificity, inheritance and the Cascade）
* 盒子模型和外边距合并（Box model and margin collapse）
* 包含块（The containing block）
* 堆叠和块格式化上下文（Stacking and block-formatting contexts）
* 初始值、计算值、应用值和实际值（Initial, computed, used, and actual values）
* CSS 简写属性（CSS shorthand properties）
* CSS 弹性盒子布局 \(CSS Flexible Box Layout\) 
* CSS 网格布局 \(Grid Layout\)
* 媒体查询
* 动画

## 浮动

> [CSS清除浮动的8种方法以及优缺点](https://juejin.im/post/5d6f2b845188250587727971)

```text
.clearfix{
    content: "";
    display: block;
    overflow:hidden;
    visibility:hidden;
    height: 0;
    clear: both;
}
.clearfix{
    zoom: 1;
}
```

## 定位及包含块

> [CSS 定位体系](http://w3help.org/zh-cn/kb/)

## 布局

> [三列布局几种经典实现方式](https://juejin.im/post/5bf666d1518825719f208b37)
>
> [CSS 绝对定位 absolute 详解](https://juejin.im/entry/58b3d54e8d6d810057f599bb)

### 经典行布局

* 基础的行布局
* 行布局自适应
* 行布局自适应限制最大宽
* 行布局垂直水平居中
* 行布局固定宽
* 行布局某部位自适应
* 行布局导航随屏幕滚动

### 经典列布局

* 两列布局固定
* 两列布局自适应
* 三列布局固定
* 三列布局自适应


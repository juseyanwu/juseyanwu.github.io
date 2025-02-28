---
title: css相关知识
date: 2025-02-28T00:28:34+08:00
tags: [css]
series: []
featured: true
---
TS
<!--more-->

# css

### css盒模型

- 是什么： 浏览器渲染一个容器时，会把容器渲染成四个区域，分别为 content padding border margin，由这四个区域组成一个盒子模型
- 有什么特点：
  - 标准盒子模型：width 和 height 只定义 **内容区域 **的大小，内边距和边框的大小会额外添加到总宽度和总高度中。
  - IE盒子模型：将 width 和 height 定义为包括 内容区域、内边距、边框 的总和
- 使用 box-sizing: border-box 可以强制浏览器使用标准盒模型



### css 选择器

1. 基础选择器

- 元素选择器：选择制定标签的元素

```css
div {
  color: red;
}
```

- 类名选择器：选择指定的类名，类名前面加 .

```css
.button {
  background-color: blue;
}
```

- ID选择器（#）
- 通配符选择器（*）：选择页面中全部的元素

2. 组合选择器

- 后代选择器
  - 选择某元素内部的所有子元素，不限于直接子元素，可以是任意层级的后代元素：

```css
div p {
  color: green;
}
```

- 子元素选择器（使用 >）

这将应用于所有直接位于 <div> 元素下的 <p> 元素。

```css
div > p {
 color: blue;
}
```

- 相邻兄弟选择器（使用 +）

```css
h1 + p {
  color: red;
}
```

这将应用于紧跟在 <h1> 元素后的第一个 <p> 元素。

- 通用兄弟选择器（使用～）

```css
h1 ~ p {
 color: red;
}
```

这将应用于所有位于 <h1> 元素之后的 <p> 元素，无论它们之间有多少兄弟元素。

3. 伪类选择器

:hover :focus

伪类选择器用于选择处于特定状态的元素，常用于用户交互样式、动态效果等。

4. 伪元素选择器
5. 属性选择器

[attribute="value"]：选择拥有指定属性且属性值为指定值的元素

```css
input[type="text"] {
 background-color: yellow;
}
```



- 选择器优先级

​	•	**ID选择器**（#id）的优先级最高。

​	•	**类选择器**（.class）和 **属性选择器**（[type="text"]）的优先级其次。

​	•	**元素选择器**（div）的优先级最低。

!important 无敌

还有一个内联样式

**!important > 内联 > id > 类选择器 > 元素选择器**



### 说说 em/rem/vh/vw 的区别

- 他们都是css常用的相对单位

- em：相对于声明了font-size的父元素的字体大小来计算，不仅适用于字体，也适用于margin，padding，width等
- rem: 相对于根元素的字体大小
- vh: 相对于视窗高度的百分比
- vw：相对于视窗宽度的百分比



1. 移动端适配方案： rem || 媒体查询
2. pc 端适配方案：% + 媒体查询 || rem



### css当中有哪些方式可以隐藏元素？区别？

- dispaly: none （完全从文档流中移除，不参与布局计算，不触发事件）
- Opacity: 0 （可以触发事件，仍然占据空间）
- visibility: hidden （仍然在文档流中，**但是不触发事件**）
- Position: absolute \+ left: -9999px（脱离文档流，触发不到事件）
- width 0 height 0; 
- overflow: hidden;
- clip-path: polygon(00, 00,00,00) 会把元素全部裁剪掉，使其不可见，但是元素占据空间
- transform: scale(0): 占据文档流，不触发事件

| **方法**                           | **元素占用空间** | **可交互性** | **使用场景**                     |
| ---------------------------------- | ---------------- | ------------ | -------------------------------- |
| display: none                      | 不占空间         | 不可交互     | 完全移除元素，常用于动态显示隐藏 |
| visibility: hidden                 | 占空间           | 不可交互     | 隐藏元素，但保留其占用空间       |
| opacity: 0                         | 占空间           | 可交互       | 隐藏元素内容，但保留其交互性     |
| position: absolute + left: -9999px | 占空间           | 不可交互     | 将元素移出视口                   |
| z-index: -9999                     | 占空间           | 不可交互     | 将元素隐藏在其他元素下方         |
| clip-path: polygon(00,00,00,00)    | 占空间           | 不可交互     | 通过剪切隐藏元素，常用于动画     |
| overflow: hidden                   | 占空间           | 可交互       | 处理超出容器的内容               |



### 说说你对BFC的理解

- BFC 是什么：block formatting context，浏览器渲染的一个特殊区域，有自己独特的渲染规则，BFC容器是一个独立的布局环境，其中的子元素不会影响BFC之外的元素
- 触发条件：
  - float不是 none （float：left ...
  - position 的 absolute 或 fixed
  - display 取 inline-xxx table-xxx flex grid
  - overflow 取值不是visible。（hidden，auto，scroll）
- BFC的特性
  - BFC内部的元素不会影响外部元素
  - BFC 内部的元素 的外边距不会与外部元素的外边距重合
  - BFC计算高度时会把内部浮动元素的高度计算在内（清除浮动问题）
    - 父元素如果没有height，子元素设置float之后会导致父元素高度坍塌，而BFC可以解决
  - BFC 的区域不会与浮动元素重叠，因此可以用 BFC 避免文本环绕浮动元素的情况。（假设前面一个元素float：left了，后面有一个文本，默认会环绕它，但是将文本设置成bfc的话，可以避免环绕）



### 元素水平垂直居中的方法

- FlexBox

  - display: flex; align-item: center;// 垂直居中 justify-content: center //水平居中(弹性的主轴居中)

- Grid

  - dispaly: grid; place-item: center;

- position: absolute; top:50%; left:50%; transform: translate(-50%, -50%)

  - ```css
    .item {
    
     position: absolute;
    
     top: 50%;
    
     transform: translate(-50%, -50%); /* 向上和向左平移 50% */
    
    }
    ```

    

- 定位 + margin负值 （需要知道子容器的宽高）

- 定位 + margin: auto （需要子容器有固定宽高）

- table-cell

  - ```css
    .container {
     display: table;
     width: 100%;
     height: 100vh;
    }
    .item {
     display: table-cell;
     vertical-align: middle; /* 垂直居中 */
     text-align: center;   /* 水平居中 */
     width: 200px;
     height: 200px;
     background-color: lightpink;
    
    }
    ```

- 三布局：flex；gird；table；三定位：+transform +auto +负值



### 说说你对css动画的理解

- transition

  - ```css
    selector {
      transition: property duration timing-function delay;
    }
    ```

    •	property：指定动画应用的 CSS 属性（可以是某个具体的属性，或者 all，表示所有可过渡的属性）。

    •	duration：动画持续的时间，单位通常是秒（s）或毫秒（ms）。

    •	timing-function：定义动画的速度曲线，控制过渡的加速度，可以使用 ease、linear、ease-in、ease-out、ease-in-out 等。

    •	delay：设置动画开始的延迟时间。

- transform
  -  transform: rotate(45deg); // 旋转
  -  transform: scale(2) // 放大两倍
  -  transform: translateX(50px);
- Animation + keyframes



### 响应式布局的实现方式有哪些？

- 根据视窗宽度来自动调节页面模块的大小和位置



- 媒体查询

```css
/* 默认样式 */
.container {
  width: 80%;
}

/* 当屏幕宽度小于等于 768px 时 */
@media (max-width: 768px) {
  .container {
    width: 100%;
  }
}

/* 当屏幕宽度小于等于 480px 时 */
@media (max-width: 480px) {
  .container {
    width: 100%;
    padding: 10px;
  }
}
```

- 使用百分比宽度

- flexbox布局
- grid布局
- vh/vw
- max-width 和min-width



### css 性能优化

- 首页使用内联样式
- 异步加载 css
- 压缩
- 合理使用选择器



### 文本单行显示，溢出则省略号

```css
p{
  width: 100%;
  overflow: hidden; //超出则隐藏
  white-space: nowrap; // 文本不换行
  text-overflow: ellipsis; //超出...
}
```



### css画三角形

- 利用border的特性，假设两个边框重合，一个边框transparent了，那么另一个有颜色的边框天生会被切掉一半，形成一种三角形



### 聊聊 css 与处理器

- less
- sass
- stylus

1. 是一种css语言
2. 可以使用变量，函数，继承，混入



### flex布局

- 弹性容器的子容器会默认继承弹性容器的100%的高度
  - 继承的是交叉轴轴方向上的长度
    - 假设使用flex-direction: column使得主轴变为y轴，那么内部的子容器会默认拥有弹性容器的100%的宽度（交叉轴）
- 默认情况下，子容器在主轴上是不放大，会缩小的
- flex的三个参数 flex: 0 0 150px 
  - 第一个参数是 flex-grow （是否允许放大）默认为0
  - 第二个参数是flex-shrink (是否允许缩小) 默认为 1
  - 第三个参数是flex-basis （基准大小）
- flex-warp: warp 允许换行

---
title: 
date: 2021-08-17 21:04
tags: CSS
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/2.jpg
summary: 盒模型、文档流、布局、定位、装饰领域
---


这节课程先从CSS的诞生背景和基础定义入手，初步认识CSS；然后介绍了如何能够正确地学习CSS。介绍了CSS关键的盒模型、文档流、布局、定位等关键概念和相关CSS属性，并展示了CSS装饰文档的可能性。最后，在简略看下如何调试eSS，以及当今都有什么工具可以帮助我们更好的写CSS、用更好的理念去用CSS。



# CSS常用规则

## 布局相关

### 盒模型（重要）

在具体介绍布局相关的属性之前，先要了解:在CSS中，所有的元素都被一个个的“盒子(box)”包围着，理解这些“盒子”的基本原理，是我们使用CSS实现准确布局、处理元素排列的关键。

![image-20210815215329724](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815215329724.png)



CSS中组成个块级盒子需要

- Content box:这个区域是用来显示内容，大小可以通过设置width和height.
- Padding box:包围在内容区域外部的空白区域，大小通过padding相关属性设置。
- Border box:边框盒包裹内容和内边距。大小通过border相关属性设置。
- Margin box:这是最外面的区域，是盒子和其他元素之间的空白区域。大小通过margin相关属性设置。



盒子

- 块级盒子(block box)

- 内联盒子(inline box)。 

  这两种盒子会在页面流(page flow)和元素之间的关系方面表现出不同的行为




>关于盒模型可以看看这篇👉 [CSS盒模型的面试六问你能答出几个？](https://juejin.cn/post/6988877671606272031)，如果完全不懂盒模型，则多百度几篇关于【盒模型】，【块级盒子】，【内联盒子】的文章，理解这些对布局很重要。



盒模型的一些关键词

- margin:设置外边距
- border:设置边框
- padding:内边距
- width & height:内容宽高
- box- sizing:修改宽高的定义范围
- display:改变元素是块级盒子还是内联盒子的特征



### 正常文档流

默认的，块级元素按照基于其父元素的书写顺序(默认值:horizontal-tb)的块流动方向(block flow direction)放置

每个块级元素会在上一个元素下面另起一行，它们会被设置好的margin分隔。块级元素是垂直组织的。



内联元素的表现有所不同---它们不会另起一行;只要在其父级块级元素的宽度内有足够的空间，它们与其他内联元素被安排在同一行。

如果空间不够，溢出的文本或元素将移到新的一行。



## 弹性布局

弹性盒子是一种用于按行或按列布局元素的一维布局方法。元素可以膨胀以填充额外的空间，收缩以应更小的空间。

弹性盒子关键词

- display: flex: 一键开启弹性盒子模式，替代正常文档流
- flex-direction:更改弹性盒子的「主轴」
- justify- content:子元素主轴线上如何对齐
- align-items:子元素横轴线上如何对齐
  



> 弹性布局推荐阮一峰的这篇文章👉[Flex 布局教程](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)，如果是新手，一定要学会这种布局方式，超方便。<br/>
> 这篇也说的很详细，不过要翻强，是英文[css-tricks 弹性盒子介绍](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)


## 定位（position）



position: static

不管是正常的文档流，还是弹性盒子，内里元素排布都是相互影响的。前面的元素占了一块地，后面的元素肯定得往后稍稍。

这其实只是其中一种「定位情况」， 叫「静态定位」具体到CSS就是position: static;默认给到每个元素



position: relative

position还能有其他值，比如「相对定位」， position: relative

相对定位在文档流中仍然占据位置，但可以用top, left, bottom, right 属性做一些偏移的操作


position: absolute,
这种叫「绝对定位」。绝对定位的元素完全脱离了文档流和什么弹性盒子。绝对定位的盒子的定位、大小，你可以完全指定。

此时top, left,已经不是相对于原位置，而是相对于一个非static定位的父元素容器I



position: fixed

它和absolute类似, 其top, left等属性是相对于浏览器窗口



z-index

因为非static值的position属性让元素之间可以相互覆盖，css 提供了z- index属性来控制哪个元素覆盖在最上层



>  除了布局流、弹性盒子和绝对定位的使用，还有float、table、grid 布局等可以自行探索



# 装饰领域

## 文字

网页字体样式包括`类型、大小、颜色`基本效果，另外还包括一些特殊的样式，如`字体粗细、下划线、斜体、大小写样式`等。

```
/*文本尺寸*/
font-size:18px;  

/*文本字体*/
font-family:"隶书"; 

/*文本加粗  bold 加粗  bolder 更粗*/
font-weight:bold;    

/*文本颜色*/
color:red;   

 /*文本倾斜  oblique也可以  但最好用italic*/
font-style:italic;   

```



```
/*文本水平居中  center 居中     justify  两端对齐       left 左对齐   right  右对齐*/
text-align:center;  

/*字符间距*/
letter-spacing:2px;   

 /*行高*/
line-height:20px;    

  /*首行缩进*/
text-indent:2em;  

/*单词间距*/
word-spacing:2px;   

 /*垂直居中*/
line-height:2px;    

/*字符装饰线   underline  下划线       line-through   删除线     overline  上画线    更多用于超链接样式*/
text-decoration:underline;   
```



## 背景

```
/*背景颜色*/
background-color:#ccc;    

/*背景图片 可以简写   直接加颜色   就是添加背景颜色  图片也一样*/
background-image:url(img/*.jpg);   
```



>[MDN CSS background 属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background)



## 边框



>[MDN CSS border 属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border)



## 阴影



盒子阴影

![image-20210815230238248](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815230238248.png)

>[MDN CSS box-shadow 属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow)
>
>[最全的CSS阴影总结](https://juejin.cn/post/6982595708796796965)



文字阴影

![image-20210815230221504](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815230221504.png)

> [MDN text-shadow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-shadow) 



## 交互相关

cursor

属性设置光标的类型（如果有），在鼠标指针悬停在元素上时显示相应样式。

> MDN [cursor-pointer](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor)



过渡 transition

过渡可以为一个元素在不同状态之间切换的时候定义不同的过渡效果。比如在不同的伪元素之间切换，像是 [`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover)，[`:active`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active) 或者通过 JavaScript 实现的状态变化。

> [MDN transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)



动画 animation

`animation` 属性用来指定一组或多组动画，每组之间用逗号相隔。

> [MDN animation](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)



transform

**`transform`**属性允许你旋转，缩放，倾斜或平移给定元素。这是通过修改CSS视觉格式化模型的坐标空间来实现的。

> [MDN transform](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)
>
> [CSS之详解2D转换](https://juejin.cn/post/6976617452738183176)



# CSS精益求精

## CSS调试

审查CSS

从页面上选择一个元素，可以右键该元素，选择审查元素（Inspect) 

从DevTools左侧HTML tree中选择该元素。

- 在面板里，你可以直接开关、编辑、新增属性的值。

![image-20210815231547558](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815231547558.png)





## CSS扩展

CSS预选择器

另一种组织CSS的方法是利用一些对于前端开发者可用的工具，它们让你可以稍微更程式化地编写CSS。预处理工具以你的原文件为基础运行，将它们转化为样式表。

代表工具有: 

- less
- sass
- stylus



> [less学习指南](https://juejin.cn/column/6992233701916540936)



## CSS革新

这些年CSS的发展，我们编写样式已经不一定需要写css文件了。

以styled- components为代表的CSS -in-js 方案，用JavaScript的力量武装css



>[styled- components官网](https://styled-components.com/)



以tailwindcss为代表的utility- class方案，改样式就改html文件即可，用有限的选择帮助你定好设计规范。

> [tailwindcss官网](https://www.tailwindcss.cn/)


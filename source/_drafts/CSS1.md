
---
title: CSS是什么？怎么学？
date: 2021-08-16 21:04
tags: CSS
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/1.jpg
summary: 
---


这节课程先从CSS的诞生背景和基础定义入手，初步认识CSS；然后介绍了如何能够正确地学习CSS。介绍了CSS关键的盒模型、文档流、布局、定位等关键概念和相关CSS属性，并展示了CSS装饰文档的可能性。最后，在简略看下如何调试CSS，以及当今都有什么工具可以帮助我们更好的写CSS、用更好的理念去用CSS。



# 前言

- CSS是啥？
- CSS怎么学？
- CSS基础
- CSS进阶



# CSS是啥

CSS,层叠样式表(cascading syle sheets)，-种用来为结构化文档(基本就是html)添加样式的语言。

举例来说，要选择一个HTML页面里所有的段落元素，然后将其中的文本改成红色，可以这样写CSS

![image-20210815202724354](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/16/image-20210815202724354.png)




在学习HTML时，我们可以看到浏览器给予每个标签的默认样式。

有了CSS，我们可以给文档添加自定义样式

- 比如改变标题和链接的颜色及大小。
- 也可用于修改布局
- 比如将一个单列布局变成双列，包含主要内容区域和存放相关信息的侧边栏区域。
- 另外还可以用来做一些特效和动画



## CSS诞生背景
在没有css以前，所有样式都混在html里。假如一个标题要用斜体字、红色的字符、白色的底色的话，要这样写:

![image-20210815203234600](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815203234600.png)




有了CSS之后，样式就可以和文章结构分离了。

![image-20210815203729298](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815203729298.png)



除了做到分离，CSs 这一个样式语言单独抽出来，能够提供更大的表达空间;

上面例子里，css语法一样可以合在html里写。

![image-20210815203842675](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815203842675.png)





## CSS基础规则

让我们来仔细CSS的结构
整个结构称为规则集(通常简称“规则”)，各部分释义如下:

![image-20210815204238678](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815204238678.png)

- 选择器:选择了个或多个需要添加样式的元素(在这个例子中就是p元素)
- 声明：一个单独的规则，如color: red;用来指定添加样式元素的属性。
- 属性:指定要改变HTML元素样式
- 属性的值：从指定属性的众多外观中选择个值(除了red之外还有很多color的值)



注意1

- 每个规则集（除了选择器的部分）都应该包含在成对的大括号里`{}`
- 在每个声明里要用冒号`:` 将属性与属性值分隔开。
- 在每个规则集里要用分号`;`将各个声明分隔开。

注意2

- 如果要同时修改多个属性，只需要将它们用分号隔开
- 也可以选择多种类型的元素并为它们添加一组相同的样式。将不同的选择器用逗号分开

![image-20210815204639398](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815204639398.png)

## 选择器

选择器有许多不同的类型。上面只介绍了元素选择器，用来选择HTML文档中给定的元素。但是选择操作可以更加具体。

下面是一 些常用的选择器类型:

| 选择器名称                         | 选择的内容                                                   | 示例                                                         |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 元素选择器(也称作标签或类型选择器) | 所有指定(该)类型的HTML元素                                   | p<br />选择<p>                                               |
| ID选择器                           | 具有特定ID的元素(单一HTML页面中，每个ID只对应一个元素， 一个元素只对应一个ID) | #my-id<br />选择 <p id= "my-id">或 <a id="my-id">            |
| 类选择器                           | 具有特定类的元素(单一页面中，一个类   可以有多个实例)        | .my-class   <br />  选择<p class= ”my-class">和 <a class= "my-class"> |
| 属性选择器                         | 拥有特定属性的元素                                           | img[ src]<br/>选择`<img src=" my image.png">`而不是< img>    |
| 伪(Pseudo) 类选择器                | 特定状态下的特定元素(比如鼠标指针悬停)                       | a: hover<br/>仅在鼠标指针悬停在链接上时选择<a>。             |



层叠与继承

CSS代表层叠样式表(Cascadjing Style Sheets)，理解第一个词cascading很重要——cascade的表现方式是理解CSS的关键。

示例

我们有两个关于h1的规则。h1最后显示【红色】

- 这些规则有相同的优先级，但顺序在最后的生效。

![image-20210815205856519](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815205856519.png)



浏览器有个选择器优先级来决定规则，基本上是一个选择器越具体越优先。

- 一个元素选择器不是很具体👉会选择页面上该类型的所有元素

- 一个类选择器稍微具体点👉它会选择该页面中有特定class属性值的元素一所以它的优先级就要高一点。

  示例

  下面的h1最后会显示绿色

  ![image-20210815210331224](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815210331224.png)



一些设置在父元素上的css属性是可以被子元素继承的，有些则不能。

示例

如果你设置一个元素的color 和font- family，每个在里面的元素也都会有相同的属性值，除非你直接在元素上设置属性。

![image-20210815210843425](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815210843425.png)

这些概念一起来控制css规则应用于哪个元素;有时候会感觉有些复杂，但是当你对css有更多经验的时候，你就可以记住它们，即便忘记了细节，可以在网上查到。



看一个更复杂的例子

【颜色】和【字体加粗】都被继承了；【边框border】 就没有(不然每个子元素都有框框得多丑)，说明浏览器会根据常识判断哪些属性该被继承；

![image-20210815212610017](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815212610017.png)



# CSS怎么学

## 免费课程


在进一步讲解CSS有哪些规则之前，先给大家分享几个学习资源。因为CSS的内容非常多，也非常适合自学，这里给大家几个课后能不断耕耘CSS知识的免费网站。



[codecademy](https://www.codecademy.com/)【英文】

老牌在线编程教育网站。全程交互式自助式学习体验。非常适合CSS 边学边练的场景。



[udacity](https://www.udacity.com/)【视频类】

也是老牌在线编程教育网站。虽然是外文站点，但进入课程内中文是拉满的。

推荐理由

- 是免费;
- 是视频式教学+课后实验互动的形式，给喜欢看着老师讲解的同学推荐。
  

[w3school](https://www.w3school.com.cn/)和[runoob](https://www.runoob.com/)

免费，交互式，内容相当全面，不错的实操演练场。



[freecodecamp【英文地址】](https://www.freecodecamp.org/) Or [freecodecamp【中文地址】](https://chinese.freecodecamp.org/)

Github上star最多的项目。由社区贡献而成的全面的程序员自学课程。



挑一个

推荐顺序的话就是从前到后推荐。就是`专业在线课程团队出品>自助式学习≈社区型自助式`。
如果你是零基础，上面任一个课程， 一个周未左右应该能学的差不多。有了基础后， 以后你再想深挖哪个场景下的css应用规则，再去看文档即可。什么场景(字体、定位、颜色等)查哪些属性你心中应已了然。

> 以上是老师推荐，个人推荐，自己觉得哪个适合自己选哪个，其实知识都是那些，只是学习方式不同而已，所以选择自己喜欢的方式即可



## 持续学习

下面这些真学习资料， 如果你干前端这行，它们会陪你到一辈子。



[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

CSS文档库。基本会是前端程序员最常来的地方(html、8 js规则也在里面)。同时，里面还有丰富的各式教程，作为一个自由探索的网站也是相当不错。



[css-tricks](https://css-tricks.com/almanac/)

另一个Css文档库，用有别于mdn的形式组织css知识，还有非常活跃的css社区，里面有各种奇技淫巧。作为mdn文档的补充相当合适。



[*w3c CSS 标准](https://www.w3.org/Style/CSS/)

前面的不管是教程还是文档，基本只会教你用法。大部分用法其实也是自说明的，比如color; red;就是文本变成红色，还要啥自行车?

但:

- 现实中有很多CSs规则，在不同的场景下会不同的表现，而普通文档不会告诉你为什么(甚至不告诉你有这事儿)

- 不像color这种，有很多CSS规则射组合起来使用会实现很神奇的效果，你可能会好奇为什么(其实color能影响的远不止文本的颜色，你想知道么? )

  

  w3c文档，就是解答这些问题（平时基本不逛，遇到问题时可在这查询）






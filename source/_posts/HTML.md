---
title: 
date: 2021-08-15 16:15
tags: HTML
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//00juejincundang/%E5%B0%81%E9%9D%A2/2021/10/02/DIK%609H%7D2QD%7B25I-T%7B8_YC_M.png
summary: HTML的基本介绍
---


HTM知识体系

- HTML是什么

- HTML发展历史

- HTML在前端开发中的角色

- HTML和JS/CSS的关系

- HTML如何使用，如何写出更加具有语义话的HTML

  

# HTML简介

HTML(HyperText Markup Language,超文本标记语言),用于构建网页基本结构及其内容的标记语言。
超文本:文本中包含指向其他文本的链接
标记语言:将文本以及文本相关的其他信息结合起来,展现出关于文档结构,如:HTML、XML、KML、 Markdown等

发展历史

- 1989年——伯纳斯-李提出了基于互联网的超文本系统

- 1993年——IETF(互联网工程任务组)发布首个TML提案,由此HTML语言第一版诞生

- 1994年——W3C成立,随后接管了HTML的标准化工作

- 1995年——在经历过几个草案之后HTML2.0发布（这个版本主要是补充一些基本功能,包括了基于表单的文件上传、表格、国际化等功能

- 1997年——1月发布了HTML3.2，随后12月发布了HTML4.0（这个 版本中采用了许多特定浏览器的元素类型和属性

- 2014年——HTML5作为W3C推荐标准发布

  

  HTML5主要解决了几个问题：

  1、文档结构的混乱，以前的文档结构过渡依赖于div标签，HTML提出了多种语义化的标签，使得文档便于理解，并且有利于SEO优化

  2、解决了浏览器兼容问题，统一标准

  3、扩展了外部应用的一些功能，提供了一些新的API

# HTML结构

## HTML说明

- HTML文档包含多个HTML元素,元素具备不同的特性

- HTML元素=开始标签+结束标签+元素内容

- 一些元素只有一个标签,如img、 input、br等

- HTML元素标签不区分大小写

- 元素可以嵌套在其他元素中间

- 元素可以拥有属性,属性包含有元素的额外信息

  ![image-20210815132516080](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815132516080.png)



## 基本结构

![image-20210815132441283](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815132441283.png)

```
<!DOCTYPE html>:放在HTML文档最前面的位置，加上之后就会按照W3C的HTML 5标准来解析渲染页面

<html>:根元素，包含整个页面的内容

<head>:对用户不可见，其中包含例如面向搜索引擎的关键字、页面描述、字符编码声明、CSS样式等

<body>:该元素包含能够被用户访问到的内容，包括文本、图像、视频、游戏、音频等

```

### head中包含的元素

meta

- charset
- name
- http- equiv

```
定义文档字符编码
<meta charset="utf- -8"> 

关键字
<meta name="keywords" content="HTML">

页面描述
<meta name="description" content="HTML基础">

主要用于移动端，定义设备屏幕上用来显示网页的区域
<meta name="viewport" content="width=device -width,initial- scale=1.0, maximum- scale=1.0, user - scalable=0">

http头部自定义meta,用于向特定网站提供一些信息https://wiki.whatwg.org/wiki/MetaExtensions
<meta "http-equiv="expires" content="31 Dec 2021">

```

title

```
<title>:页面的标题，显示在浏览器标签页上
```

style

```
<style>: CSS样式
```

link

```
当前页面的favicon
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">

链接到样式表
<link rel="stylesheet" href="my- CcSs file.css">

可替换的样式表(非所有浏览器支持)
<link href-"fancy.css" rel="alternate styleshet" type="text/css" title="Fancy">
```

script

```
可执行脚本
<script type="text/javascript" src="javascript.js">
```

属性

- defer：立即下载， 延迟执行，表示脚本可以等到dom被完全解析和显示之后在执行，只对外部脚本有效。有defer属性的脚本会阻止DOMContentL oaded事件，直到脚本被加载并且解析完成。
- async: 立即下载脚本， 不妨碍其他操作，比如下载其他资源或载其他脚本， 只对外部脚本有效

![image-20210815134347111](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815134347111.png)

### body

内联元素

- 只占据它对应标签的边框所包含的空间
- 只能容纳文本或其他内联元素
- 只能通过修改水平边距、边框或者行高的方式改变尺寸
- 常用的内联元素: `<a>、 <span>. <br>、 <i>、 <em>、<strong>、<label>、 <q>. <var>、 <cite>、<code>`



块级元素

- 占据其父元素的整行，总是从新行上开始
- 能容纳其他块元素或者内联元素
- 可以控制宽高、行高、边距、边框等改变其尺寸
- 常用的块级元素

```
<div>、<p>、 <h1>-<h6>、<ol>、<ul>、<dl>、<table>、<address> 、<blockquote> 、<form>
```



行内块级元素

- 元素在行内排列，不会独占一行
- 支持设置宽高以及垂直边距、边框
- 常用的内联元素: `<img>、 <input>、 <td>`

### 语义化

根据内容的结构，选择合适的标签构建出便于开发者阅读的可维护性更高的代码结构，同时能够让机器**更好地解析**。

![image-20210815135522740](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815135522740.png)

语义化—区块

header

```
<header>
- 展现介绍性信息
- 通常包含一组介绍性或是辅助导航的元素，如标题、Logo、 搜索框、作者名称等
- 不能放在<footer>、<address> 或者另一个<header>元素内部
```

![image-20210815140113980](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815140113980.png)

nav

```
<nav>
- 在当前文档或其他文档中提供导航链接，如菜单、目录、索引等
- 用来放置一些热门的链接，不常用的链接通常放到footer里置于底部
```

![image-20210815140125293](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815140125293.png)

article

```
<article>
- 独立的文档、页面、应用、站点
- 可独立分配的或可复用的结构，如论坛帖子、新闻文章、博客、用户提交的评论、交互式组件等
```

![image-20210815140346733](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815140346733.png)

section

```
<section>
- 按主题将内容分组，通常会有标题
- <section> 通常出现在文档的大纲中
- 不要把<section>作为 普通容器来使用，比如说用于美化片段样式，此时用<div>更合适
- 如果元素里边是独立的整块的内容，可以单发布，则更适合用<article>
```



aside

```
<aside>
- 表示一个和其余页面内容几乎无关的部分，或者说单独拆出来不会影响整体的内容
- 通常放在侧边栏，用于展示广告、tips、 引用内容等
```

![image-20210815140821979](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815140821979.png)

footer

```
<footer>
- 表示最近一个章节的页脚
- 通常包含该章节作者、版权数据或者文档链接等信息
- footer内的元素不属于章节内容，不包含在大纲中
```

![image-20210815140922261](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815140922261.png)



可以看看[MDN](https://developer.mozilla.org/zh-CN/docs/Learn)这个页面的语义化

![image-20210815141309105](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815141309105.png)



语义化-分组

figure、figcaption

```
<figure>/ <figcaption>
- <figure> 包裹被独立引用的内容:图表、插图、代码等,通常会有一个标题
- <figcaption>与其相关联的图表的说明/标题，通常位于<figure>的第一个或最后一一个
```

![image-20210815141745515](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815141745515.png)

blockquote

```
<blockquote>
- 块级引用元素
- cite属性表示该来源的url
```

![image-20210815141937538](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815141937538.png)

dl、dt、dd

```
<dl>/ <dt>/ <dd>
- 用于描述-组键值对
- 通常用于元数据、术语定义等场景
```

![image-20210815142110423](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815142110423.png)



语义化—文本

cite

```
<cite>
- <cite> 元素通常用于引用作品标题.
- 包括论文、文件、书籍、电影等的引用

```



time

```
<time> >
- 机器可读的时间和日期
- datetime表示此元素关 联的时间日期，若不指定则该元素不会被解析为日期
```



其他

```
<address>某个人或组织的联系信息
<mark>在引用中使用，表示需要引起注意
<code>代码片段
<small>免责声明、注意事项等
```



### 多媒体元素

图片

  img

- src属性是必须的，嵌入图片的文件路径
- alt属性包含一条对图像的文本描述，非强制。屏幕阅读器会将这些描述读给需要使用阅读器的使用者听，让他们知道图像的含义。图像无法加载时(网络错误、内容被屏蔽或链接过期时)，浏览器会在页面上显示alt属性中的文本
- decoding 解码方式:异步、同步
- loading懒加载



picture

- 元素通过包含零或多个<source>元素和一个<img>元素来为不同的显示/设备场景提供相应的图像版本
- media属性:依据的媒体条件渲染相应的图片，类似媒体查询
- type属性: MIME类型，根据浏览器支持性渲染相应的图片

![image-20210815142723085](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815142723085.png)



音视频

video

- src属性是必须的，嵌入视频文件路径
- controls 是否展示浏览器自带的控件，可以创建自定义控件
- autoplay是否自动播放
- source元素表示视频的可替代资源(不同格式、清晰度，读取失败或无法解码时可以依次尝试)



![image-20210815143258998](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815143258998.png)



## HTML解析



DOM(文档对象模型)：对节点结构化表述，并定义了一种方式可以使程序对该结构进行访问将web页面和脚本语言连接起来

- 构建DOM树
- 样式计算，构建CSSOM树
- 将DOM和CSSOM组合成- -个Render树
- 布局计算
- 绘制

![image-20210815150252169](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/08/15/image-20210815150252169.png)












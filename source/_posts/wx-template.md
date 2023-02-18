---
title: 小程序template模板使用详解
date: 2021-09-07
tags: 小程序
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/16.jpg
summary: 小程序template模板
---
WXML提供模板（template），可以在模板中定义代码片段，然后在不同的地方调用。


# 模板的基本使用

## 创建模板文件

在page里面创建一个template文件夹，可以利用小程序开发工具【新建Page】快速创建文件

![image-20211007123341112](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/07/image-20211007123341112.png)



> **注：**调用模板的时候，起作用的只有wxml和wxss文件，模板中的JS文件是不起作用的。模板中的逻辑都要在**调用的文件**中处理。

> 创建文件可根据自己项目设计，并非固定如此

## 定义模板

在`<template/>`内定义代码片段，使用 name 属性，作为模板的名字。

```
<template name="msgItem">
    <view>
        <text class="info">这是一个msg模板</text>
    </view>
</template>
```

## 使用模板

在wxml中要使用模板，有两步

1）、声明，关键  import 标签

2）、使用，关键  is属性

```
<!-- index.wxml -->

<!-- 声明需要使用的模板文件 -->
<import src ="../template/template.wxml"/>

<!--使用-->
<template is="msgItem"/>
```

> 这里is的名字和模板name命名的保持一致

## 模板的wxss

如果模板有自己的wxss，如我们的`template.wxss`文件，则需要在调用模板的文件（如示例的`index.wxss`）导入，否则不会生效

```
/**index.wxss**/
@import "../template/template.wxss";
```

> 归纳：
> - wxss导入wxss中
> - wxml导入wxml中
> - js无效

# 模板的数据传递

【调用的wxml】通过`data`给模板传值

```
<!-- index.wxml -->

<template is="msgItem" data="{{...item}}"/>
```



item是在调用的js中定义好的

```
<!-- index.js -->

Page({
  data: {
    item: {
       title: '模板',
       msg: 'this is a template',
    }
  }
})
```



在模板直接使用

```
<!-- template.wxml -->

<template name="msgItem">
    <view>
        <text class="info">
            {{title}}: {{msg}}
        </text>
    </view>
</template>
```

> 如果有传递多个参数，则用逗号隔开
> `<template is="msgItem" data="{{data1, data2}}"/>`


# 模版文件中的事件处理

模板使用的是【调用模板的js文件】里的事件。

- 定义在自己的`template.js`并不会生效

![image-20211007131916131](https://gitee.com/Olivivian/PicGoImages/raw/master/img//https/gitee.com/Olivivian/PicGoImages/raw/master/img/Typora/typora-user-images/2021/10/07/2021/10/07/image-20211007131916131.png)

```
<!--template.wxml-->

<template name="msgItem">
    <view>
        <text class="info" bindtap="handleTap">
            {{title}}: {{msg}}
        </text>
    </view>
</template>

```



```
<!-- index.js -->

handleTap() {
    console.log('template 模版 click')
  },

```

## 优化模板事件

如果是模板公用的方法，在每个调用的文件都要把方法写一遍，会有很多重复的代码，我们可以这样改进一下。

虽然`template`模板不能直接使用自己的js，但是我们可以把方法统一写在`template.js`文件里，然后在使用模板的文件js里面引入一下。

![image-20211007133531684](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/07/image-20211007133531684.png)



在任意js文件统一定义方法

```
<!-- template.js -->

const template = {
    handleTap() {
        console.log('template 模版 click')
    }
}

export default template;
```



在需要使用的地方导入即可

```
// index.js
import template from '../template/template';

Page({
  handleTap:template.handleTap
})
```



## 关于js文件中的数据传递

在`template.js`里可以直接拿到`index.js`文件的整个data

![image-20211007134501125](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/07/image-20211007134501125.png)





# template模板和Component组件的异同



**相同点**

- 都是为了实现代码的复用
- 都不能单独呈现，必须依附显示在页面



**区别**

**template模板**：轻量级，主要是展示，没有配置文件(.json)和业务逻辑文件（.js）,所以template模板中的变量引用和业务逻辑事件都需要在【引用模板的页面js】文件中进行定义；

**Component组件**：有自己的业务逻辑，由4个文件构成，与page类似，但是js文件和json文件与页面不同。



**选择**

- 如果只是展示，使用template就够了；

- 如果涉及到的业务逻辑交互比较多，最好使用component组件；



# import 的作用域

import 有作用域的概念，即只会 import 目标文件中定义的 template，而不会 import 目标文件 import 的 template。

```
C import B import A

//C能用B，B能用A，但是C不能用A
```



![image-20211007141552243](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/07/image-20211007141552243.png)







参考资料：

[微信小程序template模板](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/template.html)



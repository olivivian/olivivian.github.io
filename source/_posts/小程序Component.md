---
title: 小程序自定义组件Component超全实用指南
date: 2021-10-06
tags: 小程序
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/25.jpg
summary: 
top: true
---

在小程序中，想要将页面内的功能模块抽象出来，在不同的页面中**重复使用**，我们可以使用它的自定义组件，自定义组件可以将复杂的页面拆分成多个**低耦合**的模块，这样不仅使用起来方便，而且还有助于我们的代码维护。



# 基础准备（可忽略）

## 新增文件夹

首先在根目录下创建一个专门放自定义组件的文件夹（文件夹名称任意，位置也任意）

![image-20211006103521102](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006103521102.png)



## 新建Component文件

然后在小程序编辑器里，右键，新建Component

![image-20211006103715178](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006103715178.png)



为什么要特意说这一步呢？不知道有没有小伙伴们和我一样一直只把小程序开发工具当预览工具用，然后开发是用其他编辑器的。

![image-20211006111612994](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006111612994.png)



后面发现直接在小程序新建Component或者Page，它会一口气把四个文件都建好，并且内容模板也会填好，所以现在开发者工具除了预览，我还用它新建文件。

![image-20211006115815839](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006115815839.png)



## 示例背景说明

我们后面就以下图中的模块分割标题为例写一个简单的组件示例

![image-20211006113723009](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006113723009.png)

# 引入自定义组件

创建不多说，如以上【新建Component文件】即可，如果是自己手动创建，别忘了在json文件声明（小程序新建的默认就有）

```
{
  "component": true
}
```

**引入组件方法**

![image-20211006121146357](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006121146357.png)

在页面的 `json` 文件中进行引用声明

```
<!-- 引用组件的json文件 -->
{
  "usingComponents": {
    "x-title": "/components/title/title"
  }
}
```



在页面的 `wxml` 中像使用基础组件一样使用自定义组件（名字和声明的保持一致）

```
<!-- 引用组件的wxml文件 -->
<x-title></x-title>
```



# 传值

## 父组件给子组件传值

我们上面把标题的内容写死了，但是实际中使用我们肯定是需要根据不同的模块，传入不同的标题内容，这样我们就需要使用到父子之间的传值了。

**父级给子级传值**

```
<!-- 父级wxml -->
<x-title titleText="全部订单"></x-title>

<!-- 如果父级的值是一个变量则 -->
<x-title titleText="{{currentTitle}}"></x-title>
```

**子级接收父级传过来的值**

```
<!-- 子级js -->
properties: {
        titleText:{
            type:String,
            value:'其他'
        }
    },
```

![image-20211006144753528](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006144753528.png)



## 子组件给父组件传值

把组件稍微修改一下，新增了详情操作按钮，当前通过循环已得出多个模块，现在想在点击详情的时候，子级把当前模块的id传给父级。

![image-20211006152520535](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006152520535.png)



**子组件给父组件传参**

```
<!-- 子级wxml -->
 <view class="title-oper" bindtap="gotoDetail">详情</view>
```

```
<!-- 子级js -->
 gotoDetail(){
    this.triggerEvent('gotoDetail',this.data.titleId)
 }
```

![image-20211006152941044](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006152941044.png)



**父组件接收子组件的参数**

```
<!-- 父级 wxml -->
<x-title titleText="{{item.title}}"
             titleId="{{item.id}}"
             bind:gotoDetail="gotoDetail"></x-title>
```



```
<!-- 父级 js -->
 //通过e.detail获取子组件传过来的参数
gotoDetail(e){ 
    const id = e.detail 
    console.log('从子组件接收到的id',id)
  }  
```



![image-20211006153841068](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006153841068.png)



## 父级调用子组件的方法

子组件定义了一个方法

```
<!-- 子级 js -->
childMethod(){
    console.log('我是子组件的方法')
 },
```



父级先给子组件一个id

```
<!-- 父级 wxml -->
<x-title id="titleCom"></x-title>

<van-button type="primary" bindtap="triggerChildMethod">调用子组件方法</van-button>
```



在js页面的生命周期中获取组件，然后存到我们自定义的变量titleCom中，接着便可直接调用子组件里面的方法了

```
<!-- 父级 js -->
 onReady(){
    this.titleCom = this.selectComponent("#titleCom");
  },
  
triggerChildMethod(){
    this.titleCom.childMethod();
  }  
```

![image-20211006162110270](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006162110270.png)





>**如果this.selectComponent()返回为null**
>
>1、检查wxml定义的id和js使用的是否一致；
>
>2、自定义组件是否渲染，例如你使用了wx:if，导致组件还未渲染



>传值官网相关文档：[地址](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/events.html)



# 在自定义组件中使用插槽（slot）

我们上面在自定义组件中加了【详情】查看的操作按钮，但是有的地方我们可能并不想用文字，想改成图标或者按钮，当某处放置的节点内容不确定时，我们就可以使用插槽来处理。

> 插槽就相当于在子组件中放一个占位符，这样父组件就可以向子组件填充html了。

![image-20211006165249359](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006165249359.png)

## 单插槽

![image-20211006171332866](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006171332866.png)

在子组件加入插槽

```
<!-- 子级 wxml -->
 <slot></slot>
```

父级即可在组件内任意填充内容，比如插入一个图标（如果子级没有加slot，及时填充了html也不会被渲染）

```
<!-- 父级 wxml -->
 <x-title>
 	<view class="oper-wrap">
            <van-icon name="arrow" />
    </view>
 </x-title>

```

![image-20211006170913218](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006170913218.png)



## 多插槽

![image-20211006174523925](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006174523925.png)

先在**子组件**的js开启一下多slot支持

```
 <!-- 子级 js -->
 options: {
        multipleSlots: true // 在组件定义时的选项中启用多slot支持
    },
```



在**子组件**加上插槽需要给插槽加上名字

```
 <!-- 子级 wxml --> 
 <slot name="icon"></slot>
 
  <slot name="oper"></slot>
```



在**父级**使用

```
 <!-- 父级 wxml --> 
 <view class="icon-wrap" slot="icon">
    <van-icon name="orders-o" size="24"/>
 </view>

<view class="oper-wrap"  slot="oper">
   <van-button type="primary" custom-style="{{customStyle}}">更多</van-button>
</view>
 
```





![image-20211006174307449](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006174307449.png)



## 注意

**问：为什么加了插槽，却没有反应？**

![image-20211006175223429](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/06/image-20211006175223429.png)



虽然我只在【子组件】加了1个插槽，但是因为加上了名字，所以同样需要在【子组件】的js里开启多插槽

```
 options: {
        multipleSlots: true // 在组件定义时的选项中启用多slot支持
    },
```



>插槽官网文档：[地址](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/wxml-wxss.html)



# Component的生命周期



```
Component({
  lifetimes: {
    attached: function() {
      // 在组件实例进入页面节点树时执行
    },
    detached: function() {
      // 在组件实例被从页面节点树移除时执行
    },
  },
  //组件所在页面的生命周期
   pageLifetimes: {
    show: function() {
      // 页面被展示
    },
    hide: function() {
      // 页面被隐藏
    },
    resize: function(size) {
      // 页面尺寸变化
    }
  }
  // 以下是旧式的定义方式，可以保持对 <2.2.3 版本基础库的兼容
  attached: function() {
    // 在组件实例进入页面节点树时执行
  },
  detached: function() {
    // 在组件实例被从页面节点树移除时执行
  },
  // ...
})
```



> 生命周期官网：[地址](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/lifetimes.html)




---
title: 小程序引入vant-Weapp保姆级教程及安装过程的问题解决
date: 2021-09-25
tags: 插件
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/6.jpg
summary: vant-Weapp使用教程
---

当你想在小程序里引入vant时，第一步：打开[官方文档](https://vant-contrib.gitee.io/vant-weapp/#/home)，第二步：切到快速上手，然后开始步骤一、步骤二、步骤三？

![image-20210925093852009](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925093852009.png)

你只会看到

![image-20210925094920494](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925094920494.png)



--------------------------以下是正文-------------------------

*如果正准备安装，可以直接跳到下面的【正确的安装姿势】一步一步走，就不会出现问题啦！*

# 问题汇总

可能出现的一些问题汇总

## 问题一：构建npm，提示找不到package.json文件

按官网，步骤一，通过npm安装，这个时候还没问题，但是当你到第四步点击【构建npm】时，就可能出现

![image-20210925104011474](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925104011474.png)

所以在npm安装时，先确保package.json存在，不存在的话先`npm init`初始化一下项目。新建小程序，默认是没有package.json文件的（嗯反正我的没有🤔）





## 问题二：构建npm，未找到miniprogram文件

有package.json文件之后，再次点击【构建npm】，又提示

![image-20210925104048843](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925104048843.png)



如果出现未找到miniprogram的情况，则自行在根目录创建miniprogram解决这个问题。



## 问题三：构建npm成功，但是miniprogram里没东西



![image-20210925113320459](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925113320459.png)

如果是先npm安装了，发现没有package.json再进行创建的话，package.json里并没有你的依赖信息，所以构建为空。

![image-20210925105444951](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925105444951.png)



重新执行`npm i @vant/weapp -S --production`，在点击构建即可

![image-20210925113410473](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925113410473.png)







## 问题四：引入报错

以为终于安装完可以开始用了，但是.....还是报错！！！

![image-20210925101654057](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925101654057.png)



按照快速上手的方法引入组件时，会出现此路径错误



![image-20210901143347733](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/01/image-20210901143347733.png)

官网是这样

![image-20210925101957491](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925101957491.png)

我们需要改成

```
"usingComponents": {
	"van-button": "/miniprogram/miniprogram_npm/@vant/weapp/button/index"
}
```

好了，终于用上了。

![image-20210925105808938](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925105808938.png)





#  正确的安装姿势

我们根据以上错误分析，结合官网步骤，来解锁正确的安装姿势

![image-20210925110006061](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110006061.png)



## 第一步：创建小程序

![image-20210925110213893](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110213893.png)



当前的目录文件是这样的

![image-20210925110325999](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110325999.png)



## 第二步：先执行

```
npm init
```

生成package.json文件，我做测试，就直接一直回车了，这个可根据自己需求配置

![image-20210925110615636](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110615636.png)



## 第三步：通过npm安装（官网步骤一）

```
npm i @vant/weapp -S --production
```

![image-20210925110705708](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110705708.png)

## 第四步： 修改 app.json（官网步骤二）

将 app.json 中的 `"style": "v2"` 去除，小程序的[新版基础组件](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#style)强行加上了许多样式，难以覆盖，不关闭将造成部分组件样式混乱。

![image-20210925110805809](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925110805809.png)

## 第五步：修改 project.config.json（官网步骤三）

开发者工具创建的项目，`miniprogramRoot` 默认为 `miniprogram`，`package.json` 在其外部，npm 构建无法正常工作。

需要手动在 `project.config.json` 内添加如下配置，使开发者工具可以正确索引到 npm 依赖的位置。

```
{
  ...
  "setting": {
    ...
    "packNpmManually": true,
    "packNpmRelationList": [
      {
        "packageJsonPath": "./package.json",
        "miniprogramNpmDistDir": "./miniprogram/"
      }
    ]
  }
}
```

![image-20210925111000290](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111000290.png)





>注意： 由于目前新版开发者工具创建的小程序目录文件结构问题，npm构建的文件目录为miniprogram_npm，并且开发工具会默认在当前目录下创建miniprogram_npm的文件名，所以新版本的miniprogramNpmDistDir配置为'./'即可

## 第六步：在根目录新增miniprogram文件夹

![image-20210925111128059](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111128059.png)



## 第七步：构建npm包（官网步骤四）

![image-20210925111246836](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111246836.png)





![image-20210925111428355](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111428355.png)



构建完成之后，你会在miniprogram文件看到vant的文件夹，这样代表安装成功，可以开始使用了。

![image-20210925111346825](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111346825.png)





## 第八步：引入使用

在`app.json`或`index.json`中引入组件

```
"usingComponents": {
  "van-button": "/miniprogram/miniprogram_npm/@vant/weapp/button/index"
}
```

![image-20210925111644625](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111644625.png)



然后在wxml就可以开始使用了

![image-20210925111749950](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925111749950.png)



# 结语
如果现在不需要使用那就赶紧收藏一下，万一之后就要用了呢！



![image-20210925113935763](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/09/25/image-20210925113935763.png)

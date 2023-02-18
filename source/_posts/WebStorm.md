---
title: WebStorm提高工作效率的实用配置
date: 2021-10-23
tags: WebStorm
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/7.jpg
summary: 开发效率“狂飙”秘诀
---



## WebStorm打开项目忽略node_modules目录设置

当项目打开比较慢时，可以配置选择不打开node_modules目录，这样可以更快的打开项目

配置路径：  File → Settings → Editor → File Types

![image-20211023145431137](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023145431137.png)





## WebStorm快速定位已打开页面目录的方法

如果你只知道文件名字，想到找到文件的具体位置

![image-20211023144620455](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023144620455.png)

动效展示







## WebStorm解决git冲突

①   路径： VCS →  Git → Resolve conflicts

![image-20211023143831890](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023143831890.png)



## WebStorm打开设置

①   配置路径：  File → Settings

> 设置快捷键 `Ctrl + Alt + S`

![image-20211023133843271](https://gitee.com/Olivivian/PicGoImages/raw/master/img//https/gitee.com/Olivivian/PicGoImages/raw/master/img/https/gitee.com/Olivivian/PicGoImages/raw/master/img/Typora/typora-user-images/2021/10/23/2021/10/23/2021/10/23/image-20211023133843271.png)



## WebStorm自定义文档注释模板

①   配置路径：  File → Settings → Editor → Live Templates

②   找到指定位置新增配置

![image-20211023141223572](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023141223572.png)

如以上配置的效果

![image-20211023141447423](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023141447423.png)

如果想设置**变量**

![image-20211023142148596](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023142148596.png)



效果

![image-20211023142600452](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023142600452.png)





## WebStorm配置微信wxss样式支持

①   配置路径：  File → Settings → Editor →File Types

②  找到添加的地方，输入要支持的文件后缀

```
微信    *.wxss
支付宝  *.acss
```



![image-20211023133822439](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023133822439.png)



## WebStorm编译less并自动生成css/wxss/acss

①   配置路径：File | Settings | Tools | File Watchers | +

![image-20211023134807214](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023134807214.png)



②   配置在**当前目录**生成.css  (如果是微信就改成`.wxss`，支付中改为`.acss`)

```
Arguments：
--no-color $FileName$ $FileNameWithoutExtension$.wxss
# --no-color 禁用彩色的输出
# $FileName$ 当前编辑文件名
# $FileNameWithoutExtension$.css  去除.less扩展名再加上.css扩展名

Output paths to refresh：
$FileNameWithoutExtension$.wxss
# 保存在当前less目录下，并刷新项目结构显示文件出来
```

🍇 *如果想生成到指定文件夹的配置*

```
Arguments：
--no-color $FileName$ $ProjectFileDir$/pages/$FileDirPathFromParent(less)$/$FileNameWithoutExtension$.wxss
# --no-color 禁用彩色的输出
# $FileName$ 当前编辑文件名
# $ProjectFileDir$/pages/$FileDirPathFromParent(less)$/$FileNameWithoutExtension$.css 项目目录/pages/在当前目录找到父目录less的路径/当前编辑文件名去除.less扩展名再加上.css扩展名

Output paths to refresh：
$ProjectFileDir$/pages/$FileDirPathFromParent(less)$/$FileNameWithoutExtension$.css
# 保存在指定的目录下，并刷新项目结构显示文件出来
```



![image-20211023135133368](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/10/23/image-20211023135133368.png)
































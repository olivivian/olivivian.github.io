---
title: Chrome调试技巧
date: 2022-03-03
tags: Chrome
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/1.jpg
summary:  Chrome Devtools的高端玩法
---


# 条件断点

有时你设置的断点是不是被执行了太多次？假设有一个包含 `200` 个元素的循环，但是你只对第 `110` 次循环的结果感兴趣，又或者你只对一些满足某些条件的结果感兴趣，怎么办呢？

```
这样的情况下，你可以设置一个条件断点：

- 右击行号，选择 Add conditional breakpoint...(添加条件断点)

- 或者右击一个已经设置的断点并且选择 Edit breakpoint(编辑断点)

- 然后输入一个执行结果为 true 或者 false 的表达式（它的值其实不需要完全为 true 或者 false 尽管那个弹出框的描述是这样说的）。
```

![image-20230110184641845](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110184641845.png)

在这个表达式中你可以使用任何这段代码可以获取到的值（当前行的作用域）。如果条件成立，这个断点就会暂停代码的执行

# 不刷新页面重新请求

如果想要重新请求某个接口，可以不用刷新页面。

```
右键点击接口 > 选择【重放XHR（Replay XHR）】
```

![image-20230111112947708](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230111112947708.png)

# console的使用

## 大括号

假如有这么一堆你想要输出但看起来并不易读的数据，可以把console.log 的参数包装在大括号中

![image-20230110185517848](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110185517848.png)

这样就可以获得一个一个对象，很容易就能知道哪一个值对应哪一个变量

![image-20230110185601700](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110185601700.png)

> ECMAScript 2015 中引入了 enhanced object literal(增强对象文字面量)

## console.table

可以试试用，`console.table`打印对象或者数组

## table + `{}`

![image-20230110185951304](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110185951304.png)

## console.dir

有时候你想要打印一个 `DOM` 节点。 `console.log` 会将这个交互式的元素渲染成像是从 `Elements` 中剪切出来的一样。

如果说想要查看 **这个节点所关联到的真实的js对象** ，并且想要查看他的 **属性** 的话，可以使用`console.dir`

![image-20230110190252801](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110190252801.png)



# 复制 copy

复制控制台打印出来的最新数据

```
copy($_)
```

复制当前网页的html

```
copy($0)
```

# 保存 save

## 存储为一个全局变量（`Store as global` ）

 右键，可以将当前的变量（比如一个对象），转换成一个全局变量，它会创建 一个名为 `temp*` 的变量，第一次叫`temp1`，第二次叫`temp2`。

通过使用这些变量来操作对应的数据，不用再担心影响到他们原来的值。、

## 保存代码片段

控制台还可以用来保存代码片段，在【源代码（Sources）】-【代码段（Snippets）】里面。

![image-20230110181946091](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110181946091.png)

快捷执行保存的代码片段，快捷键打开Command Menu，输入框中输入 `!` ，就可以根据名字来筛选预设代码块。（还可以输入`>`，或者`?`试试其他效果）

```
 Win：[ Ctrl] + [P] 
 
 Mac： [⌘] + [P] 
```



![image-20230110182230231](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110182230231.png)

# Command的使用

利用快捷键调出Command，在 `Chrome` 的调试打开的情况下 按下

```
 Win：[ Ctrl] + [Shift] + [P] 
 
 Mac： [⌘] + [Shift]+ [P] 
```

## 截屏

输入`截图（screenshot）`

1、选中某个节点，可以针对这个节点截图

2、可以自定义区域截图

3、截图整个网页，包括滚动条下面的（长图）

4、截取当前屏幕展示的页面

![image-20230110105204248](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110105204248.png)



## 改变面板布局

输入` 面板布局（layout）`，可以选择想要的布局，一共三种(这里不再显示已经激活的选项)

- 使用水平面板布局
- 使用垂直面板布局
- 使用自动面板布局



![image-20230110110803646](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110110803646.png)



## 切换主题

输入`主题（theme）`，修改控制面板的主题颜色，可选项有`明亮` & `暗黑` 两种

![image-20230110145617726](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110145617726.png)

# 控制台中的符号使用

## 符号👉$

```
$0 对我们当前选中的html节点的引用
$1 对上一次我们选择的节点的引用
$2 对在那之前选择的节点的引用，等等。
一直到 $4

$_ 对上次执行结果的引用，可以用来查看上次的执行结果
```

可以直接在控制台打印试试，如$0会直接打印出当前的节点（还可以尝试做一些相关操作，例如: `$1.appendChild($0)`)）

![image-20230110183233178](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230110183233178.png)



```
$i 引入npm库

1.先安装 Console Importer 插件
2.关闭浏览器重新打开
```

在 [Chrome插件:Console Importer](https://link.juejin.cn/?target=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fconsole-importer%2Fhgajpakhafplebkdljleajgbpdmplhie%2Frelated) 的帮助之下，可以快速的在 `console` 中引入和测试一些 `npm` 库。

运行 `$i('lodash')` 或者 `$i('moment')` 几秒钟后，你就可以获取到 `lodash / momentjs` 了

# 元素面板

## 通过 `'h'` 来隐藏元素

有的时候想要隐藏页面上的元素，我们可以用过给节点手动加样式来实现，其实我们还可以通过使用快捷键来快速实现隐藏元素。

```
在元素面板（Elements）中，
按一下 'h' 就可以隐藏你在元素面板中选择的元素。
再次按下 'h' 可以使它出现。
```

如下示例：它的实现原理就是，给你选中的元素，自动加上一个`__web-inspector-hide-shortcut__`样式

![image-20230111114743797](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230111114743797.png)



## 阴影编辑器

如果是`box-shadow` 属性或者 `text-shadow` 属性，点击阴影方形符号，就会出现一个【阴影编辑器】，可以用来很方便的调试阴影效果

![image-20230111115109452](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230111115109452.png)



# 打开Drawer面板

如果想要在 `Elements` 选项卡打开的同时可以看到 `console` 面板。

可以在 `DevTools`（任何选项卡）中时，按 `[esc]` 来显示它，再次按 `[esc]` 隐藏它。

> 点击【控制台】旁边的三个点，还可以展示更多功能。

![image-20230111115752145](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230111115752145.png)




















































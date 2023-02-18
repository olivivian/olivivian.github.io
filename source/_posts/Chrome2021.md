---
title: 一起来看看2021谷歌浏览器开发者工具都更新了哪些值得关注的新功能
date: 2021-10-13
tags: Chrome
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/8.jpg
summary: Chrome新功能
---


谷歌浏览器一直在提示更新，提示了好久，一直没更，最近终于给它更到最新版本了，一起来看看都更了些啥吧！

当前最新版本：Chrome 94


# 1、设定你的 DevTools 用户界面语言

Chrome DevTools 现在支持超过 80 种语言，允许您设定自己喜欢的语言！

- 打开[设置](https://developer.chrome.com/zh/docs/devtools/customize/#settings)，然后点击**偏好**下的**语言**下拉菜单。（拉到最后是【中文】）

- 选择自己喜欢的语言后，重新加载 DevTools（就是把控制台关掉，在打开）。

![image-20211013001403903](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013001403903.png)



> 都没注意过，之前不能直接设置其他语言吗？🧐



# 2、帧（Frame）详情页获取 origin trials 信息

你现在可以从**应用**面板的帧（frame）详情页那里获取网站的 origin trials 信息。Origin trials允许你提前尝试正处于实验阶段的新功能。通过注册参加 Origin trials， 你就可以在该新功能还未放给所有用户之前， 利用该功能进行限时的产品开发。



打开有注册参加 origin trials 的网页(参考 [demo 页面](https://mediastreamtrack.glitch.me/))。在**应用**面板那里，滚动至**帧**区域，选中 top frame。

![image-20211013001506590](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013001506590.png)



# 3、设备列表新增 Nest Hub 设备

您现在可以在[设备模式](https://developer.chrome.com/zh/docs/devtools/device-mode/)下模拟 Nest Hub 以及 Nest Hub Max 的尺寸。

点击 [切换设备工具栏图标](https://developer.chrome.com/zh/docs/devtools/device-mode/#viewport)  ![切换设备工具栏](https://wd.imgix.net/image/admin/9FiBHFCzfPgP8sy6LMx7.png?auto=format) ，在**设备列表**里选择 Nest Hub 或者 Nest Hub Max 设备。

![image-20211013001608400](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013001608400.png)





> Nest Hub 是什么？

Nest Hub是一个集成的智能显示，它与智能家居配件一起工作，播放音乐和视频，并显示您的最新照片。 有了Google助理， Nest Hub还可以让您知道谁在门口，找到您的下一个食谱，控制您的智能灯。

![image-20211012234829256](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/12/image-20211012234829256.png)

# 4、新的 CSS 容器查询（Container queries）徽章

DevTools 在容器元素（Container elements，指的是那些匹配 `@container` @规则的祖先元素）的旁边，新增了**容器**徽章。点击该徽章，网页将突出显示选中容器元素，以及该容器所有的后代元素。

![image-20211013001828819](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013001828819.png)



# 5、利用新的复选框反转过滤网络请求的条件

你在**网络**面板那里，使用新的**反转**复选框，反转过滤条件。

比如我示例中，过滤文本框输入`status-code:200`，看到的是状态码为 200的网络请求。

点了反转，状态码不是200的就被过滤出来了

![image-20211013011157642](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013011157642.png)



![image-20211013002151598](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013002151598.png)



# 6、 控制台的边栏即将被弃用

控制台的左边栏将会被移除。该边栏里的过滤界面将会被移动到工具栏里。

![image-20211013002733498](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013002733498.png)



# 7、在问题选项卡以及网络面板那里显示原生 `Set-Cookie` 响应头

DevTools 现在可以在**问题**选项卡那里显示原生（raw） `Set-Cookie` 响应头（response headers）。

此前，DevTools 并不会在**网络**面板那里显示异常 cookie（不正确的 `Set-Cookie` 响应头）。

现在，通过**网络**面板新增的 `response-header-set-cookie` 过滤条件，用户可以过滤掉含有原生 `Set-Cookie` 的响应。DevTools 也会把**问题**选项卡里面的原生 `Set-Cookie` 响应头给链接到**网络**面板。

![image-20211013002920946](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013002920946.png)



# 8、在控制台里显示原生访问器为自己的属性

**控制台**现在会将原生访问器（native accessors）始终显示为它们自己的属性（own properties）。

例如说，此前在**控制台**计算 `new Int8Array([1, 2, 3])` 表达式时，原生访问器（如 length、byteOffset）并没有在预览中展示。经过这次更新，原生访问器会在预览中展示，并且在展开时会提前计算出结果。

![image-20211013003036442](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013003036442.png)



# 9、正确输出带有 #sourceURL 行内脚本的错误堆栈信息

DevTools 现在可以正确解析带有 #sourceURL 的内联脚本（inline scripts），并且还能针对调试这种情况，输出正确的错误堆栈信息。

此前，DevTools 会错误输出带有 #sourceURL 的内联脚本的位置信息。这是由于之前的位置输出是对应该 #sourceURL 所在的 `<script>` 标签。正确的位置输出应该是要对应该文档。

![image-20211013003821612](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013003821612.png)



# 10、更改计算样式边栏里面元素的颜色格式

现在可以通过 Shift + 点击**颜色预览**，来更改**计算样式**边栏里的元素颜色格式。

![image-20211013004655726](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013004655726.png)



# 11、使用原生的 HTML 提示框替换自定义提示框

DevTools 现在针对所有的组件都采用原生 HTML 提示框，此前，DevTools 一直都是使用内部开发的自定义提示框，这是碍于原生的 HTML 提示框缺乏自定义风格（Styling）支持，因此 DevTools 使用自定义提示框的支持。

不幸的是，维护自定义提示框的实现是一件很棘手的事。我们经常会遇到一些很复杂的 bugs。

在重新评估自定义提示框带来的好处之后，我们认为原生的 HTML 提示框对于 DevTools 来说已经足够了。采用原生提示框可以避免用户遇到各式各样的问题。

![image-20211013011316889](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013011316889.png)



# 其他

## 想看当前浏览器的版本

![image-20211013005943861](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013005943861.png)

## 想看当前版本更新了什么

![image-20211013010305756](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/13/image-20211013010305756.png)





参考资料

[developer.chrome](https://developer.chrome.com/tags/new-in-devtools/)


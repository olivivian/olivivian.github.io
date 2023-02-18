---
title: 原来个性化定制github主页这么简单？
date: 2023-01-07
tags: github
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/13.jpg
summary: 装饰你的github主页
---

## 新建仓库

先创建一个和用户名同名的仓库。（关键一步）

![image-20221126093236216](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221126093236216.png)



仓库设置为`Public`，选择添加` README`，点击创建仓库。

![image-20221126093348740](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221126093348740.png)

创建好之后，点击编辑

![image-20221126101508543](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221126101508543.png)



## 页面定制

打开文件，可以看到，github有给出一些默认的欢迎内容，可以解开注释进行使用

![image-20221126101545781](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221126101545781.png)



## 个性化定制

### 增加徽标

![image-20230107113711175](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107113711175.png)

生成网站  https://shields.io/

可以自定义颜色，内容，再嵌套`a`标签即可实现点击跳转至对应网站的效果

```
最简单的写法
https://img.shields.io/badge/+内容+颜色

示例
https://img.shields.io/badge/Blog-brightgreen

<img src="https://img.shields.io/badge/-HTML5-E34F26?style=flat-square&logo=html5&logoColor=white" />
<img src="https://img.shields.io/badge/-CSS3-1572B6?style=flat-square&logo=css3" />
<img src="https://img.shields.io/badge/-JavaScript-oringe?style=flat-square&logo=javascript" />
```



### GitHub 资料奖杯

添加奖杯信息  https://github.com/ryo-ma/github-profile-trophy/

![image-20230107142924939](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107142924939.png)



```
![trophy](https://github-profile-trophy.vercel.app/?username=xxx)
```

- 通过`title`指定显示的内容：`&title=Stars,Followers`
- 通过`rank`过滤指定内容：`&rank=S,AAA`
- 设定行和列的大小：`&row=2&column=3`
- 主题设定：`&theme=flat` （[可用主题参考](https://github.com/ryo-ma/github-profile-trophy/#flat)官方提供）
- 边缘间隔：`margin-w=15`（宽度间隔）、`margin-h=15`（高度间隔）
- 透明背景：Transparent background：`&no-bg=true`





### 网站数据卡片

在 README 中展示其他网站数据，也可用于网站状态监控   https://github.com/songquanpeng/stats-cards

当前支持：知乎、B 站、 LeetCode、掘金、牛客、CSDN、GitHub

![image-20230107115515087](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107115515087.png)

```
![](https://stats.justsong.cn/api/csdn?id=CSDN用户名&theme=dark)
![](https://stats.justsong.cn/api/bilibili/?id=B站用户ID&theme=dark)
```



### GitHub Readme Stats

可以让在Github主页显示你的统计信息，且可以自定义主题，效果如下：

![image-20230107114940719](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107114940719.png)

```
![](https://github-readme-stats.vercel.app/api?username=你的用户名&show_icons=true&theme=dark&count_private=true)
```

显示语言统计

![image-20230107115036338](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107115036338.png)

```
![](https://github-readme-stats.vercel.app/api/top-langs/?username=你的用户名&theme=dark&layout=compact)
```

> 更多👉[GitHub Readme Stats](https://github.com/anuraghazra/github-readme-stats/blob/master/docs/readme_cn.md)



### visitor badge

显示访问量功能的组件  https://visitor-badge.glitch.me/

![image-20230107115234900](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107115234900.png)

```
<img src="https://visitor-badge.glitch.me/badge?page_id=Github主页地址&right_color=red" />
```



### Github Readme Activity Graph

显示Github活动统计图  https://github.com/Ashutosh00710/github-readme-activity-graph

![image-20230107115348309](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107115348309.png)

```
![](https://activity-graph.herokuapp.com/graph?username=你的Github用户名&theme=github)
```



### GitHub 连续打卡

在 README 中展示连续提交代码的次数    https://github.com/DenverCoder1/github-readme-streak-stats

![image-20230107143518834](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107143518834.png)



### Readme Typing SVG

文字动态输入输出   https://github.com/DenverCoder1/readme-typing-svg

```
//Markdown
[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&width=435&lines=The+five+boxing+wizards+jump+quickly)](https://git.io/typing-svg)

//HTML
<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&width=435&lines=The+five+boxing+wizards+jump+quickly" alt="Typing SVG" /></a>
```



### GitHub 信息统计

打开网站 https://metrics.lecoq.io/

输入你的 GitHub ID，稍等一会，就会返回右侧所有和你相关的数据

![image-20230107144700237](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230107144700237.png)

> [metris github地址](https://github.com/lowlighter/metrics#-documentation)

## 优秀案例

https://github.com/abhisheknaiidu/awesome-github-profile-readme














---
title: vuepress搭建文档库
date:  2022-05-06
tags: vuepress
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/12.jpg
summary:  vuepress搭建文档库
---

# 安装

1）新建一个工程文件

2）安装本地依赖

```
yarn add -D vuepress 
或
npm install -D vuepress
```

>  注：官方不再推荐全局安装 npm install -g vuepress

3）初始化项目

```
yarn init -y 
或
npm init -y (-y免去确认)
```

初始化成功后，会创建一个`package.json`文件

```
{
  "name": "y",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
     "vuepress": "^1.9.7"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

4）修改 package.json 里面的 scripts，方便运行

```
 "scripts": {
    "docs:dev": "vuepress dev docs --temp .temp",
    "docs:build": "vuepress build docs"
  },
```

>  注：启动脚本docs:dev 键值可以自定义修改，此处是为了和一些项目中默认脚本中自带的 dev 区分开，都是等效于执行vuepress dev doc，根据你目录中的.vuepress配置项和docs下的所有.md/.html文件做一个项目的编译和打包。

加` --temp .temp `是为了vuepress可以进行热更新，使用了这个命令 vuepress 会生成一个临时文件夹 .temp，需要在 .gitignore 中忽略掉该文件夹：

```
# vuepress temp file
.temp
```





# 创建第一篇文档

1）在工程文件创建一个 `docs` 文件

2）在`docs` 文件里面创建`README.md`

3）运行

命令行运行

```
yarn docs:dev 
或
npm run docs:dev
```

如果用的webStorm，直接点击运行

![image-20221229154106615](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229154106615.png)

> 👉 [WebStorm提高工作效率的实用配置](https://juejin.cn/post/7022154302621745189)

启动后的效果

![image-20221229154700780](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229154700780.png)

 我们看到的首页，是通过配置根路径下的README.md文件实现的、而导航栏、侧边栏等则是通过配置docs/config.js实现。因为没有配置东西，所以看上去什么都没有，下面就开始来增加配置。



# vuepress目录结构

 VuePress 遵循 **“约定优于配置”** 的原则，推荐的目录结构如下：

```
.
├── docs
│   ├── .vuepress (可选的)  #用于存放全局的配置、组件、静态资源等
│   │   ├── components (可选的)	#该目录中的 Vue 组件将会被自动注册为全局组件。
│   │   ├── theme (可选的)	#用于存放本地主题。
│   │   │   └── Layout.vue	
│   │   ├── public (可选的)	#静态资源目录。
│   │   ├── styles (可选的)	#用于存放样式相关的文件。
│   │   │   ├── index.styl	#将会被自动应用的全局样式文件，会生成在最终的 CSS 文件结尾，具有比默认样式更高的优先级。
│   │   │   └── palette.styl	#用于重写默认颜色常量，或者设置新的 stylus 颜色常量。
│   │   ├── templates (可选的, 谨慎配置)	#存储 HTML 模板文件。
│   │   │   ├── dev.html	#用于开发环境的 HTML 模板文件
│   │   │   └── ssr.html	#构建时基于 Vue SSR 的 HTML 模板文件。
│   │   ├── config.js (可选的)	# 配置文件的入口文件，也可以是 YML 或 toml。
│   │   └── enhanceApp.js (可选的) #客户端应用的增强。
│   │ 
│   ├── README.md
│   ├── guide (一般用户都在这个目录下创建网站指南,当然可以不用)
│   │   └── README.md （指南里面的具体内容）
│   └── config.md
│ 
└── package.json 项目初始化时，根目录下自动生成的配置文件,定义了项目的基本配置信息及需要依赖的各个模块、指定运行脚本命令的npm命令行缩写等。
 
```



# 默认主题设置

## 首页

1） 创建`.vuepress文件夹`， 在.vuepress中创建` public 文件夹`和`config.js 文件`，形成如下结构。这也是最简单的目录格式。

```
project
├─── docs
│   ├── README.md
│   └── .vuepress
│       ├── public
│       └── config.js
└── package.json
```

 

2）官网给默认的主题提供了一个首页（Homepage）的布局。

​    将docs目录下的README.md中的内容替换，并在public目录下放置一张图片，**然后重启**。

> 注：根路径默认的README.md，会被编译成index.html文件。

```
---
home: true
heroImage: /logo.jpg
actionText: 快速上手 →
actionLink: /zh/guide/
features:
- title: 简洁至上
  details: 以 Markdown 为中心的项目结构，以最少的配置帮助你专注于写作。
- title: Vue驱动
  details: 享受 Vue + webpack 的开发体验，在 Markdown 中使用 Vue 组件，同时可以使用 Vue 来开发自定义主题。
- title: 高性能
  details: VuePress 为每个页面预渲染生成静态的 HTML，同时在页面被加载的时候，将作为 SPA 运行。
footer: MIT Licensed | Copyright © 2018-present Evan You
---
```



当前看到的效果是

![image-20221229170511073](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229170511073.png)

接下来修改docs/config.js文件添加一些基本配置

```
module.exports = {
  // 网站的一些基本配置
  // base:配置部署站点的基础路径，后续再介绍
  title: 'JinDoc', // 网站的标题
  description: '前端速查文档（日常实用向）', // 网站的描述，它将会以 <meta> 标签渲染到当前页面的 HTML 中。
  head: [
    ['link', { rel: 'icon', href: '/logo.gif' }] // 需要被注入到当前页面的 HTML <head> 中的标签
  ],
}
```

实现效果

![image-20221229174834780](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229174834780.png)

## 导航栏

### 1）配置导航栏Logo

```
//修改 .vuepress/config.js
 
module.exports = {
  themeConfig: {
    logo: '/dh_logo.png',
  }
}
```

![image-20221229180135683](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229180135683.png)

### 2）导航栏链接

通过 `themeConfig.nav` 增加一些导航栏链接。

```
// 导航栏链接(themeConfig.nav)
module.exports = {
  themeConfig: {
    logo: '/dh_logo.png',
    nav: [
      { text: 'Home', link: '/' },
      // 可指定链接跳转模式：默认target: '_blank'新窗口打开，_self当前窗口打开
      { text: '百度', link: 'https://www.baidu.com' },
      { text: '谷歌', link: 'https://www.google.com', target: '_blank' },
      { text: 'bing', link: 'https://cn.bing.com', target: '_self', rel: '' },
      // 支持嵌套,形成下拉式的导航菜单
      {
        text: '语言',
        ariaLabel: 'Language Menu',
        items: [
          { text: '中文', link: '/language/chinese/' },
          { text: '英文', link: '/language/english/' }
        ]
      }
    ],
  }
}
```

![image-20221229180611319](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221229180611319.png)

### 3）侧边栏

想要使侧边栏（sidebar）生效，需要配置 themeConfig.sidebar。sidebar可以分为全局设置以及局部设置。

- 如果所有页面都需要侧边栏，则在`.vuepress/config.js`里配置。

```
  在.vuepress/config.js中配置属性：sidebar: 'auto'
```

- 如果只有部分页面需要，则在需要的页面配置（注释或删除**`.vuepress/config.js中`**sidebar: 'auto'属性）

```
在md文件的顶部写上下面代码：

# 自动补充侧边栏
---
sidebar: auto
---
 
# 禁用侧边栏
---
sidebar: false
---
```



### 4）设置侧边栏标题显示的层数。

默认情况下，侧边栏会自动显示当前页面的标题(h2~h3)组成的链接，想要改变深度可以通过在配置文件中配置`themeConfig.sidebarDepth`来设置嵌套层级

 sidebarDepth可设置的值：

```
0-禁用标题（headers）链接
1-默认值,只显示h2的标题
2-可设置的最大值，再大无效, 同时提取h2和h3标题
```

> 注：如果设置了` sidebar: 'auto' `,侧边栏会显示`h2`和`h3`标题，此时sidebarDepth的值只有0是生效的(仅显示`h2`的标题)

```
...
sidebar: 'auto',
// 设置深度，使用了sidebar: 'auto'的话只有设置0才会生效，否则默认2
sidebarDepth: 0,
...
```



# 问题及处理

1、打包时报错

检查配置文件config.js，是否配置正确（路径及标点符号），或者换一个主题试试



参考资料：

vuepress官网：https://vuepress.vuejs.org/zh/

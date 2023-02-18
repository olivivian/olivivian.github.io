---
title: CSS命名规范
date: 2019-05-03
tags: CSS
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/2.jpg
summary:  CSS命名规范之BEM 命名规范
---

# BEM 命名规范

需要明确关联性的模块关系时，才使用 BEM 格式（层级不要超过4级）

Bem 是

- 块（block）

  >  块里面不写样式
  >
  > header`, `container`, `menu`, `checkbox`, `input

- 元素（element）

  > 双下划线  块__ 元素
  >
  > menu item`, `list item`, `checkbox caption`, `header title

- 修饰符（modifier）

  > 双中划线  快/元素--修饰符 
  >
  > disabled`, `highlighted`, `checked`, `select，fixed`, `size big`, `color yellow，primary



自定义规则

- 其他

- > 单中划线     快/元素 - 单词



```html
.article{}
.article__body{}
.article__button--primary{}
.article__button--success{}
<div class="article">
    <div class="article__body">
        <div class="tag"></div>
        <button class="article__button--primary"></button>
        <button class="article__button--success"></button>
    </div>
</div>
```



```html
form { }
.form--theme-xmas { }
.form--simple { }
.form__input { }
.form__submit { }
.form__submit--disabled { }

//对应的HTML结构如下：
<form class="form form--theme-xmas form--simple">
  <input class="form__input" type="text" />
  <input
    class="form__submit form__submit--disabled"
    type="submit" />
</form>
```





单独的公共样式，不需要使用BEM

```CSS 
.hide {
    display: none !important;
}
```





每一个块(block)名应该有一个命名空间（前缀）

- `block` 代表了更高级别的抽象或组件。
- `block__element` 代表 .block 的后代，用于形成一个完整的 .block 的整体。
- `block--modifier` 代表 .block 的不同状态或不同版本。 使用两个连字符和下划线而不是一个，是为了让你自己的块可以用单个连字符来界定



> Bem 是块（block）、元素（element）、修饰符（modifier）的简写，由 Yandex 团队提出的一种前端 CSS 命名方法论。
>
> - \- 中划线 ：仅作为连字符使用，表示某个**块**或者某个**子元素**的多单词之间的连接记号。
> - __ 双下划线：双下划线用来连接**块和块**的**子元素**
> - _ 单下划线：单下划线用来描述一个**块**或者块的**子元素**的一种状态



# 规范列表

[京东规范](https://guide.aotu.io/index.html)

[ES6编程风格](https://es6.ruanyifeng.com/#docs/style)

---
title: 
date: 2021-09-06 00:40
tags: web安全
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/12.jpg
summary: web开发安全之网站都是怎么被攻击的？
---

在互联网时代，数据安全和个人隐私一直都是大家很关心的问题，怎么才能更好的保护我们的数据呢？俗话说要知己知彼才能百战不殆，所以先来了解一下Web安全中的各种攻击的类型及原理吧！🤗



# 前言

看完本篇你将收获（内容有点多，建议**收藏⭐**在看）

- 前端安全大部分的攻击类型及原型解析

具体如图👇



![image-20210905154811350](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/09/05/image-20210905154811350.png)

# Cross-Site Scripting(XSS)

跨站脚本攻击（XSS），攻击者把他们的脚本恶意的插到我们的页面执行



![image-20210903203022807](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/Typora/typora-user-images/2021/09/03/image-20210903203022807.png)

**XSS的一些特点**

- 通常难以从UI上感知(暗地执行脚本)
- 窃取用户信息(cookie/token)，在用户不知情的情况下，发送恶意请求。
- 绘制UI (例如弹窗)，诱骗用户点击/填写表单



**XSS原理**

攻击者往Web页面插入恶意可执行网页脚本代码，当用户浏览该页面时，恶意脚本被执行，从而盗取用户信息或侵犯用户其他安全隐私



## Stored XSS

**存储型攻击**

- 恶意脚本被存在数据库中
- 访问页面→读数据==被攻击
- 危害最大，对全部用户可见

一般存在于 Form 表单提交等交互功能，如文章留言，提交文本信息等，攻击者利用XSS漏洞，将内容经正常功能提交进入数据库持久保存，当前端页面获得后端从数据库中读出的注入代码时，恰好将其渲染执行。

![image-20210904153932547](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904153932547.png)



就以掘金的评论功能举例，假如它存在存储的 XSS 漏洞，我在某篇文章下面输入以下评论，网站将会显示我输入的内容。如果评论文本包含 HTML 标签，它们将被添加到网页的源代码中；特别是，任何脚本标签都会在页面加载时运行。



![image-20210904143510982](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904143510982.png)



这样，当其他人加载带有我这个评论的页面时，我的脚本标签都会运行并窃取其他用户的授权 cookie，将其发送到我指定的服务器进行收集。（很明显掘金是有做防御的，所以什么都没有发生。🧐）



这只是简单的举个例子，XSS攻击也不是这么容易成功的，它需要满足

- POST 请求提交表单后端没做转义直接入库。

- 后端从数据库中取出数据没做转义直接输出给前端。

- 前端拿到后端数据没做转义直接渲染成 DOM。

  



## Reflected XSS

反射型攻击（又名非持久型）

- 不涉及数据库
- 从URL上攻击

![image-20210904154116682](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904154116682.png)



来看一个实例，

现在页面上有一个输入框，用来提交姓名，提交到服务器端时，服务器立即解析并且直接渲染到页面上。

![image-20210904120554945](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904120554945.png)



假如没有做任何防护，我们就可以直接通过这个输入框注入脚本，完成一次XSS攻击

![image-20210904121908119](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904121908119.png)

当前我直接输入了script脚本，提交的时候，脚本被执行了，单单这样看好像没看出有什么危害🤔

那我们换个写法，现在已知这个地址接受name参数，并且无任何防护，如果我们现在给name注入这么一段代码

![image-20210905231910960](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905231910960.png)

然后用户点击了我们改造的这个链接会发生什么？

它就会获取用户的所有 cookie，并且发送到 www.cgisecurity.com/cgi-bin/cookie.cgi这个地址，这样该用户的所有信息就被别人窃取到了。

> 如果直接在浏览器测试，script可能不会生效，因为现在大部分浏览器都会针对`script`等一些危险标签的插入会做拦截过滤，你可以这样改写
>
> ![image-20210905231942747](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905231942747.png)
> 
> 因为是插入一张图片，浏览器一般不会过滤拦截，然后把`src`置空使其触发`onerror`事件，恶意脚本就会间接地被执行；





>反射攻击是指注入的脚本从 Web 服务器反射出来的攻击，例如错误消息、搜索结果或任何其他响应，其中包括作为请求的一部分发送到服务器的部分或全部输入。反射攻击通过另一条路径传递给受害者，例如在电子邮件中或在其他网站上。当用户被诱骗点击恶意链接、提交特制表单，甚至只是浏览恶意站点时，注入的代码会传播到易受攻击的网站，从而将攻击反映回用户的浏览器。然后浏览器执行代码，因为它来自“受信任的”服务器。
>
>反射型XSS攻击的特点在于即时性，它不需要存储在服务器中，通过巧妙地构造一个带恶意代码的URL，然后引导用户点击访问，即可实现攻击



## DOM-based XSS

基于DOM

- 不需要服务器的参与
- 恶意攻击的发起+执行，全在浏览器完成



还是先来看一个例子，假设以下代码用于创建一个表单，让用户选择他们喜欢的语言。查询字符串中还提供了默认语言，作为参数“default”。

![image-20210905232008016](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232008016.png)

![image-20210905210650632](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905210650632.png)

该页面是使用 URL 调用的，例如：

![image-20210905232025458](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232025458.png)

针对该页面的基于 DOM 的 XSS 攻击可以通过向受害者发送以下 URL 来完成：

![image-20210905232039405](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232039405.png)

当受害者点击这个链接时，浏览器会发送一个请求：

![image-20210905232052579](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232052579.png)

到 www.some.site。服务器以包含上述 Javascript 代码的页面进行响应。浏览器为页面创建一个 DOM 对象，其中 document.location 对象包含字符串：

![image-20210905232105798](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232105798.png)

页面中的原始 Javascript 代码不希望默认参数包含 HTML 标记，因此它只是在运行时对其进行解码并将其回显到页面 (DOM) 中。然后浏览器呈现结果页面并执行攻击者的脚本：

![image-20210905232118412](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232118412.png)

看到这里是不是觉得，这不是和上面的反射性一样吗？🤨

首先从两个示例的链接来看,结构完全一样，但是如果我们这样改造一下，把`？号`改成`#号`

![image-20210905232159500](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232159500.png)

在尝试执行，会发现，Reflected XSS（反射型）不在生效，而DOM-based XSS（基于DOM）的攻击依然生效。



>浏览器不会将 URI 片段（URI 中“#”之后的部分）发送到服务器



## Reflected XSS 和DOM-based XSS的区别

Reflected XSS（反射型）和DOM-based XSS（基于DOM）的区别就是完成注入脚本的地方不同，在基于 DOM 的 XSS 攻击中，恶意数据不会触及 Web 服务器。相反，它由 JavaScript 代码完全反映在客户端。

![image-20210903203703407](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/03/image-20210903203703407.png)

## Mutation-based XSS

突变型XSS，也叫做mXSS

> mutation，突变，来自遗传学的一个单词，gene mutation（即基因突变）

- 利用了浏览器渲染DOM的特性(独特优化)

- 不同浏览器，会有区别(按浏览器进行攻击)



不论是服务器端或客户端的XSS过滤器，都认定过滤后的HTML源代码应该与浏览器所渲染后的HTML代码保持一致，至少不会出现很大的出入。

![image-20210904223150612](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904223150612.png)





然而，如果用户所提供的富文本内容通过javascript代码进入innerHTML属性后，一些意外的变化会使得这个认定不再成立：一串看似没有任何危害的HTML代码，将逃过XSS过滤器的检测，最终进入某个DOM节点的innerHTML中，浏览器的渲染引擎会将本来没有任何危害的HTML代码渲染成具有潜在危险的XSS攻击代码。随后，该段攻击代码，可能会被JS代码中的其它一些流程输出到DOM中或是其它方式被再次渲染，从而导致XSS的执行。



> 这种由于HTML内容进入innerHTML后发生意外变化，而最终导致XSS的攻击流程，被称为突变XSS

![image-20210904160201378](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904160201378.png)



mXSS的几种类型，下面我们挑几个来说，想要了解更多可以看这篇文章👉 [fp170.pdf]( https://cure53.de/fp170.pdf)  

![image-20210904230038546](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904230038546.png)

### 3.1 Backtick Characters breaking Attribute Delimiter Syntax

反引号打破属性边界导致的 mXSS

![image-20210904231020779](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904231020779.png)

可以看到，突变后的形式变成了有效的XSS攻击



### 3.3 Backslashes in CSS Escapes causing StringBoundary Violation

CSS中反斜线转义导致的mXSS



![image-20210904231549813](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904231549813.png)



>在CSS中，允许用\来对字符进行转义，例如：`property: 'v\61 lue'` 表示 `property:'value'`，其中61是字母a的ascii码（16进制）。\后也可以接unicode，例如：\20AC 表示 € 。正常情况下，这种转义不会有问题。
>
>然而，一些现代浏览器打破了 CSS 转义的正确和标准驱动使用所表明的安全承诺。特别是，它发生在访问父元素的innerHTML 属性时。我们观察到一种将转义转换为其规范表示的行为。序列属性：'val\27ue' 将导致innerHTML 表示属性：'val'ue'。攻击者可以通过注入隐藏在正确引用和转义的 CSS 字符串中的任意 CSS 代码来滥用此行为。通过这种方式，可以绕过检查符合标准的有效代码的 HTML 过滤器

### 3.4 Misfit Characters in Entity Representation breaking CSS Strings

CSS中双引号实体或转义导致的mXSS

![image-20210904234016829](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904234016829.png)

>一些浏览器中，使用 CSS 字符串中的字符，渲染引擎将它们转换为单引号，不管这两个字符看起来不相关。 这意味着 \22,
>&quot;, &#x22; 和 &#34; 字符序列将在 innerHTML 访问时转换为 ’ 字符。
>
>只能推测这种令人惊讶的行为的原因。一种可能的解释是：\22 先被解码为 "，但考虑到双引号会闭合掉style属性，所以浏览器渲染引擎将"进一步转变为了'，以避免这种情况的发生。当然，这也意味这，除了 \22，\0022 之外，HTML实体如：
>
>```
>&quot; &#x22; &#34; 
>```
>
>等双引号的表示形式均可导致这类问题。



### 3.5 CSS Escapes in Property Names violating entire HTML Structure

CSS属性名中的转义所导致的mXSS

![image-20210904235230335](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/04/image-20210904235230335.png)

>之前说的都是在 CSS 属性值中的一些情况，如果是在CSS 属性名称中使用，也会迫使一些浏览器进入完全不同的行为；
>
>可以看到，我们用转义的内容，嵌入到font-family的属性名中，突变后，\22被解码回双引号，并且闭合掉了style属性，从而我们可以通过onload事件执行javascript代码，需要注意的是，=号，括号等也需要被写为转义形式。我们亦可在\22后加上\3e来闭合掉img标签，并在此之后插入自己的HTML标签。



> Mutation-based XSS攻击示例节选译自以下文档（英文好的建议自行阅读原文，如有错误请在评论区指出）
>
> 👉 [fp170.pdf]( https://cure53.de/fp170.pdf)  
>
> 👉[mXSS Attacks: Attacking well-secured Web-Applications by using innerHTML Mutations](https://cure53.de/fp170.pdf)





# Cross Site Request Forgery (CSRF)

跨站请求伪造

CSRF 是一种诱骗受害者提交恶意请求的攻击。它继承了受害者的身份和特权以代表【受害者】执行不需要的功能。



**CSRF特点**

- 在用户不知情的前提下
- 利用用户权限(cookie)
- 构造指定HTTP 请求，窃取或修改用户敏感信息



**CSRF的攻击流程**

![image-20210905010637766](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905010637766.png)



**举个例子**

用户收到了一封邮件，邮件中有一个链接，用户点击链接，跳转到了恶意的页面B，在恶意页面B中向A发了一个请求，此时这个请求会带有域名A特有的Cookie，域名A所在的服务器接受到这个请求之后，去验证这个Cookie，发现是合法用户，则进行了下一步请求，返回了成功的结果。

在这整个过程中

- 用户没有访问页面A
- 页面A中的特定接口被请求
- 请求执行成功

这就是跨站伪造请求



![image-20210903205030750](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/03/image-20210903205030750.png)



## GET类型的CSRF

**举个例子**

假如应用程序设计为主要使用 GET 请求来传输参数和执行操作，则汇款操作可能会简化为如下请求

![image-20210905232220622](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232220622.png)

【hacker😈】现在决定使用【张三😇】作为受害者来利用此 Web 应用程序漏洞。【hacker】 首先利用漏洞来构建以下 URL，该 URL 将从【张三】的账户转移 100,000 元到 【hacker】 的账户。【hacker】使用原始命令 URL 并将收款人名称替换为自己，同时显着提高了转账金额：

![image-20210905232233680](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232233680.png)

当【张三】登录到银行应用程序时，诱导他来点击恶意的URL，通常会这样做

- 发送带有 HTML 内容的未经请求的电子邮件
- 在受害者在进行网上银行业务时可能访问的页面上植入漏洞利用 URL 或脚本

漏洞利用 URL 可以伪装成一个普通的链接，鼓励受害者点击它，如伪装成一个抽奖链接

![image-20210905232246808](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232246808.png)

或者作为 0x0 假图像发送给【张三】

![image-20210905232304499](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232304499.png)

如果此图像标签包含在电子邮件中，【张三】将看不到任何内容。但是，浏览器*仍会*向 bank.com 提交汇款请求，在【张三】毫不知情的情况下，他的钱就被转走啦！🥶



## POST类型的CSRF

GET 和 POST 攻击之间的唯一区别是受害者如何执行攻击。假设银行现在使用 POST 并且易受攻击的请求如下所示：

![image-20210905232316001](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232316001.png)

此类请求无法通过a标签链接 或 IMG 标签传递，但可以使用 FORM 标签传递：

![image-20210905232326918](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232326918.png)

这个表单将要求用户单击提交按钮，但这也可以使用 JavaScript 自动执行：

![image-20210905232341528](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232341528.png)

这样在受害者不知情的情况下，钱又被转走啦！🥶🥶🥶



## 与 xss 区别

- 通常来说 CSRF 是由 XSS 实现的，CSRF 时常也被称为XSRF（CSRF 实现的方式还可以是直接通过命令行发起请求等）。
- 本质上讲，XSS 是代码注入问题，CSRF 是 HTTP 问题。XSS 是内容没有过滤导致浏览器将攻击者的输入当代码执行。CSRF 则是因为浏览器在发送 HTTP 请求时候自动带上 cookie，而一般网站的 session 都存在 cookie里面。





# Injection

注入

## SQL Injection

所谓 SQL 注入，就是通过把 SQL 命令插入到 Web 表单提交或页面请求的查询字符串，最终执行恶意的 SQL 命令。

![image-20210903211351360](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/03/image-20210903211351360.png)

以常用的登录为例，表单代码如下

![image-20210905232355409](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232355409.png)

后端的 SQL 语句可能是这样的

![image-20210905232407080](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232407080.png)

但如果有一个恶意攻击者输入的用户名是 `admin' --`，密码随意输入，就可以直接登入系统了，为什么？

因为本来预想的SQL 语句是

![image-20210905232419995](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232419995.png)

但是恶意攻击者用奇怪用户名将你的 SQL 语句变成了如下形式

![image-20210905232431571](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232431571.png)

在 SQL 中,`' --`是闭合和注释的意思，-- 是注释后面的内容的意思，所以查询语句就变成了

![image-20210905232446277](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232446277.png)





  ## Injection不止于SQL

除了SQL的注入，还有可能是通过一些命令注入攻击，如

- CLl
- OS command
- Server- Side Request Forgery(SSRF)，服务端伪造请求
  - 严格而言，SSRF不是injection,但是原理类似

命令注入攻击可以向Shell发送命令，让Windows或Linux操作系统的命令行启动程序。也就是说，通过命令注入攻击可执行操作系统上安装着的各种程序。

假如需要实现一个需求：用户提交一些内容到服务器，然后在服务器执行一些系统命令去返回一个结果给用户

![image-20210905232506517](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905232506517.png)

如果 `params.repo` 传入的是 `https://github.com/admin/admin.github.io.git` 确实能从指定的 git repo 上下载到想要的代码。 但是如果 `params.repo` 传入的是 `https://github.com/xx/xx.git && rm -rf /* &&`， 恰好你的服务是用 root 权限起的就糟糕了。





# Denial of Service(DoS)

DoS(Denial of Service)，即拒绝服务，造成远程服务器拒绝服务的行为被称为DoS攻击。其目的是使计算机或网络无法提供正常的服务



> 通过某种方式(构造特定请求)，导致服务器资源被显著消耗，来不及响应更多请求，导致请求挤压，进而雪崩效应。



## ReDoS:基于正则表达式的DoS

根据正则的贪婪模式特性构造正则表达式，使其因为一直匹配不上，导致接口的响应时间变长

![image-20210903212045717](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/03/image-20210903212045717.png)





# Distributed DoS(DDoS)

DDOS(Distributed Denial of Service)攻击全称分布式拒绝服务。是DoS攻击的一种方法。



指借助于客户/服务器技术，将多个计算机联合起来作为攻击平台，对一个或多个目标发动DDoS攻击，从而成倍地提高拒绝服务攻击的威力。阻止合法用户对正常网络资源的访问，从而达成攻击者不可告人的目的。DDoS的攻击策略侧重于通过很多“僵尸主机”，向受害主机发送大量看似合法的网络包，从而造成网络阻塞或服务器资源耗尽而导致拒绝服务。



> 即短时间内，来自大量僵尸设备的请求流量，服务器不能及时完成全部请求，导致请求堆积，进而雪崩效应，无法响应新请求。

攻击特点

- 直接访问IP
- 任意API
- 消耗大量带宽(耗尽)

## SYN 攻击

属于 DDOS 攻击中的一种具体表现形式。

在三次握手过程中，服务器发送 SYN-ACK 之后，收到客户端的 ACK 之前的 TCP 连接称为半连接(half-open connect)。此时服务器处于 SYN_RCVD 状态。当收到 ACK 后，服务器才能转入 ESTABLISHED 状态.

SYN 攻击指的是，攻击客户端在短时间内伪造大量不存在的 IP 地址，向服务器不断地发送 SYN 包，服务器回复确认包，并等待客户的确认。

由于源地址是不存在的，服务器需要不断的重发直至超时，这些伪造的 SYN 包将长时间占用未连接队列，正常的 SYN 请求被丢弃，导致目标系统运行缓慢，严重者会引起网络堵塞甚至系统瘫痪。

![image-20210903212508238](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/03/image-20210903212508238.png)

**打个比方**

一群恶霸试图让对面那家有着竞争关系的商铺无法正常营业，他们会采取什么手段呢？（只为举例，切勿模仿）

![image-20210905021614078](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905021614078.png)

恶霸们扮作普通客户一直拥挤在对手的商铺，赖着不走，真正的购物者却无法进入；或者总是和营业员有一搭没一搭的东扯西扯，让工作人员不能正常服务客户；也可以为商铺的经营者提供虚假信息，商铺的上上下下忙成一团之后却发现都是一场空，最终跑了真正的大客户，损失惨重。

![image-20210905021944509](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905021944509.png)

此外恶霸们完成这些坏事有时凭单干难以完成，需要叫上很多人一起。网络安全领域中 DoS 和 DDoS 攻击就遵循着这些思路。



# 传输层(MITM*攻击*)

中间人攻击(Man-in-the-MiddleAttack，简称“MITM*攻击*”)。

是指攻击者与通讯的两端分别创建独立的联系，并交换其所收到的数据，使通讯的两端认为他们正在通过一个私密的连接与对方 直接对话，但事实上整个会话都被攻击者完全控制。在中间人攻 击中，攻击者可以拦截通讯双方的通话并插入新的内容。

> 直白的说就是，浏览器和服务器彼此以为在互相沟通，但实际上有一个中间人在里面插了插了一脚，窃取了信息或者修改了请求等。

![image-20210905145019218](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905145019218.png)



**用日常生活的写信来类比的话**：

你给朋友写了一封信，邮递员可以把每一份你寄出去的信都拆开看，甚至把信的内容改掉，然后重新封起来，再寄出去给你的朋友。

朋友收到信之后给你回信，邮递员又可以拆开看，看完随便改，改完封好再送到你手上。

你全程都不知道自己寄出去的信和收到的信都经过邮递员这个“中间人”转手和处理

——换句话说，对于你和你朋友来讲，邮递员这个“中间人”角色是不可见的。



**中间人攻击类型大致有**

- Wi-Fi欺骗，*攻击者创建与本地免费Wi-Fi同名的虚假Wi-Fi接入点*
- HTTPS欺骗，*攻击者通过欺骗我们的浏览器，让我们认为自己访问的是可信任站点*
- SSL劫持，*当我们尝试连接或访问不安全的HTTP://站点时，浏览器会自己重定向到安全的HTTPS://处。这个时候攻击者就可以劫持这个重定向的过程，将其指向自建服务器的链接植入其中*
- DNS欺骗，*使浏览器URL转化异常，从而访问一些恶意的地址*
- 电子邮件劫持



**为什么中间人可以进行这种攻击？**

1、请求的所有的信息都是明文传输的，谁都可见

2、请求信息被篡改时，接收方并不知道

3、双方并没有对彼此的身份进行未验证



# 总结

**跨站脚本攻击（XSS）**，即攻击者把他们的脚本恶意的插到我们的页面执行；

- 1）存储型攻击（Stored XSS），即恶意脚本会被存在数据库中
- 2）反射型攻击（Reflected XSS），又名非持久，因为不会被储存到数据库，只是从URL上进行攻击
- 3）基于DOM的攻击（DOM-based XSS），不需要服务器的参与，恶意攻击的发起+执行，全在浏览器完成；
  恶意攻击的发起+执行，全在浏览器完成
- 4）突变型攻击（Mutation-based XSS），利用浏览器渲染DOM的特性，对浏览器针对性的攻击，比如：反引号打破属性边界、CSS中属性值/属性名的转义等

> 反射型和基于DOM的主要区别就是完成注入脚本的地方不同

**跨站请求伪造(CSRF)**，诱导用户打开黑客的网站，窃取用户登录信息，冒充用户身份进行恶意的操作。

- 1）GET类型的CSRF
- 2）POST类型的CSRF

> GET和POST攻击的区别是受害者如何执行攻击

> 跨站脚本攻击（XSS）和跨站请求伪造(CSRF)的区别，本质上讲，XSS 是代码注入问题，CSRF 是 HTTP 问题。

**注入攻击Injection**

- 1）SQL 注入攻击，通过把 SQL 命令插入到 Web 表单提交或页面请求的查询字符串，最终执行恶意的 SQL 命令
- 2）命令注入攻击

**DoS攻击(Denial of Service)**，造成远程服务器拒绝服务的攻击，目的是使计算机或网络无法提供正常的服务

**DDOS攻击(Distributed Denial of Service)**，分布式拒绝服务

**MITM攻击（Man-in-the-MiddleAttack）**，中间人攻击，针对传输层的攻击



# 碎碎念

分析各种web攻击手段是为了能够让我们更好的进行防御，没有让大家去攻击别人的意思啊w(ﾟДﾟ)w！（以上全部示例仅用于举例，切勿模仿👻）





参考资料：

[Cross Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/)

[DOM Based XSS](https://owasp.org/www-community/attacks/DOM_Based_XSS)

[XSS Filter Evasion Cheat Sheet](https://owasp.org/www-community/xss-filter-evasion-cheatsheet)

[Cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting#cite_note-11)

[The Cross-Site Scripting (XSS)](https://www.cgisecurity.com/xss-faq.html) 

[Cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery)

[Cross Site Request Forgery (CSRF)](https://owasp.org/www-community/attacks/csrf)

[谈谈对 Web 安全的理解](https://zhuanlan.zhihu.com/p/25486768?group_id=820705780520079360)

[常见六大Web安全攻防解析](https://juejin.cn/post/6844903772930441230#heading-31)

[MDN—中间人攻击（MitM）](https://developer.mozilla.org/zh-CN/docs/Glossary/MitM)

[百度百科—中间人攻击](https://baike.baidu.com/item/%E4%B8%AD%E9%97%B4%E4%BA%BA%E6%94%BB%E5%87%BB/1739730?fr=aladdin)

>本文作者：Axjy<br/>微信公众号：Axjy前端学习库<br/>版权声明：本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 3.0 CN 许可协议](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/)。转载请注明出处！

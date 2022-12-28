---
title: 
date: 2021-09-06 00:44
tags: web安全
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/41.jpg
summary: web开发安全之怎么防御各种攻击手段
---


在互联网时代，数据安全和个人隐私一直都是大家很关心的问题，要怎么保护我们的应用以及数据呢？上篇以及分析了各种攻击手段，现在我们就来看看怎么防御！🤗

# 前言

看完本篇你将收获

- ✅跨站脚本攻击XSS（Cross-Site Scripting）的大部分防御措施
- ✅跨站请求伪造CSRF（Cross Site Request Forgery ）攻击的大部分防御措施
- ✅注入Injection攻击的的防御措施
- ✅其他一些防御措施及个人用户的安全建议



# XSS的防御



1、永远不要信任用户的提交内容🚫，应该做输入过滤

>例如：邮箱，电话号码，用户名，密码……等输入格式的检查，使用户只能按照规定的格式输入。
>
>移除用户上传的DOM属性，如onerror等，移除用户上传的style节点，script节点，iframe节点等
>
>不仅前端需要做过滤，后端同样也需要，因为攻击者完全可以绕过正常输入，直接利用相关接口发送信息。



2、不要将用户提交内容直接插入到页面，建议做一些HTML转义操作

![image-20210905151054329](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905151054329.png)

3、cookies设置HttpOnly

> 这样可以禁止 JavaScript 读取某些敏感 Cookie，攻击者完成 XSS 注入后也无法窃取此 Cookie。



4、验证码：防止脚本冒充用户提交危险操作❗❗❗



5、少用 `.innerHTML`、`.outerHTML`、`document.write()`等直接插入html的方式，而改用安全性更高的`.textContent`、`.setAttribute()` 等

> 避免把攻击者恶意编写的脚本注入到代码中



6、注意使用DOM 中的内联事件监听器，如 `location`、`onclick`、`onerror`、`onload`、`onmouseover` 等，`<a>` 标签的 `href` 属性，JavaScript 的 `eval()`、`setTimeout()`、`setInterval()` 等

> 因为它们都能把字符串作为代码运行。如果不可信的数据拼接到字符串中传递给这些 API，很容易产生安全隐患



7、开启CSP防护。将CSP设置成`Content-Security-Policy: script-src 'self'`，就可以开启。

> 内容安全策略（CSP）的设计就是为了防御XSS攻击的，开启之后则网站将不允许内联脚本执行，禁止加载外域代码，禁止外域提交。虽然可以有效的防止XSS攻击，但是因为过于严格可能对自身业务开发造成一定的限制👉 [MDN CSP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)





## 利用现成的工具

- 主流框架默认防御XSS
- 或者使用一些第三方库帮助过滤，如[DOMPurify](https://github.com/cure53/DOMPurify) （针对 HTML、MathML 和 SVG 的仅支持DOM、快速、高容错的 XSS 过滤器）



## 可能被XSS攻击的实例

1、使用[DOMParser](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMParser)把srting转化为DOM时，可能携带执行脚本（需要过滤）

![image-20210905192746564](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905192746564.png)



2、用户上传svg图片时，svg中可以内嵌sctipt标签（需要过滤）

![image-20210905193418138](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905193418138.png)

3、允许用户自定义跳转链接，a标签的跳转链接是可以被写成js代码的，所以最好不要允许

![image-20210905194005432](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905194005432.png)

4、让用户自定义样式，举个例子，假如有这样一个选项组

![image-20210905194507424](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905194507424.png)

它的选中是这样写的

![image-20210905194659211](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905194659211.png)

当用户选择指定选项时，background才切换成某一个，而此时background会发送一个get请求，并且会带上一个选中的信息，这个时候就有可能受到XSS攻击

所以首先不要这样写！不要这样写！不要这样写！👻，其次需要注意类似background这种可以发送请求的属性，最后一定要用，一定记得做过滤！！！🥶



# CSRF的防御



1、利用验证码，强制用户必须与应用进行交互，才能完成最终请求

> 如果验证码使用的太频繁，会导致用户体验很不好💥，所以一般只用于特殊操作。
>
> 【CSRF 攻击的过程，往往是在用户不知情的情况下发生的，在用户不知情的情况下构造网络请求】





2、检查 HTTP Referer 字段

>根据 HTTP 协议，在 HTTP 头中有一个字段叫 Referer，它记录了该 HTTP 请求的来源地址，如果我们能判断当前HTTP请求的来源地址，只允许来自本网站的的请求才能访问，那么CSRF攻击就失效了。不过需要知道的是某些浏览器的Referer值可以被篡改。
>
>【CSRF的攻击来源通常是来自第三方网站】



3、使用token，token 验证的 CSRF 防御机制是公认最合适的方案

>后端随机产生一个 token，把这个token 保存到 session 状态中；同时后端把这个token 交给前端，前端页面提交请求时，把 token 加入到请求数据或者头信息中，一起传给后端，端验证前端传来的 token 与 session 是否一致，不一致则拒绝该请求。
>
>【`CSRF`攻击之所以能够成功，是因为攻击者可以伪造用户的请求，该请求中所有的用户验证信息都存在于 `cookie`中，因此攻击者可以在不知道用户验证信息的情况下直接利用用户的 `cookie`来通过安全验证。】



token应该和用户信息绑定，因为攻击者自己也可以通过注册用户去获取token；token应该设置过期时间；

![image-20210905200730871](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/05/image-20210905200730871.png)





4、Cookie 的 SameSite 属性👉[`SameSite`属性](http://www.ruanyifeng.com/blog/2019/09/cookie-samesite.html)



5、其他，get请求不对数据进行修改，服务器端设置 X-Frame-Options 响应头，防止页面被内嵌。



# Injection的防御



1、数据校验，还是那句话，永远不要信任用户的输入🚫

> 对用户的输入进行校验，可以通过正则表达式，或限制长度；对单引号和双"-"进行转换等。



2、不要使用动态拼装 SQL

> 可以使用参数化的 SQL 或者直接使用存储过程进行数据查询存取。



3、严格的权限管理（最小权限原则）

> 严格限制Web应用的数据库的操作权限,只给用户提供仅仅能够满足其工作的最低权限,从而最大限度的 减少注入攻击对数据库的危害



4、不要把机密信息直接存放

> 加密或者 hash 掉密码和敏感的信息。



5、特殊字符转义

> 对进入数据库的特殊字符（',",,<,>,&,*,; 等）进行转义处理,或编码转换



6、查询SQL的地方使用 [prepared statement](https://www.cnblogs.com/geaozhang/p/9891338.html)



# 防御DoS和防御DDoS

不太懂就不细说了😗

SYN 攻击防护（只是DDoS的一种）：

1. 缩短超时（SYN Timeout）时间
2. 增加最大半连接数
3. 过滤网关防护



>哈哈哈🤣，黑客为了逼迫 Github 移除反审查项目Greatfire，对它进行了DDoS攻击
>
>[GitHub 遭遇有史以来最严重DDoS攻击](https://www.leiphone.com/category/gbsecurity/s6FdUv4tcJ9OJwfI.html)



# 防御中间人

浏览器和服务器双方并没有对彼此的身份进行未验证，从而给中间人创造了攻击的条件，所以只需要增加一个安全通道来传输信息。HTTPS 就可以用来防御中间人攻击。



> 如果你没有完全关闭 HTTP 访问的话，攻击方还是可以通过某些方式将 HTTPS 降级为 HTTP 从而实现中间人攻击。





# 个人用户的web安全建议

🎨  不要忽视浏览器弹出的证书警告！你可能访问的是钓鱼网站或者假冒的服务器；

🎨  建议尽量不使用公共的 Wi-Fi，因为很可能就会发生中间人攻击的情况。如果你在通信的过程中涉及到了某些敏感信息，就完全暴露给攻击方了；

🎨  在任何网站上登录自己的账号前确保网址是走的HTTPS加密协议；

🎨  使用网页版邮件的浏览邮件或者新闻也会带来额外的风险，因为查看邮件或者新闻消息有可能导致恶意代码的攻击。

🎨 尽量不要打开可疑的链接，一定要打开时，使用不常用的浏览器。



# 总结

防御简单的总结就是

- 过滤！过滤！过滤！
- 检查！检查！检查！





# 碎碎念

因为好玩去黑网站的人，还是少数的，大多数攻击都是为了有利可图，我们不可能确保自己的应用绝对无法被攻击，但是只要攻击我们的时候，黑客花费的成本远比他可以获取的利益大得多，黑客就不会去攻击。防范强如支付宝、QQ等产品，也都曾被报过漏洞，所以防御不是绝对的，我们只能想办法让我们的应用更加安全。



参考资料：

[DOM based XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)

[XSS Filter Evasion Cheat Sheet](https://owasp.org/www-community/xss-filter-evasion-cheatsheet)

[Cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting#cite_note-11)

[Cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery)

[Cross Site Request Forgery (CSRF)](https://owasp.org/www-community/attacks/csrf)

[谈谈对 Web 安全的理解](https://zhuanlan.zhihu.com/p/25486768?group_id=820705780520079360)

[常见六大Web安全攻防解析](https://juejin.cn/post/6844903772930441230#heading-31)

[百度百科—中间人攻击](https://baike.baidu.com/item/%E4%B8%AD%E9%97%B4%E4%BA%BA%E6%94%BB%E5%87%BB/1739730?fr=aladdin)

[wiki—中间人攻击](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)

>本文作者：Axjy<br/>微信公众号：Axjy前端学习库<br/>版权声明：本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 3.0 CN 许可协议](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/)。转载请注明出处！

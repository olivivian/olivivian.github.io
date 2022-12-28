---
title: 简单说说HTTP
date: 2021-10-02 17:46:00
tags: HTTP
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/7.jpg
summary: HTTP的状态码、请求头、响应头、Cookies及请求方法合集
---

<br/>

# HTTP和HTTPS的区别图解

HTTPS和HTTP相比多了一层加密



![image-20211002153855635](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002153855635.png)


<br/>

# HTTP的常用状态码

**200**	 👉	OK，客户端请求成功

**301**👉	资源(网页等)被永久转移到其它URL

**302**👉	临时跳转

**401**	 👉	Unauthorized -请求未经授权

**404** 	👉	请求资源不存在，可能是输入了错误的URL

**500** 👉	服务器内部发生了不可预期的错误

**504** 👉	 Gateway Timeout-网关或者代理的服务器无法在规定的时间内获得想要的响应。

![image-20210920192949824](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/20/image-20210920192949824.png)


<br/>

# HTTP常用请求头（Request Headers）

**Accept**：
 接收类型，表示浏览器支持的MIME类型（对标服务端返回的Content-Type）

![image-20211002161729473](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002161729473.png)



**Content-Type**：
客户端发送出去实体内容的类型

![image-20211002161801679](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002161801679.png)

**Cache-Control**：
指定请求和响应遵循的缓存机制，如no-cache

![image-20211002163255317](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002163255317.png)

**If-Modified-Since**：
 对应服务端的`Last-Modified`,用来匹配看文件是否变动，只能精确到1s之内



**Expires**：
缓存控制，在这个时间内不会请求，直接使用缓存，服务端时间



**Max-age**：
 代表资源在本地缓存多少秒，有效时间内不会请求，而是使用缓存



**If-None-Match**：
 对应服务端的ETag,用来匹配文件内容是否改变（非常精确）



**Cookie**：
 有cookie并且**同域**访问时会自动带上

![image-20211002155443610](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002155443610.png)

**Referer**：
该页面的来源URL（适用于所有类型的请求，会精确到详细页面地址，csrf拦截常用到这个字段）

![image-20211002161835593](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002161835593.png)

**Origin**：
最初的请求是从哪里发起的（只会精确到端口)）,Origin比Referer更尊重隐私

![image-20211002161858626](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002161858626.png)

**User-Agent**：
 用户客户端的一些必要信息，如UA头部等

![image-20211002155948600](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002155948600.png)

# HTTP常用响应头（Response Headers）

**Content-Type**： 
 服务端返回的实体内容的类型



**Cache-Control**：
指定请求和响应遵循的缓存机制，如no-cache

![image-20211002163336562](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002163336562.png)

**Last-Modified**：

 请求资源的最后修改时间



**Expires**：
应该在什么时候认为文档已经过期，从而不再缓存它

![image-20211002163349623](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002163349623.png)

**Max-age**：
 客户端的本地资源应该缓存多少秒，开启了	Cache-Control	后有效



**ETag**：
资源的特定版本的标识符，`Etags`类似于指纹



**Set-Cookie**：
 设置和页面关联的cookie,服务器通过这个头部把cookie传给客户端



**Server**：
服务器的一些相关信息

![image-20211002160637134](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/10/02/image-20211002160637134.png)

**Access-Control-Allow-Origin**：
 服务器端允许的请求Origin头部(譬如为*)




<br/>

# HTTP的各类请求方法

**GET**：		 

请求一个指定资源的表示形式.使用GET的请求应该只被用于获取数据



**POST**：	 		

用于将实体提交到指定的资源，通常导致在服务器上的状态变化或副作用



**PUT**：	 		  

 用请求有效载荷替换目标资源的所有当前表示



**DELETE**：	 	

删除指定的资源



**HEAD**：	    	

请求一个与GET请求的响应相同的响应，但没有响应体



**CONNECT**：	 

建立一个到由目标资源标识的服务器的隧道。



**OPTIONS**：	 

 用于描述目标资源的通信选项。



**TRACE**： 		

沿着到目标资源的路径执行一个消息环回测试。



**PATCH**： 		

用于对资源应用部分修改。


<br/>

# HTTP的缓存

![image-20210920225414298](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/09/20/image-20210920225414298.png)

## 强缓存

**Expires** ：时间不准

**Cache- Control的值有**

- **max-age** :单位是秒，缓存时间计算的方式是距离发起的时间的秒数，超过间隔的秒数缓存失效
- **no-cache** :不使用强缓存，需要与服务器验证缓存是否新鲜
- **no-store** :禁止使用缓存(包括协商缓存)每次都向服务器请求最新的资源
- **must-revalidate** :在缓存过期前可以使用，过期后必须向服务器验证



## 协商缓存

**ETag/lf-None-Match**,：hash 码，代表的是一个资源的标识符

**Last- Modified/lf- Modified-Since**：文件的最后修改时间


<br/>

# 视频直播协议



| 协议       | 描述                                                         | 优点   |
| ---------- | ------------------------------------------------------------ | ------ |
| HLS        | 1、HTTP Live Streaming, Apple公司<br/>2、基于HTTP协议<br/>3、把一段视频流，分成一个个小的基于HTTP的文件来下载 | 跨平台 |
| RTMP       | 1、Real Time Messaging Protocol<br/>2、Adobe公司<br/>3、基于TCP | 时延低 |
| HTTP - FLV | 1、基于HTTP<br/>2、http+flv，将音视频数据封装成FLV格式，然后通过HTTP协议传输给客户端 | 时延低 |


<br/>

# Cookie

Set-Cookie - response

| Name=value                       | 各种cookie的名称和值                                         |
| -------------------------------- | ------------------------------------------------------------ |
| Expires=Date                     | Cookie的有效期，缺省时Cookie仅在浏览器关闭之前有效。         |
| Path= Path                       | 限制指定Cookie的发送范围的文件目录，默认为当前               |
| Domain=domain                    | 限制cookie生效的域名，默认为创建cookie的服务域名             |
| secure                           | 仅在HTTPS安全连接时，才可以发送Cookie                        |
| HttpOnly                         | JavaScript脚本无法获得Cookie                                 |
| `SameSite=[None\Strict\Lax]` | - None同站、跨站请求都可发送<br/>- Strict仅在同站发送<br/>- 允许与顶级导航一起发送，并将与第三方网站发起的GET请求一起发送 |











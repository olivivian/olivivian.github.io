---
title: git问题解决方案汇总
date: 
tags: Git
categories: 工具
img: 
summary: 
---

# 更换网络，git代码提交报错

```
错误提示：
Unable to access...Could not resolve host
```

## 找到本机IP

```
ipconfig
```



![image-20221029185036636](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221029185036636.png)

## 找到git目录下的 hosts文件

一般目录为 C:\Program Files\Git\etc

```
在该文件下 添加 192.168.1.117 github.com
```

![image-20221029185428182](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221029185428182.png)

---
title: Jenkins前端部署配置
date: 2021-03-07
tags: Jenkins
categories: 工具
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/16.jpg
summary: 利用Jenkins自动化部署Web项目
top: true
---


# 前期准备

在【系统管理（Manage Jenkins）】--【插件管理（Manage Plugins）】安装一些必要的插件

![image-20210223100202305](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223100202305.png)

![image-20210223100216347](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223100216347.png)

## 安装NodeJS

![image-20210223100356939](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223100356939.png)

点击【系统管理（Manage Jenkins）】--【全局工具配置（Global Tool Configuration）】

![image-20210223102720906](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223102720906.png)



找到【NodeJS】，点击新增【NodeJS】

![image-20210223102800526](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223102800526.png)



填写一下别名，点击保存

![image-20210223102902708](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223102902708.png)

## 安装插件【 publish over ssh 】，用于自动构建发包到服务器上

【系统管理（Manage Jenkins）】--【插件管理（Manage Plugins）】，搜索插件【publish over ssh 】，点击安装即可

![image-20210223160413401](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223160413401.png)

安装完成后，到【系统管理（Manage Jenkins）】——【系统设置（Configure System）】，找到Publish over SSH，点击新增。

![image-20210223161220327](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223161220327.png)

配置服务器相关信息

![image-20210223161445781](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223161445781.png)

点击【高级】进行其他配置

![image-20210223161615316](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223161615316.png)

测试配置

![image-20210223161750619](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223161750619.png)

 #  一、新建项目

选择【构建一个自由风格的软件项目】；

名称必须填英文（否则部署的过程可能会出现问题）

![image-20210223090635858](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223090635858.png)

# 二、项目配置

新建完之后会直接跳到项目配置

![image-20210223092913719](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223092913719.png)

## General

勾选【参数化构建过程（This project is parameterized）】;

点击 》 添加参数--选项参数（Choice Parameter）;

![image-20210223093244926](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223093244926.png)

填写 》选项参数（Choice Parameter）；

并且继续选择   》添加参数——字符参数（String Parameter）

```
status

deploy
roll_back

|deploy : 发布 |
----------------
|roll_back : 回滚 |
```



![image-20210223093507899](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223093507899.png)

填写 》字符参数（String Parameter）

```
version
0
                ↑*回滚选项*↑
     --------------------------------
**      回滚请填写回滚版本号     **
     --------------------------------
```

![image-20210223094201482](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223094201482.png)

## 源码管理

1、选择Git；2、填写仓库地址；3、添加git的用户名，密码； 4、填写用来发布的分支；

![image-20210223095452937](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223095452937.png)

![image-20210223095555808](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223095555808.png)



![image-20210223095648343](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223095648343.png)

点击添加之后，凭证就会在这个下拉列表看到

![image-20210223095834778](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223095834778.png)

选择凭证，最终完成git的配置

![image-20210223095918628](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223095918628.png)

##  构建触发器

选择》Provide Node & npm bin/ folder to PATH  选项，如果之前的NodeJS没有安装成功，则看不到这个选择

![image-20210223102923510](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223102923510.png)



## 构建

点击【增加构建步骤】；

选择  》执行Shell （Execute Shell）

![image-20210223103324446](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223103324446.png)



填写命令

```
case ${status} in
  deploy)
    node -v
    npm -v
    npm install -g cnpm --registry=https://registry.npm.taobao.org
	cnpm -v
	cnpm install
	cnpm run build
    echo "Status:$Status"
     path="D:/frontEnd/payCenterBackup/${BUILD_NUMBER}"  
    mkdir -p  $path
    \cp -r ${WORKSPACE}\\\dist $path
    echo "Completing!"
    ;;
    
  roll_back)
    echo "status:$status"
    echo "version:$version"
	cd ${WORKSPACE}
    rm -rf dist
    cd D:/frontEnd/payCenterBackup/$version
    \cp -r dist ${WORKSPACE}/
      ;;
esac
```



![image-20210223155138626](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223155138626.png)



## 构建后操作

关联发布的服务器，选择【Send build artifacts over SSH】，要先安装插件【 publish over ssh 】，否则可能不会有这个选项，上面的前期准备有写安装方法。

![image-20210223155933822](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223155933822.png)

SSH Publishers配置信息

![image-20210223163659865](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223163659865.png)



# 三、最终效果

![image-20210223170433354](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com//Typora/typora-user-images/2021/02/23/image-20210223170433354.png)


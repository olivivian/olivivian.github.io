

使用小插件[deploy-cli-service](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fdeploy-cli-service)轻松实现前端自动化部署。



# 安装

```
npm install deploy-cli-service --save-dev
```

# 配置文件

在项目根目录下手动创建 `deploy.config.js` 文件，可复制以下代码按情况

```
module.exports = {
  projectName: 'vue_samples', // 项目名称
  privateKey: '',//本地私钥地址    如：/Users/fuchengwei/.ssh/id_rsa
  passphrase: '',//本地私钥密码
  cluster: [], // 集群部署配置，要同时部署多台配置此属性如: ['dev', 'test', 'prod']
  dev: {
    // 环境对象
    name: '开发环境', // 环境名称
    script: 'npm run build', // 打包命令
    host: '192.168.0.1', // 服务器地址
    port: 22, // 服务器端口号
    username: 'root', // 服务器登录用户名
    password: '123456', // 服务器登录密码
    distPath: 'dist', // 本地打包生成目录
    webDir: '/usr/local/nginx/html', // 服务器部署路径（不可为空或'/'）
    bakDir: '/usr/local/nginx/backup', // 备份路径 (打包前备份之前部署目录 最终备份路径为 /usr/local/nginx/backup/html.zip)
    isRemoveRemoteFile: true, // 是否删除远程文件（默认true）
    isRemoveLocalFile: true // 是否删除本地文件（默认true）
  },
  test: {
    // 环境对象
    name: '测试环境', // 环境名称
    script: 'npm run build:test', // 打包命令
    host: '192.168.0.1', // 服务器地址
    port: 22, // 服务器端口号
    username: 'root', // 服务器登录用户名
    password: '123456', // 服务器登录密码
    distPath: 'dist', // 本地打包生成目录
    webDir: '/usr/local/nginx/html', // 服务器部署路径（不可为空或'/'）
    bakDir: '/usr/local/nginx/backup', // 备份路径 (打包前备份之前部署目录 最终备份路径为 /usr/local/nginx/backup/html.zip)
    isRemoveRemoteFile: true, // 是否删除远程文件（默认true）
    isRemoveLocalFile: true // 是否删除本地文件（默认true）
  },
  prod: {
    // 环境对象
    name: '生产环境', // 环境名称
    script: 'npm run build:prod', // 打包命令
    host: '192.168.0.1', // 服务器地址
    port: 22, // 服务器端口号
    username: 'root', // 服务器登录用户名
    password: '123456', // 服务器登录密码
    distPath: 'dist', // 本地打包生成目录
    webDir: '/usr/local/nginx/html', // 服务器部署路径（不可为空或'/'）
    bakDir: '/usr/local/nginx/backup', // 备份路径 (打包前备份之前部署目录 最终备份路径为 /usr/local/nginx/backup/html.zip)
    isRemoveRemoteFile: true, // 是否删除远程文件（默认true）
    isRemoveLocalFile: true // 是否删除本地文件（默认true）
  }
}
```

# 配置注意

1）**如果不想把服务器密码保存在配置文件中，可以在配置文件中删除 `password` 字段**。在部署的时候会弹出输入密码界面。

2）如果把服务器密码保存在配置文件，并且是公开项目，可以不上传这个配置文件

```
.gitignore文件配置，忽略配置文件上传

deploy.config.js
```

3）如果不想在部署前执行打包命令，在配置文件中删除 `script` 字段即可。

4）如果需要部署前备份，在配置文件中配置 `bakDir` 字段，为空不会备份。ps: 服务器需要安装 zip 模块，可使用 yum install zip 命令。

# 配置部署命令

在`package.json`中配置启动部署的命令

```
 "scripts": {
    "deploy:test": "deploy-cli-service deploy --mode test",
    "deploy:prod": "deploy-cli-service deploy --mode prod"
}
```



# 开始部署

```
运行部署命令

npm run deploy:test
```

![image-20221230114757475](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20221230114757475.png)




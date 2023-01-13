---
title: electron-vue项目搭建
date: 2023-01-12 13:57:29
tags:
categories:
---

[TOC]

# 环境说明

* node版本：v14.13.1
* npm版本：6.14.8
* vue-cli版本：5.0.3
* vue：2.x



# vue项目创建

使用vue-cli来创建一个vue 2项目：

```sh
vue create hello-world
```

提示时，选择vue2。

创建成功后，进入到项目文件夹，执行启动命令进行测试。



# electron-builder插件集成

> 参考：https://www.jianshu.com/p/dfcf2a6a497c
>
> https://www.jianshu.com/p/1dbb96bc8f37

停止项目运行。

进入到项目文件夹，执行以下命令来启动vue项目管理器：

```sh
vue ui
```

左下角点击三个点，选择vue project manager，然后导入本项目。

然后进入插件页面，点击添加插件按钮，搜索”vue-cli-plugin-electron-builder“，选择之后，点击安装。

安装完成后，点击“安装完成”，（必须要点击安装完成，否则项目架构会出问题）



# linux系统搭建node环境

> Linux arm也通用
>
> 参考：https://www.cnblogs.com/zt88cn/p/12023706.html

1. 下载node.js，网址：nodejs.cn
2. 解压到某目录，例如解压后node目录为：/home/orangepi/node-v12.13.1-linux-armv7l
3. 执行以下命令 ```sudo ln /home/orangepi/node-v12.13.1-linux-armv7l/bin/node /usr/local/bin/node```

4. 执行以下命令```sudo ln -s /home/orangepi/node-v12.13.1-linux-armv7l/lib/node_modules/npm/bin/npm-cli.js  /usr/local/bin/npm```

5. 执行node -v和npm -v查看版本



# 设置electron镜像

npm config set electron_mirror https://repo.huaweicloud.com/electron/ 

npm install -g electron



# 注意事项

## arm 打包报错：snapcraft

增加打包配置：

```javascript
linux: {
	tartget: [
		"AppImage"
	]
}
```

## linux下使用ffi-napi时，npm install报错问题

> https://segmentfault.com/q/1010000042601075?utm_source=sf-similar-question
>
> https://blog.csdn.net/weixin_33304777/article/details/116893532

报错：gyp ERR! stack Error: not found: make

```sh
yum i gcc-c++
sudo apt-get install build-essential
```

执行第一行命令后没有成功，执行完第二个后可以。可能只执行第二个就行

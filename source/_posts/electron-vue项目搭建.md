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

停止项目运行。

进入到项目文件夹，执行以下命令来启动vue项目管理器：

```sh
vue ui
```

左下角点击三个点，选择vue project manager，然后导入本项目。

然后进入插件页面，点击添加插件按钮，搜索”vue-cli-plugin-electron-builder“，选择之后，点击安装。

安装完成后，点击“安装完成”，（必须要点击安装完成，否则项目架构会出问题）






















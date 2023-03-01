---
title: 安卓adb常用指令
date: 2023-03-01 09:56:00
tags:
categories:
---

## 查看所有已安装的应用列表：

```shell
adb shell pm list packages
```

找到包名：com.xxx.yyy.zzz



## 卸载软件：

```shell
adb uninstall com.xxx.yyy.zzz
```



## 安装软件：

```shell
adb install xxx.apk
```



## 覆盖安装：

```shell
adb install -r xxx.apk
```



## 打开软件：

```shell
adb shell am start com.xxx.yyy.zzz/.MainActivity
```


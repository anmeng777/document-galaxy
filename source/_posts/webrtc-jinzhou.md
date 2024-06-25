---
title: 晋州音视频对讲梳理
date: 2024-05-30 13:31:44
tags:
categories:
---

## 主进程

```mermaid
flowchart LR
A[初始化] --> B[监听求助键]
B --> C[收到求助键信号]
C --> D[发送HTTP请求 /monitor/videoRqt]

A --> E[建立wss通信]
E --> F[每分钟发送心跳]
E --> G[监听音视频对话控制消息]
G --> H[收到'开始音视频对话'消息]
G --> I[收到'结束音视频对话'消息]
G --> J[收到'切换音视频对话'消息]
G --> K[收到'音视频对话心跳'消息]
G --> L[收到'强制结束对话'消息]
G --> M[收到'取消视频对话请求'消息]
H --> O[加载对讲流程\n包括建立信令服务器连接\n加入房间等]
O --> P[接通]
I --> R[挂断对讲]
J --> S[切换摄像头]
K --> Q[如果当前处于对讲中\n且连续15秒\n没有收到心跳]
Q --> R
L --> R
M --> R
```



## 技术实现

原有程序基础上：

* 增加晋州专属通话页面

* 配置页面
  * 增加晋州协议选项
  * 如果选择了晋州协议
    * 隐藏：ws连接
    * 增加：
      * 晋州求助http url
      * 晋州websocket url
      * 增加车道号等
    * 跳转对讲的时候不进入原有通话页面，而是晋州新页面
    * 程序启动时需要判断，如果是晋州协议，自动跳转到晋州通话页面，否则还是原有通话页面

* 在background中监听UDP数据包，如果收到了就发送http请求（已实现）

* 在background中建立晋州ws连接，如果收到通话消息了就调用前端方法



---
title: ed大桥开发记录
date: 2024-07-08 09:30:23
tags:
categories:
---

ed大桥开发记录



先是提供了一个“桥梁监测信息数据接口标准”文档，里面有关于这个桥梁的用户名、密码（用于调用登录接口，但是登录接口是做什么用的不知道）。提供的用户名密码是：eddq   Ed@dq852



后来提供了一个新版文档“桥梁监测信息数据接口标准 - new”，但是里面也有一些疑问没有解答。后来给了个最新的接口文档。



在线接口文档：链接: https://apifox.com/apidoc/shared-de01c59e-310a-462b-b625-72daaf67085d?pwd=cqjky_123456 访问密码: cqjky_123456

bridgeNumber=73代表这个大桥，token写死：eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1aWQiOiLphILkuJzlpKfmoaUiLCJleHBpcmVfdGltZSI6LTEsImJyaWRnZUlkcyI6Ils3M10ifQ.qtvHiYWHeF-mwVxw0fjR-Hs3tBoMIUxIQZWos2acwzY



文档提供的设备和表格中没有对应上的以实际返回设备为准

![image-20240708093809429](https://pic.tele.anmeng.tech/file/fbdb8ca1807cd1daeca60.png)





测点列表就是设备列表

![image-20240708094041051](https://pic.tele.anmeng.tech/file/a17d1611f08b296c73620.png)



测点数据返回的是单个设备的多条历史数据

![image-20240708094016649](https://pic.tele.anmeng.tech/file/007f9271989a9ff9ad4ef.png)

![image-20240708093941383](https://pic.tele.anmeng.tech/file/4f3670ab6bcaf6153d17c.png)



测点列表中返回的“meaptNumber”字段是唯一的，可以作为设备编号来使用

![image-20240708094153169](https://pic.tele.anmeng.tech/file/c414b180a0a30a5e425ac.png)





模块名是：protocol-bridge-sys



设备同步参考代码

```java
String pointNo = pointItem.getStr("pointNo");
String pointName = pointItem.getStr("pointName");
String paramCode = pointItem.getStr("dictMonitorParamCode");
if (StringUtils.isEmpty(paramCode) || StringUtils.isEmpty(pointName)
        || StringUtils.isEmpty(pointNo)) {
    // 不需要监测的点位
    continue;
}

SyncDeviceDto syncDeviceDto = new SyncDeviceDto();
syncDeviceDto.setDeviceName(structName + "-" + formatName(pointName));
// 通过参数类型获取产品id
String productId = productMap.get(paramCode);
if (StringUtils.isEmpty(productId)) {
    log.error("桥梁监测参数:{} 缺少对应产品", paramCode);
    continue;
}

syncDeviceDto.setProductId(productId);
syncDeviceDto.setExternalDeviceId(pointNo);
syncDeviceDto.setManufacturer(Manufacturer.zhaoshanglujian.getCode());
syncDeviceDto.setModelNumber(ModelNumber.def.getValue());
// 公司
syncDeviceDto.setCompany(bridgeConfig.getBelongCompany());
syncDeviceDto.setLocation(address + "-" + pointName);

// 减少对平台压力
Thread.sleep(10);
assert dagService != null;
dagService.syncDevice(syncDeviceDto);
```



从本地数据库中读取设备的api：findSubDevicesByExtId



产品pid：

```tex
复用的
应变计	
105120	
挠度计	
105119
裂缝计
105118
温湿度计
105147

新的通用
桥梁倾角仪	
112597
索力传感器	
112596
风速风向传感器	
112595
GNSS传感器	
112594
加速度传感器	
112590
伸缩缝位移	
112598
```



SyncDeviceDto的Company配成107



设备名称命名规则：请输入不超过128位的中文/字母/数字/下划线/中划线且开头结尾不可有空格的内容




















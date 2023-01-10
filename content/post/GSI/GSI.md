---
title: "Android GSI 介绍"
date: 2022-11-14T20:41:03+08:00
draft: false
slug: "GSI"
tags: ["Android"]
categories: ["Technology"]
---

# GSI
## 什么是 GSI
GSI，中文名"通用系统镜像",可以在支持 Treble 的设备上刷入 GSI 以便体验最新的 Android 操作系统  
Google 的 GSI 是 AOSP 未经修改的，可在各种 Android 设备上运行
## GSI 要求
刷入 GSI 的设备需符合以下要求：
- Bootloader 已解锁
- 完全符合 Treble 要求
- 出场时搭载 Android9 或更高版本

搭载 Android8 或 Android8.1 的设备可能支持 Treble，但在 Android12 及更高版本的 GSI 中，移除了对 Android8 或 8.1 的不完全 Treble 的兼容性  
设备需支持 VNDK 才能跨版本刷入 Android 版本的 GSI  
### 检查 GSI 要求
运行以下命令以检查设备是否支持 Treble  

~~TMD Chroma 不支持 Shell 高亮~~

```
adb shell getprop ro.treble.enabled
```

返回为 True 则支持，False 则表示不兼容 GSI  

运行以下命令检查设备是否支持 VNDK

```
adb shell cat /system/etc/ld.config.version_identifier.txt \
| grep -A 20 "\[vendor\]"
```

在输出的 vendor 部分中查找 namespace.default.isolated  
若返回 True，则代表设备可以安装跨版本的 GSI，若返回 false 则不可  

GSI 的架构类型必须与设备一致，运行此命令检查架构类型  

```
adb shell getprop ro.product.cpu.abi
```

也可使用 [Treble Checker](https://play.google.com/store/apps/details?id=com.blackcurrantstudioz.TrebleCheck)或[Treble 信息](https://play.google.com/store/apps/details?id=tk.hack5.treblecheck) 查看上述信息

## GSI 选择
若您的设备支持A/B,或A-only但支持system-as-root,请选择文件名中带有"ab"字样的镜像  
若您的设备支持动态分区，则可以使用 DSU  
若您的设备不支持 system-as-root，也非 A/B 设备，请选择文件名中带有 A-only 字样的镜像  

## 刷写 GSI
将 GSI 刷入至符合要求的任何 Android 设备  
重启到 Fastboot，动态分区设备重启到 Fastbootd  

擦除 System  
```
fastboot erase system
```
刷入 GSI  
```
fastboot flash system system.img
```
擦除用户数据和其他一些分区数据  
```
fastboot -W
```

若出现以下错误
```
Resizing 'system_a'    FAILED (remote: 'Not enough space to resize partition')
fastboot: error: Command failed
```
则说明系统分区空间不足，可能需要删除产品分区或扩容 system  

更改导航栏模式输入
```
adb exec-out cmd overlay enable-exclusive com.android.internal.systemui.navbar.mode
```
可选`threebutton`,`twobotton`,`gestural`

<meting-js server="netease" type="song" id="399366427">
---
title: "Android GSI 介绍"
date: 2022-11-14T20:41:03+08:00
draft: false
slug: "GSI"
image: "https://tva4.sinaimg.cn/large/0072Vf1pgy1foxkjjz8vbj31hc0u0k80.jpg"
tags: ["Android"]
categories: ["Technology"]
---

# GSI
## 什么是GSI
GSI,中文名"通用系统镜像",可以在支持Treble的设备上刷入GSI以便体验最新的Android操作系统  
Google的GSI是AOSP未经修改的,可在各种Android设备上运行
## GSI要求
刷入GSI的设备需符合以下要求:
- Bootloader已解锁
- 完全符合Treble要求
- 出场时搭载Android9或更高版本

搭载Android8或Android8.1的设备可能支持Treble,但在Android12及更高版本的GSI中,移除了对Android8或8.1的不完全Treble的兼容性  
设备需支持VNDK才能跨版本刷入Android版本的GSI  
### 检查GSI要求
运行以下命令以检查设备是否支持Treble  

{{< highlight go >}}
adb shell getprop ro.treble.enabled
{{< / highlight >}}

返回为True则支持,False则表示不兼容GSI  

运行以下命令检查设备是否支持VNDK

{{< highlight go >}}
adb shell cat /system/etc/ld.config.version_identifier.txt \
| grep -A 20 "\[vendor\]"
{{< / highlight >}}

在输出的vendor部分中查找namespace.default.isolated  
若返回True,则代表设备可以安装跨版本的GSI,若返回false则不可  

GSI的架构类型必须与设备一致,运行此命令检查架构类型  

{{< highlight shell >}}
adb shell getprop ro.product.cpu.abi
{{< / highlight >}}

也可使用 [Treble Checker](https://play.google.com/store/apps/details?id=com.blackcurrantstudioz.TrebleCheck)或[Treble 信息](https://play.google.com/store/apps/details?id=tk.hack5.treblecheck) 查看上述信息

## GSI选择
若您的设备支持A/B,或A-only但支持system-as-root,请选择文件名中带有"ab"字样的镜像  
若您的设备支持动态分区,则可以使用DSU  
若您的设备不支持system-as-root,也非A/B设备,请选择文件名中带有A-only字样的镜像  

## 刷写GSI
将GSI刷入至符合要求的任何Android设备  
重启到Fastboot,动态分区设备重启到Fastbootd  

擦除System  
```
fastboot erase system
```
刷入GSI  
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
则说明系统分区空间不足,可能需要删除产品分区或扩容system  

更改导航栏模式输入
```
adb exec-out cmd overlay enable-exclusive com.android.internal.systemui.navbar.mode
```
可选`threebutton`,`twobotton`,`gestural`

<meting-js server="netease" type="song" id="399366427">
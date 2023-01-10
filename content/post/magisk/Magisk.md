---
title: "如何使用第三方 Recovery 禁用 Magisk 模块"
date: 2022-11-15T20:55:56+08:00
draft: false
slug: "Magisk"
tags: ["Android","Magisk","short"]
categories: ["Technology"]
---
# 快速禁用 Magisk 模块
## Magisk 模块标识
Magisk 模块位于`/data/adb/modules`  
在此目录下的所有文件夹均对应模块   
模块目录中共有三种标识，均为文件，我们也从这下手  
标识：
- skip_mount(若存在，Magisk 不会挂载模块自定义的 system)
- disable(若存在，模块在下次启动时会被禁用)
- remove(若存在，模块在下次启动时会被移除)

## 在第三方 Recovey 中管理模块
在`/data/adb/modules`中的模块文件夹打开终端，当然，也可以使用`Adb shell`  
输入  
```
touch disable
```
即可禁用此模块 (使用`touch`创建`disable`)  
同理，输入
```
touch remove
```
即可移除模块  

<font color="red">不要直接删除模块文件夹，可能会导致无法修复的问题</font>

## 通过 ADB 移除所有模块
启动 ADB 工具，并输入
```
adb wait-for-device shell magisk --remove-modules
```
再连接设备，并开机 (System)  
若还是无法启动，强制重启一次即可  

<meting-js server="netease" type="song" id="1992552055">

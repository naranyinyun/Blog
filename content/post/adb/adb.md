---
title: "配置 ADB 环境"
date: 2022-12-25T19:37:38+08:00
draft: false
slug: "Adb"
image: "https://tva4.sinaimg.cn/large/0072Vf1pgy1foxkf6k4jrj31hc0u0k6b.jpg"
tags: ["Android","Developer"]
categories: ["Technology"]
---
# 配置 ADB 环境以及基础用法
## 配置 ADB 环境
### 方案一
在[Android Developers](https://developer.android.google.cn/studio/releases/platform-tools?hl=zh-cn)下载适用于您的设备平台的 SDK Platform-Tools  
如果您所在地有网络问题无法下载 SDK Platform-Tools , 我们提供镜像, 这是[下载链接](https://mirror.nalanyinyun.ml/AliDrive/platform-tools_r33.0.3-windows.zip)(33.0.3,Windows Only)  
下载文件后解压至您认为适合的路径，然后在`Windows 搜索`中输入`环境变量`,并打开`编辑系统环境变量`,或者从控制面板打开`系统属性`，这取决于您  
点击位于右下方的`环境变量`,在下方的系统变量中有`Path`,双击`Path`  
点击`编辑环境变量`面板右侧的`新建`,然后点击`浏览`, 并选择您刚才解压的`SDK Platform-Tools`所在路径  
### 方案二
要使用`Chocolatey`安装`Android Debug Bridge`，在 PowerShell(管理员) 或其他终端中输入： 
```
choco install adb
```

您可能对`Chocolatey`是什么感到疑惑，`Chocolatey`是 Windows 平台上的一种命令行式的包管理工具  
如果您打算安装`Chocolatey`,在`PowerShell`中输入：
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### 方案三
您可以下载`秋之盒`,`搞机助手`等工具箱使用它们集成的`Android Debug Bridge`  
他们均提供简明易懂的 GUI，我们不再赘述用法  

这样，`Android Debug Bridge`就成功在您的设备上安装了  
享受`Android Debug Bridge`带来的便利吧  

<meting-js server="netease" type="song" id="1460606295">
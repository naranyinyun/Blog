---  
title: "为小米平板 2 刷入 Windows 11 或 10"  
date: 2023-10-28T19:54:45+08:00  
draft: false  
slug: "XiaomiPad2"  
tags: ["Technology"]  
---  
# Intro  
本文将介绍如何将 Windows 10 & 11 刷入 Xiaomi Pad 2  
此外 [Nalanyinyun's OneDrive](https://mirror.nalanyinyun.top/) 将提供本文所需所有文件的镜像  
> The Nalanyinyun's OneDrive is a mirror for lots of sources, it's free, fast, no trick.  
> Nalanyinyun's OneDrive 是为源提供的镜像，免费，高速而毫无套路  
> 我们不需要你关注任何公众号，也无需付费或感受糟糕的下载体验。  

# 准备工作  
所需物品  
- 一个不小于 8GB 的 **FAT32** 格式的外置存储设备  
- 键盘和鼠标，必须可以通过 USB 方式连接到电脑  
- 一个 OTG 转接器或 USB 集线器，推荐至少有两个接口并可外置供电  
- 将你的平板充满电，因为接下来的操作过程可能会非常长，低电量水平会导致失败
- 你要安装的系统镜像，提前存至存储设备中 *我非常推荐你使用 Windows LTSC 2021 或 2019 你可以在 MSDN 上找到它们

# 前置步骤  
## 1.0 在外置存储设备上安装 PE  
### 1.0.1 格式化存储设备  
首先，确认你的存储设备可以通过 USB 连接到电脑，并且格式为 FAT32 , 且只有一个分区 (推荐) 如果已经确认，请转至 1.0.2  
打开 DiskGenius  
![](/DiskGenius.png)  
选中你的移动存储设备，依次点击右上方 `磁盘` - `删除所有分区`  
保存更改  
点击 `新建分区` , 然后在 `请选择文件系统类型:` 中选择 `FAT32` 并确认  
### 1.0.2 安装 PE  
下载 [Xiaomi Pad 2 Touchable PE](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/Xiaomi%20Pad%20Source/Xiaomi%20Pad%202%20Touchable%20PE.7z)  
将压缩包内所有文件解压至存储设备**根目录**  
### 1.0.3 准备驱动  
下载 [Xiaomi Pad 2 Drives](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/Xiaomi%20Pad%20Source/Xiaomi%20Pad%202%20Drivers.7z)  
建议将驱动提前解压至你熟悉的目录，否则你可能会花费超过 4 分钟的时间解压此文件  
### 1.0.4 确认  
确认你的文件结构正常，如果你没有把驱动解压至根目录，他的结构看起来应该是这样  
``` Markdown  
Length Name  
------ ----  
LOST.DIR  
Boot  
efi  
sources  
附件  
bootmgfw.efi  
bootmgr.efi  
```  
# 在平板上操作  
## 1.0 进入 PE  
将存储设备连接至平板并重启，如果提示 `Shim UEFI key mangement` 此类提示，按下电源键进入 BIOS  
接入键盘，依次操作 `Boot Manager` - `System Setup` 关闭 `Secure Boot`  
按下 ESC, 拔下键盘插入存储设备，用音量键选择 `Commit Change and reboot` 按电源键确认。  
重启后即可进入 PE, 你可能每次进入 PE 都需要执行此操作  
## 1.1 操作分区  
在 DiskGenius 中按照 1.0.1 的步骤删除 本地硬盘 中的所有分区，注意 新建分区时应选择 NTFS 格式，勾选创建 ESP 分区  
## 1.2 安装系统  
打开 Dism++ , 依次点击 右上方 `文件` - `释放镜像` 选择你的镜像和释放目录，勾选`格式化`,`添加引导`  
点击确认，等待释放完成  
完成后点击 `打开会话` - `驱动管理` - `添加驱动` 选择你在 1.0.3 中解压的文件，注意，是**整个文件夹**, 即 `Xiaomi Pad 2 Drivers` 文件夹  
等待添加完成，点击重启并在屏幕熄灭后迅速拔下存储设备  
## 1.3 OOBE  
完成 Windows 引导即可享受  

---
title: "如何在Windows环境下使用BBdown"
slug: "bbdown"
date: 2022-11-10T21:06:57+08:00
draft: false
---
# 配置BBdown
## 本体
从[BBdown](https://github.com/nilaoda/BBDown)的Github下载BBdown程序并添加环境变量(不加也行)
## 依赖
使用BBdown需要FFmpeg或mp4box  
从[FFmpeg](https://ffmpeg.org/)下载FFmpeg并配置环境变量(必须配置)
# 使用BBdown
打开Powershell/CMD  
我这里没有添加环境变量,所以在BBdown所在目录打开Powershell/CMD  
运行BBdown  
```
./bbdown
```
登录BiliBili  
```
./bbdown login
```
用法  
```
./BBDown <url> [command] [options]
```
常用指令
```
--audio-only 只下载音频
--video-only 只下载视频
-ia 交互式选择清晰度(最常用)
```

# 用于测试Action的实例内容 无需在意
test 
PR测试

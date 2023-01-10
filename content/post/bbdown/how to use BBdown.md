---
title: "如何在 Windows 环境下使用 BBdown"
slug: "bbdown"
date: 2022-11-10T21:06:57+08:00
draft: false
tags: ["BiliBili","CLI","Windows"]
categories: ["Technology"]
---
# 配置 BBdown
## 本体
从[BBdown](https://github.com/nilaoda/BBDown)的 Github 下载 BBdown 程序并添加环境变量 (不加也行)
## 依赖
使用 BBdown 需要 FFmpeg 或 mp4box  
从[FFmpeg](https://ffmpeg.org/)下载 FFmpeg 并配置环境变量 (必须配置)
# 使用 BBdown
打开Powershell/CMD  
我这里没有添加环境变量，所以在 BBdown 所在目录打开 Powershell/CMD  
运行 BBdown  
```
./bbdown
```
登录 BiliBili  
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


<meting-js server="netease" type="song" id="1377642003"></meting-js>

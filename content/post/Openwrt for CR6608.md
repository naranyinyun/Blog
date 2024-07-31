---
title: '为 CR6608 安装 Openwrt'
date: 2024-07-31T19:31:14+08:00
draft: flase
slug: "Openwrt for CR6608"
tags: ["Technology"]
description: "完整的 Openwrt Install Guide for CR6608"
categories: ["Technology"]
---
## 准备
1. Openwrt 固件
2. 一台**运行 Openwrt**的设备（辅助设备）
3. 一台 CR6608
## 获取 SSH 权限并刷入 pb-boot
## 辅助设备准备
将 [xqsystem.lua](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/CR660X%20Source/xqsystem.lua) 上传至辅助路由器的`/usr/lib/lua/luci/controller/admin/`
```shell
scp -O [path xqsystem.lua] [username]@[router ip]:/usr/lib/lua/luci/controller/admin/
```

上传后关闭辅助路由器的 DHCP 服务

### 降级
使用小米的路由器刷写工具刷入[此固件](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/CR660X%20Source/%E9%99%8D%E7%BA%A7%E5%9B%BA%E4%BB%B6/miwifi_cr6608_all_c11bb_1.0.100_2.bin)


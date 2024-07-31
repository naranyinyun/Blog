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
### 辅助设备准备
将 [xqsystem.lua](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/CR660X%20Source/xqsystem.lua) 上传至辅助路由器的`/usr/lib/lua/luci/controller/admin/`
```shell
scp -O [path xqsystem.lua] [username]@[router ip]:/usr/lib/lua/luci/controller/admin/
```

上传后关闭辅助路由器的 DHCP 服务，将 LAN 口 IP 改为 `169.254.31.1`

### 降级
使用小米的路由器刷写工具刷入[此固件](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/CR660X%20Source/%E9%99%8D%E7%BA%A7%E5%9B%BA%E4%BB%B6/miwifi_cr6608_all_c11bb_1.0.100_2.bin)
{{< notice notice-tip >}}
即便你刷了红米 AX1600 的固件，你依旧可以使用此固件获取 SSH
{{< /notice >}}

### 获取 SSH
对于 CR6608 设备，你可以直接使用路由器铭牌上的密码登录路由器后台。CR6609 也可。CR6606 需要进行 [SSH 密码计算](https://miwifi.dev/ssh)

登录路由器后台后，保存好 URL 中的 STOK 片段，例如
> http://192.168.31.1/cgi-bin/luci/;stok=[6b718c43fcad63e808594111ad4a4cb4]/web/home#router

方括号的部分即为 STOK
{{< notice notice-warning >}}
STOK 每次登录都会变化，请尽快完成接下来的操作
{{< /notice >}}

接下来，访问如下两个 URL
> http://[CR6608 IP]/cgi-bin/luci/;stok=[STOK]/api/misystem/extendwifi_connect?ssid=[辅助设备网络 SSID]&password=[辅助设备网络密码]
>  
> http://[CR6608 IP]/cgi-bin/luci/;stok=[STOK]/api/xqsystem/oneclick_get_remote_token?username=xxx&password=xxx&nonce=xxx

如果一切正常，两个 URL 均应返回 `code 0`. 如报错，请检查辅助设备配置并重试以上步骤
### 刷入 pb-boot
通过 SSH 连接 CR6608
``` shell
ssh root@[CR6608 IP]
```
密码即为路由器管理密码

下载[pb-boot](https://mirror.nalanyinyun.top/zh-CN/The%20Mirror%20of%20Source/CR660X%20Source/pb-boot/pb-boot.img)

``` shell
scp -O [pb-boot path] root@[CR6608 IP]:/tmp
ssh root@[CR6608 IP]
mtd write /tmp/pb-boot.img Bootloader
```
### 刷入 Openwrt

如果一切正常，断开路由器电源，然后按住 `reset` 并插入电源，直到路由器面板灯呈呼吸灯状
{{< notice notice-tip >}}
请使用网线连接 CR6608
{{< /notice >}}

打开 192.168.1.1 , 选择恢复固件，你可以刷入 `Kernel` 进行安装，也可以直接安装 `Factory`

如果你刷入 `Kernel` 镜像，进入后选择`系统`>`备份与升级`>`刷写新的固件`
{{< notice notice-warning >}}
请选择 Sysupgrade 镜像，如果你安装最新版的 Openwrt, 提示镜像校验失败是正常的，请忽略并刷入但
**必须确保你的镜像型号正确才能这么做！**
{{< /notice >}}

## 尾语
{{< notice notice-warning >}}
Openwrt 最新稳定版可能无法连接 SSH , 如遇此情况，切换到 Snapshot 版本即可
{{< /notice >}}
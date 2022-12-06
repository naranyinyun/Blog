---
title: "从 Pixiv 直连分析 GFW 和 SNI 阻断"
date: 2022-12-06T13:22:10+08:00
draft: false
slug: "D_C"
image: "https://tva1.sinaimg.cn/large/0072Vf1pgy1foxk7rv2gpj31hc0u04e6.jpg"
tags: ["Network"]
categories: ["Technology"]
---
# GFW 的屏蔽手段
## DNS 缓存污染 (DNS 投毒)
GFW 监听所有在 53 端口上使用 UDP 的 DNS 请求，若发现查询域名与黑名单匹配，GFW 会伪装成 DNS 服务器并返回虚假查询结果  
常见的有`127.0.0.1`,`1.1.1.1`,`0.0.0.0`  
可以通过使用 DoH 或 DoT 以规避 DNS 缓存污染  
## TCP 旁路阻断
GFW 检测到建立 TCP 连接的 IP 处于黑名单时，会抢先在服务器返回 ACK 之前向客户端发送一个 TCP Reset 报文提前终止 TCP 连接
## 路由扩散技术封锁TCP/UDP
GFW 的路由扩散技术会向各个路由节点重分发错误的路由表，发往被屏蔽 IP 的所有报文都会被错误的路由表引入一个黑洞路由  
但通过错误的路由表，也可以把报文引入一个服务器，服务器可以分析这些报文，也可以发送一个虚假的响应  
# SNI 阻断和直连
在 TLS1.3 中，客户端会首先向服务器发送一个`ClientHello`包  
SNI 允许客户端在`ClientHello`中直接请求指定的域名证书  
但 SNI 的有效负载没有加密，GFW 可以窃听其中的`Server Name`来匹配黑名单决定是否阻断链接  
我们用 WireShark 抓取一个`ClientHello`看看 (访问本站，本站支持 TLS1.3,QUIC,ESNI)：   

![WireShark](/post/direct_connect/WireShark.png)  

不难看到，`server name`中直接写着域名，GFW 通过查看此内容就可以阻断连接  
那看到这里，就有聪明的同学有疑问了： 
"既然 SNI 的有效负载是明文传输，那我给 SNI 的有效负载加密，不就可以绕过 SNI 阻断了吗"  
没错，这种机制叫做 ESNI，目前 GFW 对 ESNI 的策略是全部阻断....
## 直连
如果你在发给服务器的`Server Name`中填一个根本不存在的域名或者其他乱七八糟的东西  
服务器会返回给你一张默认的证书  
欸，那就巧了，Pixiv 的默认证书是一张`*.pixiv.net`的泛证书  
GFW 还没有屏蔽 Pixiv 的服务器 IP  
客户端就可以和服务器建立连接了

## 局限性
GFW 检测某个包是否违规就是通过检查`Server Name`判断是否阻断连接  
但问题是，服务器返回的默认证书不一定可用，甚至在接收到错误的`Server Name`时会直接拒绝连接  
而不同于服务器，虚拟服务器如果没有接收到有效`Server Name`就没法知道你要访问哪个服务  

晚安，"自由之人"

<meiting-js server="netease" type="song" id="1872393298">
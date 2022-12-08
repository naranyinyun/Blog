---
title: "在 Render 上部署 Alist V3"
date: 2022-12-08T21:06:19+08:00
draft: false
slug: "Alist_render"
image: "https://tva3.sinaimg.cn/large/0072Vf1pgy1foxkd6lx6jj31kw0w0wyb.jpg"
tags: ["Web"]
categories: ["Technology"]
---
# Deploy Alist on Render
## Alist
在 GitHub 上 fork [Alist 的仓库](https://github.com/alist-org/alist-render)  
最好在 fork 的时候改一下仓库名
## Database (Postgres)
在 Render 上部署 Alist 需要一个远程数据库,这里我用的是[ElephantSQL](https://www.elephantsql.com/)  ~~不得不说,这网站插图风格十分诡异~~  
在 ElephantSQL 上注册一个数据库，在 Detail 界面会得到一堆信息，这些一会儿要用  
## Render
注册一个 Render 账号，进入 Dashboard 之后：
1. 点击 New+
2. 选择 Web Service
3. 连接到你的 Github 账户
4. 选择刚才 fork 的 Github 仓库 (Branch 选择 v3)
5. 填写 Name，选择 Region 等基础信息
剩下的都别碰，划到最底下，点击 Advanced  
点击 Add Environment Variable
你需要将以下表格中的环境变量依次填入： 
|Key|Value|
|---|---|
|DB_HOST|填入 ElephantSQL 中的 Server 后的内容|
|DB_NAME|填入 User & Default database 后的内容  |
|DB_PASS|填入 Password 后的内容|
|DB_PORT|5432|
|DB_SSL_MODE|verify-full 或 disable|
|DB_TYPE|postgres|
|DB_USER|与 DB_NAME 一致|
|PORT|8080 或 443|
|CDN|https://unpkg.com/alist-web@$version/dist/ (可不填 Jsdelivr已被污染,不再考虑)|

点击最下方 Create Web Server  
完成，可选进行进一步配置，如配置自定义域名，在 Settings 中 
### 一些提示
IANA 把 5432 端口唯一分配给了 PostgresSQL  
若环境变量中无 CDN，默认使用本地 dist，速度较慢，推荐使用 Unpkg  
Render 每月有 750 小时的在线时间，**不要使用 UptimeBot 等阻止 Render 休眠**  
Render 前 500GB 流量免费，尽量不要开启下载代理
## 完成
享受 Alist 的强大功能，如果需要配置自定义域，推荐使用 Cloudflare 以便使用 CDN 和 WAF  

<meting-js server="netease" type="song" id="1857521048">

---
title: "在Hugo中添加Meting-JS和Aplayer"
date: 2022-11-16T20:52:36+08:00
draft: false
slug: "Aplayer"
image: "https://tva2.sinaimg.cn/large/0072Vf1pgy1foxkbxnphoj31hc0u0tpt.jpg"
tags: ["Hugo"]
categories: ["Technology","Web"]
---
# Meting-Js And Aplayer
## 添加 Meting-Js
在当前主题的`<head>`部分填入以下内容  
通过CDN引入(Jsdelivr):

{{< highlight html >}}
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>
{{< /highlight >}}

通过Unpkg CDN引入:  

{{< highlight html >}}
<!-- require MetingJS -->
<script src="https://unpkg.com/meting@2.0.1/dist/Meting.min.js"></script>
{{< /highlight >}}

## 添加Aplayer
在主题的`head`部分填入以下内容  
通过Jsdeliver CDN引入  

{{< highlight html >}}
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
{{< /highlight >}}

通过cdnjs CDN引入  

{{< highlight html >}}
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.css"></script>
{{< /highlight >}}

通过Unpkg CDN引入

{{< highlight html >}}
<!-- require APlayer -->
<link rel="stylesheet" href="https://unpkg.com/aplayer@1.10.1/dist/APlayer.min.css">
<script src="https://unpkg.com/aplayer@1.10.1/dist/APlayer.min.js"></script>
{{< /highlight >}}

## 更改Goldmark
在站点根目录中`config.toml`中寻找并修改以下内容(添加)

{{< highlight toml >}}
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
{{< /highlight >}}

`config.yaml`

{{< highlight yaml >}}
markup:
    goldmark:
        renderer:
            unsafe: true
{{< /highlight >}}

## 使用Meting-JS
参考 https://github.com/metowolf/MetingJS  
实例:

{{< highlight html >}}
<meting-js server="netease" type="song" id="1889184941">
{{< /highlight >}}

# 外部资源链接
[Meting-JS](https://github.com/metowolf/MetingJS)  
[Aplayer](https://aplayer.js.org/#/)  

<meting-js server="netease" type="song" id="22707008">
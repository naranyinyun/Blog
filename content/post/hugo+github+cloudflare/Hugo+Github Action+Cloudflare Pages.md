---
title: "使用 Hugo+Github Action+Cloudflare Pages 搭建博客"
date: 2022-11-11T20:32:27+08:00
draft: false
slug: "bdst"
tags: ["Hugo","CI","Cloudflare"]
categories: ["Web","Technology"]
---
# 我为什么把在本地构建的 Hugo 搬到 GitHub 上？
本来都在本地没什么，有时我也有多端编辑的需要  
但大多是先写 Markdown 再传到电脑上  
就这样，我的博客快乐的运行了半年  
直到今年九月，我用来存站点文件的硬盘坏了  
这一坏，啥都没了，我的站点没有备份  
这才下定决心把东西都搬到云端  
# Hugo+GitHub+Cloudflare
## Hugo
只需如往常一样使用 Hugo  
如果你的主题是通过`git clone`安装的，请进入主题目录删除`.Git`文件夹  
## Github
把你的站点文件全部上传到 GitHub，无需使用`hugo`来`Build`站点  
### Github Action
重中之重，如果没有 GitHub Action，把站点上传到 GitHub 将毫无意义 
新建一个仓库用于存储站点 

配置 Github-Tokens:
1. 打开 Settings
2. 打开 Developer settings
3. 展开 Personal access tokens
4. 选择 Tokens(classic)
5. 点击 Generate new tokens
6. 点击 Generate new tokens(classic)
7. 授予 `repo` 和 `workflow` 许可并调整过期时间
8. 保存 Token 一会儿要用

配置 Secrets:
1. 进入仓库并打开 settings
2. 展开 Secrets
3. 点击 Actions
4. 点击 New repository secret
5. 键入 `PERSONAL_TOKEN` 至 name
6. 键入 刚才配置的 Token 至 `Secrets`
7. 点击 Add secret



在你的站点目录新建`.github/workflows/hugo-build.yml`(文件名称随意)  
在文件中输入  
{{< highlight yaml >}}
name: github pages

on:
  push:
    branches:
      - main  # 选择构建分支(站点源文件)

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.108.0' #0.109.0 会出构建问题，我也不知道为啥
          # extended: true

      - name: Build
        run: hugo

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          personal_token: ${{ secrets.personal_token }}
          PUBLISH_BRANCH: CF-PAGES # 构建后推送到的分支
          publish_dir: ./public # 构建后存储到的文件夹
{{< / highlight >}}
**中文注释，在使用时编码必须为 UTF-8，如报错可删去注释**  
**extended 别删，大多数时候都会用到扩展版**

`Push`到`Main`即可测试是否可用

## Cloudflare Pages
配置 Cloudflare Pages:
1. 点击 Pages
2. 点击 创建项目
3. 点击 连接到 Git
4. 添加 账户并选择仓库
5. 选择 生产分支 (Action 构建后推送的分支)
6. 键入 啥也别键入，别碰构建设置
7. 点击 保存并部署
8. 处理 剩余事项

## All Done
大功告成，你的 Hugo 站点已经部署到 Cloudflare 服务器，站点在全球均可访问！

# TL;DR
你可以 Fork[我的仓库](https://github.com/naranyinyun/Blog)进行爆改  
本仓库使用 GPL 3.0 协议，请您遵守开源许可  

<meting-js server="netease" type="song" id="1356059919"></meting-js>

---
title: "我和 Hugo 的爱恨情仇"
date: 2022-12-02T12:54:25+08:00
draft: false
slug: "Why Hugo"
image: "https://tva4.sinaimg.cn/large/0072Vf1pgy1foxli0u4b3j31hc0u0qoj.jpg"
tags: ["Hugo"]
categories: ["Technology"]
---
# Hugo
## 为什么选择 Hugo?
关于此问题的答案, 你可以在网上找到太多太多  
比如 Hugo 是使用 Go 语言编写的，相较于使用 Javascript 的 Hexo 和使用 Ruby 的 Jekyll,Hugo 的速度可以说吊打，无论是创建，构建  
但对于我来说，Hugo 的绝大多数优点都抵不过这一个  
` 简单 `  
没错, Hugo 的配置, 使用, 乃至他的文件结构都易于理解且方便使用  
配置主题没有那么多繁琐的步骤, 自行修改也极其方便  
Hugo 自带的 Web 服务器也易于调试, 几乎可以实时的显示你的更改  
Hugo 的文档也十分干净, 不像 Jekyll, 他们的文档写的好像歧视 Windows 用户  
## 为什么不是 Hugo
Hugo 在部署博客方面无疑是极强的, 但部分人觉得他的一大问题就是社区太小, 或者说中文社区太小  
这就要求你在使用 Hugo 的时候必须有基础的英文能力, 一些调试经验和智慧的大脑  
他的主题不能说少, 但和 Hexo 相比就相形见绌了, Hexo 在中文社区的火爆程度可以用烂大街形容   
大部分的独立博客都是基于 Hexo 的  
但这都是和其他框架比, 该说说我遇见的糟心事了  
另外, Hugo 能够对上眼的主题太少了, 我能对上眼的就三个,[Doks](https://getdoks.org/),[kagome](https://github.com/miiiku/hugo-theme-kagome) 和 [Stack](https://github.com/CaiJimmy/hugo-theme-stack)  
最近, 我想找一个个人主页主题来彻底替代 Jekyll, 没什么, 我就是单纯的不喜欢这个框架  
但是我找来找去, 发现一件事:  
**这咋都是博客主题**  
到现在也没有换掉 Jekyll...  
## Hugo,NodeJS 和 Doks
[Doks](https://getdoks.org/) 是一个现代化的文档主题, 基于 Hugo   
但是在部署他的过程中, 要使用 NodeJS, 或者说 NPM  
现在的 NPM 性能问题没那么严重了, 但我还是不愿意使用  
`Clone`,`npm install`  
然后问题就来了,`NPM` 卡住了..., 卡住了...  
Highlight-JS 这个玩意根本就不在 NPM 的服务器上, 我看他卡了 5 分钟才去访问链接看一下  
OK 完全没问题, 这都可以我自行解决, 更糟心的还在后面  
`npm run start`  
他启动了 Hugo 的预览服务器, 和我自己 `hugo server` 的效果一样  
但是我在改文件的过程中发现了一件事:  
我在改文件, Hugo 也检测到文件更改重新生成站点  
但是浏览器上的内容纹丝不动  
我甚至直接把文件删了, 他还是没反应  
我重新启动了一下 Hugo 服务器, 好了  
然后我继续改文件, 改到路径的时候 - 意外发生了  
404, 没错, 404, 我试着用 URL 直接访问根目录里的文件, 还是 404  
显然, 这玩意根本就没同步我的更改  
那我改了半天改个寂寞呢  
后来又是一样的毛病, 一直持续到我受不了了  
我自己在根目录运行了 `hugo server`  
他居然好使了, 我也不知是谁的毛病, 但是我觉得嫌疑最大的是 NodeJS, 我用 `yarn run start` 他还是一样不同步更改  
我实在是被折腾烦了, 就直接 `npm run build`, 部署到 Cloudflare Pages, 一看正常了  
就挺无语的  
## 我为什么还用 Hugo
因为 Hugo 的设计, 操作都十分契合我 ~~ 懒得学~~  
即使他和 NodeJS 一起用的时候很糟心  
但我依旧不会忘记  
> 在那个寒冷的冬夜  
> 在 Hexo 无情折磨我的那个冬夜  
> 是 Hugo   
> 带给了我黎明一般的曙光  

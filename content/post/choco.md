---
title: '在 Windows 上安装 Chocoatey'
date: 2023-12-17T19:17:17+08:00
draft: false
slug: "choco"
description: "Chocolatey 是一个 Windows 下的包管理器，就像 APT, 它允许你只用终端就能管理电脑上的软件"
---
# 安装
## 通过 .nupkg 离线安装
访问 [Chocolatey Installation](https://chocolatey.org/install) , 转至 `Step 2`, 选择 `PS DSC`, 下滑，选择 `Download` , 关于 PowerShell 上的离线安装，这里不做过多介绍，如需参考，转至 [Microsoft Learn | Manual Package Download](https://learn.microsoft.com/en-us/powershell/gallery/how-to/working-with-packages/manual-download?view=powershellget-3.x)
## 通过在线脚本安装
以管理员权限打开 `PowerShell`, 输入
``` Powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
等待脚本运行完成
{{< notice notice-info >}}
如果 PowerShell 提示 ` 无法加载文件 <any file> ，因为在此系统上禁止运行脚本`, 在管理员 PowerShell 中输入 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`
{{< /notice >}}

{{< notice notice-warning >}}
如果你不知道你在做什么，请在安装之后切换回 `Restricted`, `RemoteSinged` 和更宽松的执行策略可能会导致严重的安全性问题
{{< /notice >}}
## 使用
### 修改默认安装路径
在高级系统设置中点击编辑系统环境变量，点击 Path , 将 `C:\ProgramData\chocolatey\bin` 改为你希望安装的路径，我选择的是 `D:\ChocolateySoftware`
{{< notice notice-note >}}
如果不更改安装路径，你的每一次操作都需要在管理员 PowerShell 中运行
{{< /notice >}}
### CLI 用法
``` Shell
# 安装软件
choco install adb

# 卸载软件
choco uninstall adb

# 搜索软件
choco search adb

# 查看本地已经安装的软件
choco list -lo

# 更新
choco upgrade adb

# 查看版本
choco version adb
``` 

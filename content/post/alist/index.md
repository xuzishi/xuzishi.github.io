---
title: Alist
subtitle: 

# Summary for listings and search engines
summary: Alist - private netdisk

# Link this post with a project
projects: []

# Date published
date: '2023-09-02T00:00:00Z'

# Date updated
lastmod: '2023-09-02T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: ''
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Alist

categories:
  - Notes
---


# 云盘服务
采用 AList 部署私有云盘
https://github.com/alist-org/alist/releases

## Windows
cd 到解压目录下，运行程序：
` .\alist.exe server `
获得管理员信息：
` .\alist.exe admin `
会提示管理员用户名和密码。

可以新建一个vbs文件，使其后台启动：
``` vb
Dim ws
Set ws = Wscript.CreateObject("Wscript.Shell")
ws.run "alist.exe server",vbhide
Wscript.quit
```
可以通过把该vbs文件快捷方式到 启动 文件夹中，实现开机自启。

停止服务的vbs：
``` vb
Dim ws
Set ws = Wscript.CreateObject("Wscript.Shell")
ws.run "taskkill /f /im alist.exe",0
Wscript.quit
```

在浏览器中打开 ` 127.0.0.1:5244 ` 进入管理后台，用上一步提示的用户名和密码登录。
右下方 管理 可以进行设置。

## 添加本地文件挂载
存储 - 添加
驱动：本机存储 - 挂载路径：网盘中的路径 - 根文件夹路径：本机需要挂载的根文件夹
另可设置权限

## 添加用户
用户 - 添加
设置用户名和密码 - 基本路径：该用户可访问的路径 - 权限


## References
[AList 文档 - 手动安装](https://alist.nn.ci/zh/guide/install/manual.html)

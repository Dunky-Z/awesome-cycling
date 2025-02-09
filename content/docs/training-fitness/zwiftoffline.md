---
title: "ZwiftOffline"
description: ""
summary: ""
date: 2025-02-09T13:04:48+02:00
lastmod: 2025-02-09T13:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

[ZwiftOffline](https://github.com/zoffline/zwift-offline?tab=readme-ov-file)是一个开源社区自制的 Zwift 的 server 端，可以在没有网络的情况下进行 Zwift 课程或路线训练，多平台支持。

## 安装 ZwiftOffline

- 从[GitHub Release 页面](https://github.com/zoffline/zwift-offline/releases/latest)下载最新的 zoffline 发布版。
- 找一个目录用于运行 Zwift offline，我新建了一个`zwiftoffline`目录，保存刚刚下载的`exe`文件，然后运行你下载的 zoffline.exe。一旦运行，zoffline 会在其所在的相同文件夹中创建一个`storage`目录，用以保存你的 Zwift 进度。
- 从[GitHub Rlease](https://github.com/oldnapalm/zoffline-helper/releases/latest)下载配置脚本等文件，将其也解压到`zwiftoffline`目录。
- 进入`zwiftoffline/zoffline-helper`目录，右键点击`configure_client.bat`，选择以管理员身份运行。这个脚本会自动配置 zoffline，以便你可以在本地运行 Zwift。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/6769deefaa7c142c42411a43af345e8d.png)
- 前往[Zwift 官网](https://www.zwift.com/)，拉到页面底部，可以看到安装链接，安装 Zwift 软件。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/734f7507b1e68958bba2ea2525216752.png)
- 进入`zwiftoffline`目录，双击`zoffline_1.0.140279.exe`，运行 zoffline。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/029bd1af360095a4a279b52c822cd5c7.png)
- 启动原版 Zwift 程序，点击 Start Zwfit 即可开始骑行，**如果显示的页面还是原来 Zwift 的登录页面，看看是不是开了代理，关闭代理再试试**。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/e577c5169d652b1ae201a337a0d292f8.png)

## 获取个人原来的 Zwift 资料信息

如果不配置这一项，那么使用 Zwift offline 骑行的时候，会显示你的信息是一个新的账号，而不是你原来的账号。

在登录页面可以进入设置：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/ce3667b3f69bf3ab3fd81c191aee51f8.png)

填写邮箱和密码，勾选所有选项，点击 Submit 即可：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/9cc77352a1f299516e1f76989bdc60c3.png)

这样再登录到 Zwift 时就是原来的账号了。

## 链接 Strava 上传活动

登录[Strava](https://www.strava.com/settings/api)，申请 API，获取`Client ID`和`Client Secret`。

填写内容可以参考下图：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/d8024be9518e5a262538aa5d48c7fbb0.png)

授权回调域：launcher.zwift.com

申请完成后会得到下面的信息：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/a5024f9e2e150810251222315be11ac9.png)

在登录页面可以进入设置，填写得到的`Client ID`和`Client Secret`。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/29afa480ea0c6ceba03f89a14b30c987.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/84b0932cd611d78a1497f82aafa86fb7.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/2457689c2493d63ffa77e465948d3d84.png)

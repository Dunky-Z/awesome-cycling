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
- 找一个目录用于运行 Zwift offline，我新建了一个`zwiftoffline`目录，保存刚刚下载的`exe`文件，然后运行你下载的 zoffline.exe。一旦运行，zoffline 会在其所在的相同文件夹中创建一个`storage`目录，用以保存你的 Zwift 进度。生成`storage`目录后，按`Ctrl+C`先关闭 zoffline，稍后还有其他配置。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/10/ed838fae543dc8d607c231d89fc4888b.png)
- 前往[Zwift 官网](https://www.zwift.com/)，拉到页面底部，可以看到安装链接，安装 Zwift 软件。记住安装的路径，我安装在了`C:\Program Files (x86)\Zwift`。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/734f7507b1e68958bba2ea2525216752.png)
- 运行 Zwift，这时候客户端会开始更新，因为安装的只是一个登录器，游戏本体还需要下载。**一定要安装之后就执行这一步，因为后续的配置会改变网络配置，导致无法下载游戏本体。**
- 从[GitHub Rlease](https://github.com/oldnapalm/zoffline-helper/releases/latest)下载配置脚本等文件`zoffline-helper.zip`，将其也解压到`zwiftoffline`目录。
- 进入`zwiftoffline/zoffline-helper`目录，右键点击`configure_client.bat`，选择以管理员身份运行。这个脚本会自动配置 zoffline，以便你可以在本地运行 Zwift。期间会弹窗让你选择Zwift目录，就是之前需要记住的安装目录：
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/19/52b44adfe177bde733156c3d2faefe5e.png)
  - 最终运行完的结果如下：
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/6769deefaa7c142c42411a43af345e8d.png)
- 进入`zwiftoffline`目录，双击`zoffline_1.0.140279.exe`，运行 zoffline。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/029bd1af360095a4a279b52c822cd5c7.png)
- 启动原版 Zwift 程序，**如果显示的页面还是原来 Zwift 的登录页面，看看是不是开了代理，关闭代理再试试**。
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/e577c5169d652b1ae201a337a0d292f8.png)
- 下图是官方原版登录界面，**如果显示这个页面说明配置失败**：
  - ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/19/d8c93c7c78d2f33555bed4a3be9d671f.png)
- 将输入法切换为微软英文输入法，点击`Start Zwift`即可开始游戏。如果是搜狗输入法将会卡在登录页面。

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

其中授权回调域填写：launcher.zwift.com

申请完成后会得到下面的信息：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/a5024f9e2e150810251222315be11ac9.png)

在登录页面可以进入设置，填写得到的`Client ID`和`Client Secret`。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/29afa480ea0c6ceba03f89a14b30c987.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/84b0932cd611d78a1497f82aafa86fb7.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/2457689c2493d63ffa77e465948d3d84.png)

右击管理员运行`zoffline-helper/disable_zoffline.bat`，这一步把hosts的配置都清除。

命令行里运行`zoffline-helper/strava_auth.exe --client-id CLIENT_ID --client-secret CLIENT_SECRET`，把CLIENT_ID和CLIENT_SECRET替换成你的strava应用的client id和client secret。

浏览器打开`localhost:8000`授权访问。

把目录中生成的`strava_token.txt`移动到目录`storage/1`下。

右击管理员运行`zoffline-helper/configure_client.bat`，重新配置hosts。

## 上传训练课程

虽然Zwift有很多训练课程，但是我还是习惯在Intervals ICU上创建好自己的课程，然后上传到Zwift。虽然Intervals ICU上的课程可以直接同步到Zwift，但是单机版的没法同步这些课程，所以只能手动上传。

具体如何创建课程我就不多说了，这里假设你已经有了一系列`.zwo`训练课程文件，那么你只需要将其保存到`Documents/Zwift/Workouts/1`目录下即可：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/15/f18d29b2d3e548bf2fe0878d54b2f45f.png)

> 注意哦，不是运行目录下的`zwiftoffline\storage\1\customworkouts`哦，开始我自作聪明把课程放到这个目录下，结果发现上传不了，后来才发现是放错了。

## 常见问题

### 卡在蓝色登录界面

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/20/03f08f3fa8d593d33b38647a46f22341.png)

进程管理中关闭Zwift，输入法需要切换为微软英文输入法重新登录：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/20/48a6263e5ffe475ec5753b13cffd2ec1.png)

### 配置Zwiftoffline后无法更新Zwift

因为`configure_client.bat`会修改Hosts文件，导致无法连接到Zwift服务器，所以在更新Zwift时需要先关闭`zoffline`，然后再更新。可以进入`zwiftoffline/zoffline-helper`目录，右键点击`disable_zoffline.bat`，选择以管理员身份运行，可以清除网络配置，然后再打开Zwift开启更新。

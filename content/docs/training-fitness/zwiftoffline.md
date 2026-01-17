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

## 前言

[ZwiftOffline](https://github.com/zoffline/zwift-offline?tab=readme-ov-file)是一个开源社区自制的 Zwift 的 server 端，可以在没有网络的情况下进行 Zwift 课程或路线训练，多平台支持。

本教程将详细介绍如何在 Windows 系统上安装和配置 Zwift 单机版，包括基础安装、账号配置、Strava 同步、训练课程上传以及移动端 Companion 配置等完整流程。

## 准备工作

### 下载必要文件

1. **ZwiftOffline 主程序**
   - 从[GitHub Release 页面](https://github.com/zoffline/zwift-offline/releases/latest)下载最新的 zoffline 发布版（`.exe`文件）

2. **配置辅助工具**
   - 从[GitHub Release](https://github.com/oldnapalm/zoffline-helper/releases/latest)下载`zoffline-helper.zip`配置脚本文件

3. **Zwift 官方客户端**
   - 前往[Zwift 官网](https://www.zwift.com/)，拉到页面底部，下载并安装 Zwift 软件
   - **重要**：记住安装路径，后续配置需要用到（例如：`C:\Program Files (x86)\Zwift`）

### 创建运行目录

创建一个目录用于存放 ZwiftOffline 相关文件，例如新建`zwiftoffline`目录。

## 基础安装与配置

### 初始化 ZwiftOffline

1. 将下载的`zoffline.exe`文件保存到`zwiftoffline`目录
2. 运行`zoffline.exe`，程序会在同目录下自动创建`storage`目录（用于保存 Zwift 进度）
3. 看到`storage`目录生成后，按`Ctrl+C`关闭 zoffline，稍后进行配置

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/10/ed838fae543dc8d607c231d89fc4888b.png)

### 安装并更新 Zwift 客户端

1. 运行刚安装的 Zwift 程序，客户端会开始更新游戏本体
   - **⚠️ 重要提示**：必须在配置网络之前完成此步骤，因为后续配置会修改 hosts 文件，导致无法连接到 Zwift 服务器下载游戏本体

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/734f7507b1e68958bba2ea2525216752.png)

### 配置网络连接

1. 将下载的`zoffline-helper.zip`解压到`zwiftoffline`目录
2. 进入`zwiftoffline/zoffline-helper`目录
3. 右键点击`configure_client.bat`，选择**以管理员身份运行**
4. 脚本会自动配置 zoffline，期间会弹窗让你选择 Zwift 安装目录（即之前记住的路径）

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/19/52b44adfe177bde733156c3d2faefe5e.png)

5. 配置完成后，会显示如下结果：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/6769deefaa7c142c42411a43af345e8d.png)

### 启动并验证

1. 进入`zwiftoffline`目录，双击运行`zoffline.exe`（文件名可能因版本而异，如`zoffline_1.0.140279.exe`）

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/029bd1af360095a4a279b52c822cd5c7.png)

2. 启动原版 Zwift 程序，检查登录界面
   - **成功标志**：显示 ZwiftOffline 的登录页面（如下图）

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/e577c5169d652b1ae201a337a0d292f8.png)

   - **失败标志**：如果显示官方原版登录界面，说明配置失败

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/19/d8c93c7c78d2f33555bed4a3be9d671f.png)

3. **⚠️ 重要提示**：
   - 如果显示的是原版登录页面，检查是否开启了代理，关闭代理后重试
   - 将输入法切换为**微软英文输入法**，点击`Start Zwift`开始游戏
   - 使用搜狗输入法等第三方输入法可能会卡在登录页面

## 高级配置

### 同步原有账号信息

如果不配置此项，使用 Zwift offline 时会显示为新账号，而不是你原来的账号信息。

**配置步骤：**

1. 在登录页面点击设置按钮进入设置界面

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/ce3667b3f69bf3ab3fd81c191aee51f8.png)

2. 填写你的 Zwift 邮箱和密码，勾选所有选项，点击 Submit 提交

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/9cc77352a1f299516e1f76989bdc60c3.png)

3. 配置完成后，再次登录 Zwift 时就会显示为原来的账号了

### 配置 Strava 自动上传

#### 申请 Strava API

1. 登录[Strava API 设置页面](https://www.strava.com/settings/api)
2. 创建新应用，填写以下信息：
   - **应用名称**：自定义（如：ZwiftOffline）
   - **类别**：其他
   - **授权回调域**：`launcher.zwift.com`
   - **网站**：可留空或填写个人网站

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/d8024be9518e5a262538aa5d48c7fbb0.png)

3. 申请完成后，记录下`Client ID`和`Client Secret`

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/a5024f9e2e150810251222315be11ac9.png)

#### 在 ZwiftOffline 中配置 Strava

1. 在登录页面进入设置，填写`Client ID`和`Client Secret`

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/29afa480ea0c6ceba03f89a14b30c987.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/84b0932cd611d78a1497f82aafa86fb7.png)

点击`Submit`提交：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/2457689c2493d63ffa77e465948d3d84.png)

#### 授权 Strava 访问

> 这一步可以省略，如果通过上面的步骤没法上传，再尝试这个步骤手动配置

1. 右键以管理员身份运行`zoffline-helper/disable_zoffline.bat`，清除 hosts 配置
2. 在命令行中运行以下命令（替换`CLIENT_ID`和`CLIENT_SECRET`为你的实际值）：

   ```bash
   zoffline-helper/strava_auth.exe --client-id CLIENT_ID --client-secret CLIENT_SECRET
   ```

3. 浏览器会自动打开或手动访问`localhost:8000`进行授权

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/05/18/4b0dbbd3bd2dd82b1c6da8327e494ea3.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/05/18/05c02cfd9cd98aaf1e198d2f99b58f5a.png)

4. 授权完成后，将生成的`strava_token.txt`文件移动到`storage/1`目录下
5. 右键以管理员身份运行`zoffline-helper/configure_client.bat`，重新配置 hosts

### 上传自定义训练课程

如果你习惯在 Intervals ICU 等平台创建训练课程，可以手动上传到 Zwift 单机版。

**上传步骤：**

1. 将你的`.zwo`训练课程文件保存到以下目录：

   ```
   Documents/Zwift/Workouts/1
   ```

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/15/f18d29b2d3e548bf2fe0878d54b2f45f.png)

2. **⚠️ 注意**：不是`zwiftoffline\storage\1\customworkouts`目录，如果放错位置会导致课程无法上传

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/15/edd5d0ab56c733e794d196838851dfe3.png)

### 配置 Garmin Connect

Garmin Connect 可以同步你的 Zwift 活动数据到 Garmin 设备。

#### 配置账号

1. **PC 端配置**
   - 在 ZwiftOffline 登录窗口点击"Settings - Garmin"按钮
   - 输入你的 Garmin Connect 账号和密码

2. **安卓端配置**
   - 访问 `https://<zoffline_ip>/garmin/zoffline/`
   - 输入你的 Garmin Connect 账号和密码
   - 将`<zoffline_ip>`替换为运行 zoffline 的电脑 IP 地址

#### 多因素认证（MFA）

如果你的账号启用了多因素认证，需要额外配置：

1. **使用 Python 脚本（推荐）**
   - 运行`garmin_auth.py`脚本
   - 脚本会在运行目录下生成`garth`文件夹
   - 将`garth`文件夹移动到`storage/1`目录下

2. **使用 Windows 可执行文件**
   - 如果未安装 Python，可以从[zoffline-helper Release 页面](https://github.com/oldnapalm/zoffline-helper/releases/latest)下载`garmin_auth.exe`
   - 运行`garmin_auth.exe`，同样会生成`garth`文件夹
   - 将`garth`文件夹移动到`storage/1`目录下

### 配置 Intervals.icu

Intervals.icu 是一个强大的训练分析平台，可以同步 Zwift 活动数据。

#### 获取 API 凭证

1. 登录 [Intervals.icu 设置页面](https://intervals.icu/settings)
2. 进入"Developer Settings"（开发者设置）部分
3. 复制以下信息：
   - **Athlete ID**（运动员 ID）
   - **API Key**（API 密钥）

#### 配置账号

1. **PC 端配置**
   - 在 ZwiftOffline 登录窗口点击"Settings - Intervals"按钮
   - 输入之前复制的 Athlete ID 和 API Key

2. **安卓端配置**
   - 访问 `https://<zoffline_ip>/intervals/zoffline/`
   - 输入 Athlete ID 和 API Key
   - 将`<zoffline_ip>`替换为运行 zoffline 的电脑 IP 地址

### 启用多人游戏

多人游戏功能允许多个用户同时连接到同一个 zoffline 服务器进行骑行。

#### 基本配置

1. 在`storage`目录下创建`multiplayer.txt`文件（文件内容为空）

#### 远程服务器配置

如果 zoffline 运行在与 Zwift 客户端不同的 PC 上：

1. 在`storage`目录下创建`server-ip.txt`文件
2. 文件内容填写运行 zoffline 的 PC 的 IP 地址
3. **端口要求**：确保以下端口在运行 zoffline 的 PC 上开放：
   - TCP 端口：80, 443, 3025
   - UDP 端口：3024

#### 创建账号

1. 启动 Zwift，创建新账号
2. **⚠️ 注意**：此账号仅存在于你的 zoffline 服务器上，与官方 Zwift 账号无关

#### 启用密码重置功能（可选）

1. 在`storage`目录下创建`gmail_credentials.txt`文件
2. 文件内容格式：

```text
<gmail 账号>
<应用密码>
<恢复 URL 主机（可选）>
```

3. **获取应用密码**：
   - 访问 <https://security.google.com/settings/security/apppasswords>
   - 创建应用密码，允许服务器登录
   - 将生成的应用密码填入文件第二行
4. **恢复 URL 主机**（可选）：
   - 第三行可以填写恢复 URL 的主机地址
   - 如果不填写，将使用服务器 IP 地址作为默认值

### 启用 Ghosts（幽灵）

Ghosts 功能可以保存你之前的骑行记录，并在相同路线上显示为"幽灵"与你一起骑行。

#### 启用功能

1. **PC 端**

- 在 zoffline 启动器窗口中勾选"Enable ghosts"

2. **安卓端**

- 浏览器访问 `https://<zoffline_ip>/user/zoffline/`
- 勾选"Enable ghosts"
- 点击"Start Zwift"保存设置，点击后会跳转到无法访问页面不用管，这时候切换到客户端图标点击进入游戏即可。

#### 使用说明

1. **保存幽灵**：当你保存活动时，幽灵会自动保存在`storage/<player_id>/ghosts/<world>/<route>`目录下
2. **加载幽灵**：下次骑行相同路线时，幽灵会自动加载
3. **重新编组**：在聊天中输入`.regroup`命令可以重新编组幽灵

#### 自定义装备

1. 在`storage`目录下创建`ghost_profile.txt`文件
2. 可以使用`find_equip.py`脚本来自动填充此文件

### 启用 Bots（机器人）

Bots 功能可以将保存的幽灵转换为持续骑行的机器人，无论你选择什么路线，它们都会继续骑行。

#### 启用功能

- 前往[zoffline-bots 仓库](https://github.com/oldnapalm/zoffline-bots)下载机器人文件`bots.zip`
- 解压后将`bots/storage`目录下的文件复制到zwiftoffline的`storage`目录下
    ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2026/01/17/73b5c2e558cb006a07c35940c092dd05.png)
- `enable_bots.txt`文件内容可以包含一个倍数（如：`2`表示双倍机器人数量）
   - **⚠️ 警告**：如果机器人数量过多，可能导致性能问题或功能失效

#### 控制命令

在聊天中使用以下命令控制机器人：

- `.group`：编组机器人
- `.groupall`：编组所有机器人（包括使用倍数时的重复机器人）
- `.autogroup`：自动编组（当你改变路线时）
- `.autogroupall`：自动编组所有机器人
- `.stopautogroup`：停止自动编组
- `.disperse`：随机化机器人位置

#### 自定义机器人

1. 在`storage`目录下创建`bot.txt`文件
2. 可以自定义机器人的名称、国籍和装备

### 配置 RoboPacers（机器人配速员）

RoboPacers 是使用功率模拟器保存的幽灵，可以创建完美的循环配速员。

#### 获取 RoboPacers

- 上一步下载的机器人文件中已经包含了 RoboPacers，直接使用即可。

#### 创建要求

要创建可用的 RoboPacer，需要满足以下条件：

1. **更新频率**：必须使用 1 秒的更新频率录制（默认是 3 秒）
2. **循环要求**：活动必须从同一位置和速度开始和结束，否则机器人无法平滑循环
3. **配置文件要求**：
   - 必须包含唯一的玩家 ID
   - 必须包含路线 ID
   - 这样当你加入机器人时，会在交叉路口走相同的转弯

#### 编辑工具

1. **bot_editor.py 脚本**：可以用于修改以下文件：
   - `profile.bin`：设置名称、玩家 ID 和路线 ID
   - `route.bin`：裁剪多余的点以创建完美循环

#### 创建动态 RoboPacer

要创建动态 RoboPacer（在上坡时增加功率，下坡时减少功率）：

1. 使用 [standalone_power.py](https://github.com/oldnapalm/zwift-offline/blob/master/standalone_power.py) 脚本
2. **硬件要求**：
   - 2 个 ANT 适配器
   - [python-ant](https://github.com/mch/python-ant)
   - [PowerMeterTx.py](https://github.com/oldnapalm/zwift-offline/blob/master/PowerMeterTx.py)

### 使用 Bookmarks（书签）

书签功能可以保存你的位置，方便快速跳转到特定地点。

#### 自动保存书签

当你完成活动时，你的最后位置会自动保存为书签。

#### 手动保存书签

在聊天中使用以下命令保存书签：

```text
.bookmark <名称>
```

例如：`.bookmark road2sky`

#### 使用书签

1. **从书签开始新活动**：
   - 在主页屏幕选择"Join a Zwifter"
   - 选择你想要的书签

2. **传送到书签**：
   - 使用操作栏上的传送图标
   - 选择目标书签进行传送

### 启用历史排行榜

历史排行榜功能可以覆盖 60 分钟的实时结果和 90 天的个人记录，显示所有时间的最佳成绩。

#### 启用功能

1. 在`storage`目录下创建`all_time_leaderboards.txt`文件（文件内容可以为空）

#### 功能说明

- **排行榜**：显示所有时间的最佳成绩，而不仅仅是最近 60 分钟或 90 天的记录
- **荣誉衫**：仍然有效期为 60 分钟，但只有在创造新的历史记录时才会授予

### 解锁装备

可以解锁特殊装备或所有装备。

#### 解锁特殊装备

1. 在`storage`目录下创建`unlock_entitlements.txt`文件（文件内容可以为空）
2. 这将解锁需要特殊权限的装备

#### 解锁所有装备

1. 在`storage`目录下创建`unlock_all_equipment.txt`文件（文件内容可以为空）
2. 这将解锁所有可用装备

### 配置 CDN 代理

CDN 代理功能可以从 Zwift 官方服务器获取地图时间表和更新文件。

#### 启用 CDN 代理

1. 在`storage`目录下创建`cdn-proxy.txt`文件（文件内容可以为空）
2. **⚠️ 限制**：此功能只能在 zoffline 运行在与 Zwift 客户端不同的机器上时使用

#### 禁用代理

默认情况下，zoffline 会尝试使用 Google 公共 DNS 来解析 Zwift 主机名，即使 zoffline 与 Zwift 客户端运行在同一台机器上也能工作。

1. 如果要禁用此代理功能，在`storage`目录下创建`disable_proxy.txt`文件

#### 从 zoffline 提供更新文件

1. 运行`get_gameassets.py`脚本下载游戏文件
2. 这样 zoffline 可以直接提供更新文件，而不需要从 Zwift 服务器获取

## 移动端 Companion 配置

Zwift Companion 是配套的移动端社交软件，可用于与骑友互动、配对设备、点赞、使用道具等功能。使用离线版 Zwift 需要重新打包 Companion 应用。

### 准备工作

官方原版 Companion 会对网络连接和证书做严格验证，需要对其进行"打补丁并重签名"才能连接到本地 zoffline 服务器。

### 替换 APK 证书并重新签名

#### 安装 apk-mitm

1. 安装 Node.js（如果尚未安装）
2. 使用以下命令全局安装 apk-mitm：

```bash
npm install -g apk-mitm
```

3. 其他系统可参考[apk-mitm 项目 README](https://github.com/shroudedcode/apk-mitm)自行安装

#### 修改 apktool 配置

1. 使用`npm root -g`查找 apk-mitm 的实际安装路径
2. 打开`apk-mitm/dist/tools/apktool.js`文件
3. 修改`decode`方法，添加`-resm`和`dummy`参数：

```js
    decode(inputPath, outputPath) {
        return this.run([
            'decode',
            '-resm', // add this
            'dummy', // add this
            inputPath,
            '--output',
            outputPath,
            '--frame-path',
            this.options.frameworkPath,
        ], 'decoding');
    }
```

#### 生成修改后的 APK

1. 从[Zwift Offline 仓库](https://github.com/zoffline/zwift-offline)下载以下文件：
   - `ssl/cert-zwift-com.pem`（证书文件）
   - `zwift-offline-companion.apk`（原始 APK 文件）

2. 将这两个文件复制到同一目录（如：`C:\Users\Administrator\Desktop\zwift-offline-companion`）

3. 在该目录下运行以下命令：

```bash
apk-mitm --certificate cert-zwift-com.pem zwift-offline-companion.apk
```

4. 命令执行完成后，会生成`zwift-offline-companion-patched.apk`文件，将其拷贝到手机安装即可

### 配置域名重定向

#### 安装 Virtual Hosts

1. 下载[virtual hosts](https://github.com/x-falcon/Virtual-Hosts/releases/latest)软件
2. 安装到手机中

#### 创建 hosts 文件

1. 创建`hosts.txt`文件，内容如下（将`<zoffline ip>`替换为你运行 zoffline 的电脑 IP 地址）：

```
<zoffline ip> us-or-rly101.zwift.com
<zoffline ip> secure.zwift.com
```

2. **⚠️ 重要提示**：如果在 PC 上配置过 hosts 文件，可能包含以下映射：

```
127.0.0.1 cdn.zwift.com
```

   **此映射不要添加到手机端的 hosts 文件中！**

3. 将`hosts.txt`文件复制到手机，放在便于访问的位置

#### 启用域名重定向

1. 打开 Virtual Hosts 软件
2. 选择之前创建的`hosts.txt`文件
3. 启用域名重定向功能

### 使用 Companion

1. 使用离线版的账号登录 Companion，即可正常使用
2. **验证连接**：在打开和登录 Companion 时，观察 PC 端运行的 Zwift offline 命令行窗口是否有日志输出
   - 如果有日志输出，说明连接正常
   - 如果没有任何输出，说明请求未成功转发，需要检查 IP 地址配置是否正确

## 安卓设备直接使用 Zwift Offline

除了在 PC 上使用 Zwift Offline，你也可以直接在安卓设备上运行 Zwift 并连接到 zoffline 服务器。这种方式不需要 root 权限，但需要在每次安装或更新 Zwift 后重新打补丁。

### 安装必要应用

#### 下载并安装 ZofflineObb

1. 从[GitHub Release 页面](https://github.com/Argon2000/ZofflineObbAndroid/releases/latest)下载`ZofflineObb.apk`
2. 安装到安卓设备上（需要允许安装未知来源应用）

#### 下载并安装 Virtual Hosts

1. 从[GitHub Release 页面](https://github.com/x-falcon/Virtual-Hosts/releases/latest)下载`app-Github-release.apk`
2. 安装到安卓设备上

### 配置域名重定向

#### 创建 hosts.txt 文件

1. 创建`hosts.txt`文件，可以使用文本编辑器应用或在线工具（如[在线文本编辑器](https://passwordsgenerator.net/text-editor/)）
2. 文件内容如下（将`<zoffline ip>`替换为运行 zoffline 的电脑 IP 地址）：

   ```
   <zoffline ip> us-or-rly101.zwift.com
   <zoffline ip> secure.zwift.com
   <zoffline ip> cdn.zwift.com
   ```

   **⚠️ 注意**：与 Companion 配置不同，安卓设备直接使用需要包含`cdn.zwift.com`的映射

3. 将`hosts.txt`文件保存到手机，放在便于访问的位置

#### 关闭 Private DNS

1. 进入安卓设备的**设置** > **网络和互联网** > **高级** > **Private DNS**
2. 选择**关闭**或**自动**

#### 配置 Virtual Hosts

1. 打开 Virtual Hosts 应用
2. 选择之前创建的`hosts.txt`文件
3. 启用域名重定向功能（确保按钮处于开启状态）

#### 替代方案：使用 DNS 配置

如果你不想使用 Virtual Hosts 应用，也可以使用以下方法：

1. 在运行 zoffline 的 PC 上，在`storage`目录下创建`fake-dns.txt`文件
2. 在手机的 Wi-Fi 设置中，将**DNS 1**设置为运行 zoffline 的 PC 的 IP 地址
3. **注意**：如果你的路由器支持，也可以在路由器层面配置 DNS 记录，这样所有设备都可以自动使用

### 安装并打补丁 Zwift

#### 安装 Zwift

1. 从 Google Play 商店安装或更新 Zwift
2. **⚠️ 重要**：安装或更新后，**不要立即启动** Zwift
3. 如果已经启动过 Zwift，需要先清除数据：
   - 进入**设置** > **应用** > **Zwift** > **存储** > **清除数据**
   - 或者卸载后重新安装

#### 运行 ZofflineObb 打补丁

1. 打开`ZofflineObb`应用
2. 运行补丁程序（允许访问存储权限）
3. 等待补丁过程完成（通常需要 5-10 分钟）
4. 补丁完成后，应用会提示完成

**原理说明**：ZofflineObb 会修改 Zwift 应用，使其接受 zoffline 服务器的自签名证书，这是连接离线服务器的关键步骤。

### 运行 Zwift

1. **确保 Virtual Hosts 按钮处于开启状态**
2. 启动 Zwift 应用
3. 使用任意邮箱和密码登录，或创建新用户（如果启用了多人游戏功能）
4. Zwift 应该能够正常验证下载并运行

### 重要提示

- **每次更新后需要重新打补丁**：无论是从 Google Play 更新 Zwift，还是重新安装，都需要重新运行 ZofflineObb 打补丁
- **保持网络连接**：确保安卓设备与运行 zoffline 的 PC 在同一局域网内
- **防火墙设置**：确保 PC 的防火墙允许 zoffline 的端口访问

## 常见问题

### 卡在蓝色登录界面

**症状：** 登录时卡在蓝色界面，无法进入游戏

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/20/03f08f3fa8d593d33b38647a46f22341.png)

**解决方法：**

1. 在任务管理器中关闭 Zwift 进程
2. 将输入法切换为**微软英文输入法**
3. 重新启动 Zwift 并登录

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/20/48a6263e5ffe475ec5753b13cffd2ec1.png)

### 配置后无法更新 Zwift

**原因：** `configure_client.bat`会修改 Hosts 文件，导致无法连接到 Zwift 服务器

**解决方法：**

1. 关闭正在运行的`zoffline`
2. 进入`zwiftoffline/zoffline-helper`目录
3. 右键点击`disable_zoffline.bat`，选择**以管理员身份运行**，清除网络配置
4. 打开 Zwift 进行更新
5. 更新完成后，重新运行`configure_client.bat`恢复配置

### 无法自动上传活动到 Strava

**可能原因及解决方法：**

1. 检查`strava_token.txt`文件是否已正确放置在`storage/1`目录下
2. 确认 Strava API 的`Client ID`和`Client Secret`配置正确
3. 检查网络连接，确保 zoffline 可以访问 Strava API
4. 查看 zoffline 命令行窗口的错误日志，根据具体错误信息进行排查
5. 检查在申请 API 时填写的授权回调域是否正确

### 安卓客户端无法登录

**可能原因及解决方法：**

**对于 Companion 应用：**

1. 检查 Virtual Hosts 是否已正确启用
2. 确认 hosts 文件中的 IP 地址是否正确（应为运行 zoffline 的电脑 IP，而非 127.0.0.1）
3. 确保手机和电脑在同一局域网内
4. 检查防火墙设置，确保 zoffline 的端口未被阻止
5. 重新安装修改后的 APK 文件

**对于直接使用 Zwift 应用：**

1. 确认已关闭 Private DNS 设置
2. 检查 Virtual Hosts 是否已正确启用，按钮必须处于开启状态
3. 确认 hosts.txt 文件包含所有三个域名映射（包括`cdn.zwift.com`）
4. 检查是否在安装/更新 Zwift 后运行了 ZofflineObb 打补丁
5. 如果已启动过 Zwift，尝试清除应用数据后重新打补丁
6. 确认手机和运行 zoffline 的 PC 在同一局域网内
7. 检查 PC 防火墙设置，确保 zoffline 端口未被阻止

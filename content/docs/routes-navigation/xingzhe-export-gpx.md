---
title: "xingzhe-export-gpx"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2024-09-19T16:04:48+02:00
lastmod: 2024-09-19T16:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

[xingzhe-export-gpx](https://github.com/weaming/xingzhe-export-gpx) 可以将行者运动App的数据导出为GPX文件，方便在其他平台上查看和分析。

## 下载编译

下载源码：

```bash
git clone https://github.com/weaming/xingzhe-export-gpx.git
cd xingzhe-export-gpx
```


```bash
yarn; npm install typescript
yarn build
```

## 获取cookie

- 登录行者
- 点击右上角用户名进入个人主页
- F12打开浏览器开发者工具
- 点击开发者工具“网络”选项卡
- 刷新页面
- 点击任意的网络请求，如get_user_info
- 点击请求的“标头”
- 往下翻，翻到Cookie，复制Cookie的所有内容，右击即可复制

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/19/982ddfce88d818b7d3fb0cc221d6732b.png)

## 获取UserID

- 还是刚刚的页面，切换到“标头”旁边的预览
- 鼠标点击预览中的内容，Ctrl+F打开搜索框
- 搜索userid，即可找到自己的userid
- 眼尖的话，其实第二个请求里也有userid信息，都可以。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/19/d949eae90bb64f9a938f41d9559da86a.png)

## 配置config

将上面获取到的cookie和userid填入`config.js`中。

```ts
const xingzhe_prefix = 'https://www.imxingzhe.com'
const user_month_info = '/api/v4/user_month_info/'
// 选择下载年份
const year = '2023'
// 填写个人user_id
const user_id = '6413500'
// 填写个人xingzhe cookie, https://imxingzhe.com
const xingzhe_cookie = ''
module.exports = {
  xingzhe_prefix,
  user_month_info,
  year,
  user_id,
  xingzhe_cookie,
}
```

## 注意事项

- 每次只能下载一年的数据，每次下载都会覆盖上一次下载结果，所以请下载下一年的数据时，先把数据复制出来。
- 导入Strava就不用多介绍了，Strava主页右上角的+号，上传文件即可。
- Strava上传GPX文件好像一天只能上传30个左右，如果数据很多的话就比较蛋疼了。会提示超过上传限制，请稍后再试。

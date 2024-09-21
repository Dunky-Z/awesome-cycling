---
title: "GearAutomator"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2024-09-18T16:04:48+02:00
lastmod: 2024-09-18T21:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---


GearAutomator 是[XiaoSiHwang](https://github.com/XiaoSiHwang)开发的一款可以生成 Strava 运动热图以及天气卡片的工具。

## 同步 Strava 数据

GearAutomator 是一个可以生成 Strava 运动热图和天气卡片的工具，访问 [GearAutomator](https://www.gearaut.com)，点击的`Connect with Strava`按钮，然后输入 Strava 的用户名和密码登录。

根据运动数据量不同，生成时间会有所不同，请勿关闭页面，等待生成完成。Strava 的 API 限制很严格，同步数据很慢，连接上 Strava 之后，建议干其他事情，等待数据同步完成，不用频繁刷新页面。我第一次同步数据不知道花了多久一直没有显示热图，以为这个工具失效了，后来某一天再次访问，发现热图已经生成了。

## 查看热图

Zwift 虚拟骑行也会使用真实的 GPX 数据，所以在热力地图中也能看到有轨迹，虚拟骑行会用紫色轨迹表示，真实骑行会用绿色轨迹表示。图中紫色轨迹就是巴黎香街冲刺。绿色轨迹是一次路骑。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/08/24/fed51344e1e22419ca0ef77be2175cd5.png)

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/08/24/a4ec56ea0604b336d80ff0fe8369dd2c.png)

## 配置天气卡片

Strava 订阅用户可以生成每次运动的天气卡片，可以在运动简介中看到这次运动时的天气情况，如图所示：

没有订阅的用户也可以通过这个工具来生成，在天气配置页面，开启即可：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/08/24/b9732209d84fd4164a684bb7a66eaab6.png)

当下次有新的数据同步到 Strava 时，会自动在标题下面生成天气信息，如图所示：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/08/24/1d2987ccad88c1736c7251b0bb35d299.png)

如果你想自定义天气卡片的样式，可以在天气卡片配置页面进行设置，比如将英文转换为中文：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/08/24/42dc1ed8021b3f224c2e7c61513ca19b.png)

你可以直接复制下面的文本，替换即可：

```yaml
温度: ${temperature}
体感温度: ${apparentTemperature}
天气状况: ${skyCon}
湿度: ${humidity}
气压: ${pressure}
云量: ${cloudRate}
风速: ${windSpeed}
能见度: ${visibility}
空气质量:
    空气质量指数(AQI): ${aqi}
    细颗粒物(PM2.5): ${pm25}
    可吸入颗粒物(PM10): ${pm10}
    臭氧(O3): ${o3}
    二氧化硫(SO2): ${so2}
    二氧化氮(NO2): ${no2}
    一氧化碳(CO): ${co}
紫外线强度(UV): ${uv}
地面接收的太阳辐射(DSWRF): ${dswrf}
```

```yaml
温度: ${startTemperature} - ${endTemperature}
体感温度: ${startApparentTemperature} - ${endApparentTemperature}
天气状况: ${startSkyCon} - ${endSkyCon}
湿度: ${startHumidity} - ${endHumidity}
气压: ${startPressure} - ${endPressure}
云量: ${startCloudRate} - ${endCloudRate}
风速: ${startWindSpeed} - ${endWindSpeed}
能见度: ${startVisibility} - ${endVisibility}

空气质量:
    空气质量指数(AQI): ${startAqi} - ${endAqi}
    细颗粒物(PM2.5): ${startPM25} - ${endPM25}
    可吸入颗粒物(PM10): ${startPM10} - ${endPM10}
    臭氧(O3): ${startO3} - ${endO3}
    二氧化硫(SO2): ${startSO2} - ${endSO2}
    二氧化氮(NO2): ${startNO2} - ${endNO2}
    一氧化碳(CO): ${startCO} - ${endCO}
紫外线强度(UV): ${startUV} - ${endUV}
地面接收的太阳辐射(DSWRF): ${startDswrf} - ${endDswrf}
```

## Strava IFTTT 自动化工具

该功能可以根据设定的一些场景条件自动触发一些Strava的操作。点击左侧菜单栏Strava IFTTT，点击新建，可以看到如下页面，在此可以创建自己的自动化规则。接下来我会举例介绍该功能的使用。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/21/2ce1c390f26689fdcb17f95672cbc6df.png)

### 骑行运动时，自动在标题前添加骑行表情

> 表情包可以从[getemoji网站](https://getemoji.com/)查找复制粘贴进去。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/21/3b79406262b6742b84eeaf4e9a723a1b.png)

1. 填写自动化名称：标题添加骑行图标
2. 设置字段条件：运动类型-包含-骑行，虚拟骑行，山地骑行，公路骑行
3. 点击新增Action
4. 选择：在原始标题前
5. 文本框中输入复制来的自行车表情包
6. 关闭文本框
7. 滑动页面底部，点击保存
8. 显示下图表示创建成功

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/21/d7557b1af2dd3482725fc7d2562e0a7a.png)

当我们有新的骑行运动数据产生时，会自动在标题前添加骑行表情。

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/21/fb23e8074556416d7a6296043d434ddd.png)

### 配速达到4分/km时，将Strava的装备设置为指定跑鞋

1. 填写自动化名称：配速小于4分换跑鞋
2. 设置字段条件：平均配速 - 小于 - 4
3. 点击新增Action
4. 选择：装备 - 选择想要切换的装备
5. 滑动页面底部，点击保存

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2024/09/21/98a107b5a3b760987a94dfb02b4a81d8.png)

当下次新增的跑步数据配速小于4分时，会自动将装备设置为指定的跑鞋。

---
title: "Strava Statistics"
description: ""
summary: ""
date: 2025-02-20T16:04:48+02:00
lastmod: 2025-02-20T21:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

# Strava Statistics 部署文档

[Strava Statistics](https://github.com/robiningelbrecht/strava-statistics) 是一个自托管工具，利用 Strava 数据生成个人运动统计，支持 Docker 部署，提供丰富的可视化分析。下面介绍如何使用 Docker Compose 部署。

## 申请 Strava 的 API 权限

在[ZwiftOffline](https://lifeislife.cn/awesome-cycling/docs/training-fitness/zwiftoffline/)中也需要用到 API 权限，因为不同应用程序也不冲突，懒得再重新申请，所以以下填的信息使用的 ZwiftOffline 的 API 权限。

登录[Strava](https://www.strava.com/settings/api)，申请 API，获取`Client ID`和`Client Secret`。

填写内容可以参考下图：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/d8024be9518e5a262538aa5d48c7fbb0.png)

其中授权回调域填写：launcher.zwift.com

申请完成后会得到下面的信息：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/09/a5024f9e2e150810251222315be11ac9.png)

将下面链接中的`client_id`值换成上图中的客户 ID，然后浏览器中访问这个链接：

```txt
http://www.strava.com/oauth/authorize?client_id=xxxxxxx&response_type=code&redirect_uri=http://localhost/exchange_token&approval_prompt=force&scope=activity:read_all
```

点击授权：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/03/08/89a9c1d81d40e6b4687531ab92d689a2.png)

此时跳转到一个无法访问的网页，将地址栏中的`code`值记录下来，后面需要用到：

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/03/08/c3a74e83d363bb0f453ad37712dd28ac.png)

需要用这个`code`发起一个 cURL 请求得到`refresh_token`，具体做法是在命令行终端中执行下面的命令：

```bash
	curl -X POST https://www.strava.com/oauth/token \
	-F client_id=YOURCLIENTID \
	-F client_secret=YOURCLIENTSECRET \
	-F code=AUTHORIZATIONCODE \
	-F grant_type=authorization_code
```

- `client_id`值替换为申请得到的`客户ID`
- `client_secret`值替换为申请得到的`客户端密钥`
- `code`替换为上一步浏览器中得到的`code`

执行成功后可以得到下面的返回信息，需要将返回值中的`refresh_token`和`access_token`记录下来，后面需要用到：

```bash
{"token_type":"Bearer","expires_at":1740213400,"expires_in":21600,"refresh_token":"123456789123456789","access_token":"123456789123456789","athlete":{"id":117756825,"username":"dunky_zhang","resource_state":2,"firstname":"Dominic","lastname":"Zhang","bio":"骑行小白","city":"","state":"","country":null,"sex":"M","premium":true,"summit":true,"created_at":"2023-05-10T13:54:32Z","updated_at":"2025-02-06T05:29:52Z","badge_type_id":1,"weight":66.0,"profile_medium":"https://dgalywyr863hv.cloudfront.net/pictures/athletes/117756825/32138099/2/medium.jpg","profile":"https://dgalywyr863hv.cloudfront.net/pictures/athletes/117756825/32138099/2/large.jpg","friend":null,"follower":null}}#
```

## Docker Compose 部署 Strava Statistics

创建目录用于存放 Strava Statistics 的配置文件

```bash
mkdir statistics-for-strava
cd statistics-for-strava
```

创建 `docker-compose.yml` 文件

```bash
touch docker-compose.yml
```

编辑 `docker-compose.yml` 文件，填入以下内容：

```yaml
services:
  app:
    image: robiningelbrecht/strava-statistics:latest
    volumes:
      - ./build:/var/www/build
      - ./storage/database:/var/www/storage/database
      - ./storage/files:/var/www/storage/files
    env_file: ./.env
    ports:
      - 8080:8080
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
      # 因为Strava的API需要代理访问，所以下面设置了我的代理地址，请你根据自己的代理地址进行设置
      - http_proxy=http://192.168.1.9:7890
      - https_proxy=http://192.168.1.9:7890
      - all_proxy=socks5://192.168.1.9:7891
```

创建 `.env` 文件

```bash
touch .env
```

编辑 `.env` 文件，填入以下内容：

```bash
# 应用程序将托管的URL。此URL将用于清单文件中。
# 这将允许您将Web应用程序作为原生应用程序安装到您的设备上。
MANIFEST_APP_URL=http://localhost:8080/
# 您的Strava应用程序的客户端ID。
STRAVA_CLIENT_ID=xxxxxxx
# 您的Strava应用程序的客户端密钥。
STRAVA_CLIENT_SECRET=xxxxxxxxxxxxxx
# 您的Strava应用程序的刷新令牌。在上一步获取到的
STRAVA_REFRESH_TOKEN=xxxxxxxxxxxxxx
# Strava API有限速限制（https://github.com/robiningelbrecht/strava-statistics/wiki），
# 为了确保我们不会达到限速，我们希望限制每次导入处理的新活动数量。
# 考虑到每天有1000次请求限制，并且导入一个新活动最多可能需要3次API调用，250应该是一个安全的数字。
NUMBER_OF_NEW_ACTIVITIES_TO_PROCESS_PER_IMPORT=250
# 定期运行导入和HTML构建的计划。留空以禁用定期导入。
# 默认计划为每天凌晨04:05运行一次。如果您不知道什么是cron表达式，请勿更改此项。
# 请确保不要过于频繁地运行导入，以避免达到Strava API的限速。每天一次应该足够。
IMPORT_AND_BUILD_SCHEDULE="5 4 * * *"
# 设置用于计划的时区
# 有效的时区可以在此处找到（TZ标识符列）：https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
TZ=Asia/Shanghai

# 允许的选项：en_US、fr_FR 或 nl_BE
LOCALE=en_US
# 允许的选项：metric（公制）或 imperial（英制）
UNIT_SYSTEM=metric
# 渲染应用程序时使用的时间格式
# 允许的格式：24 或 12（包括AM和PM）
TIME_FORMAT=24
# 渲染应用程序时使用的日期格式
# 允许的格式：DAY-MONTH-YEAR（日-月-年）或 MONTH-DAY-YEAR（月-日-年）
DATE_FORMAT=DAY-MONTH-YEAR
# 要导入的运动类型。留空以导入所有运动类型。
# 通过此列表，您还可以决定运动类型的渲染顺序。
# 完整的允许选项列表可在以下地址找到：https://github.com/robiningelbrecht/strava-statistics/wiki/Supported-sport-types/
SPORT_TYPES_TO_IMPORT='[]'
# 您的生日。需要用于计算心率区间。
ATHLETE_BIRTHDAY=1999-01-01
# 体重历史（单位为千克或磅，取决于UNIT_SYSTEM）。需要用于计算相对功率重量比（w/kg）。
# 查看更多信息：https://github.com/robiningelbrecht/strava-statistics/wiki
ATHLETE_WEIGHTS='{
    "1970-01-01": 68
}'

# FTP（功能阈值功率）历史。需要用于计算活动压力水平。
# 查看更多信息：https://github.com/robiningelbrecht/strava-statistics/wiki
FTP_VALUES='{
    "2024-12-12": 235
}'
# 包含ntfy主题的完整URL。此主题将用于在新的HTML构建运行时通知您。
# 留空以禁用通知。
NTFY_URL=''
# 在导入期间要跳过的活动ID数组。
# 这允许您在导入时跳过特定活动。
ACTIVITIES_TO_SKIP_DURING_IMPORT='[]'

# 创建/拥有由strava-statistics管理的文件的UID和GID
# 可能仅在Linux主机上需要，详见Wiki中的文件权限部分
#PUID=
#PGID=
```

开始导入数据：

- 启动容器

  ```bash
  docker-compose up -d
  ```

- 导入数据

  ```bash
  docker compose exec app bin/console app:strava:import-data
  docker compose exec app bin/console app:strava:build-files
  ```
  导入过程非常非常慢，因为需要挨个数据获取，并且很容易出错，如果出错了，需要先关闭容器，然后重新导入。以下是导入成功的截图：
  ![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/23/af3c468483a1c46544c02b5c2d8124ac.png)


- 访问 `localhost:8080` 查看数据

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/03/08/07a1a21d1c53ab4560de20f5cbcb60db.png)


## 常见问题

### 401 Unauthorized

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/22/a541f82e213a98de7f9e69a614e0e7bc.png)

`.env`中的`STRAVA_REFRESH_TOKEN`可能过期，需要重新获取。又或者压根就忘记了获取`refresh_token`，需要重新获取。


### Failed to connect to nominatim.openstreetmap.org

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/22/86b6394d0eca978d164927d9129641ea.png)

因为需要生成一些地图热点信息，所以需要访问nominatim.openstreetmap.org，所以需要配置代理。

### Tring to calculate the relative power for activity

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/23/e39d6ef29c3288646bfd500908e58e0c.png)

因为需要计算相对功率重量比（w/kg），所以需要配置体重历史。如果发现某个活动的时间点没有配置体重信息就会报这个错。看看`.env`中的`ATHLETE_WEIGHTS`是否配置正确。我建议直接修改成我提供的数据，也就是从1970年开始都是当前的体重。因为我尝试配置了自己的体重历史，但是一直报错，所以直接改成了这个。

### Looks like you still need to import your strava data

![](https://picbed-1311007548.cos.ap-shanghai.myqcloud.com/markdown_picbed/img//2025/02/23/e31949d1bf03a1df838b21a74908bfbc.png)

如果你只执行了`docker-compose up -d`，而没有执行导入数据的命令，那么就会出现这个错误。需要执行导入数据的命令。如果你已经导入成功了，如果还报这个错，就需要重启一下容器。


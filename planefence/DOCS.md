# Planefence

Planefence 用于追踪靠近你的 ADS-B 接收器的飞机。
它可以记录低空或近距离飞机、生成噪声统计，并通过 Discord、Mastodon、Telegram、BlueSky、MQTT、RSS 等方式发送提醒或发布信息。

此加载项基于上游项目 docker-planefence 封装而成，适合已经有 ADS-B 数据源的 Home Assistant 用户使用。

## 功能概览

- 追踪站点周边飞机并生成记录
- 支持按距离、高度等条件过滤
- 提供 Planefence Web UI
- 支持 Plane-Alert 子功能，用于重点目标或特定条件告警
- 支持截图、飞机照片、热力图、OpenAIP 图层等展示能力
- 支持 Discord、Mastodon、Telegram、BlueSky、MQTT、RSS 等通知或发布方式

## 使用前提

在加载项开始工作前，需要先满足以下两个条件：

### 1. ADS-B 数据源

Planefence 需要从一个支持 BaseStation/SBS 格式、并通过 TCP 30003 端口输出数据的数据源读取飞机信息。

可选方式包括：

- 使用本仓库中的 ADS-B Multi-Portal Feeder 加载项。默认主机名已经指向它，通常无需额外配置。
- 使用其他支持 SBS 输出的数据源，例如 tar1090、readsb、dump1090 等。这种情况下需要把 PF_SOCK30003HOST 设置为对应设备或服务的 IP 地址或主机名。

### 2. 站点位置

Planefence 需要知道你的站点坐标，才能判断哪些飞机属于“附近”。

- 默认情况下，会自动读取 Home Assistant 的位置设置。
- 如果 Home Assistant 未设置位置，则需要手动填写 PF_LAT 和 PF_LON。

## 快速开始

建议先只完成最基本配置，确认有数据后再逐步启用其他高级功能。

### 基础配置项

以下是最重要、最常用的几个配置项：

- PF_SOCK30003HOST：ADS-B 数据源主机名或 IP
- PF_SOCK30003PORT：ADS-B 数据源端口，默认 30003
- PF_LAT：站点纬度
- PF_LON：站点经度
- PF_MAXDIST：判定为“附近”的最大距离
- PF_MAXALT：纳入围栏追踪的最大高度
- TZ：时区

### 默认行为

- PF_LAT 默认读取 Home Assistant 纬度
- PF_LON 默认读取 Home Assistant 经度
- PF_SOCK30003HOST 默认使用本仓库 ADS-B Multi-Portal Feeder 的加载项主机名
- TZ 默认读取 Home Assistant 时区

### 基础参数表

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| PF_SOCK30003HOST | f1c878cb-adsb-multi-portal-feeder | ADS-B 数据源主机名或 IP |
| PF_SOCK30003PORT | 30003 | ADS-B 数据源 TCP 端口 |
| PF_LAT | HOMEASSISTANT_LATITUDE | 站点纬度，默认读取 Home Assistant |
| PF_LON | HOMEASSISTANT_LONGITUDE | 站点经度，默认读取 Home Assistant |
| PF_MAXDIST | 2.0 | 最大追踪距离，默认按海里解释 |
| PF_MAXALT | 5000 | 最大追踪高度，默认按英尺解释 |
| TZ | HOMEASSISTANT_TIMEZONE | 时区，默认读取 Home Assistant |

### 最小可用配置示例

如果你使用的是本仓库里的 ADS-B Multi-Portal Feeder，通常只要保留默认值即可启动。

如果你使用外部 SBS 数据源，可以参考下面的最小配置：

```yaml
PF_LAT: "31.2304"
PF_LON: "121.4737"
PF_SOCK30003HOST: "192.168.1.50"
PF_SOCK30003PORT: 30003
PF_MAXDIST: "2.0"
PF_MAXALT: 5000
TZ: "Asia/Shanghai"
```

如果 Home Assistant 已正确设置位置和时区，那么通常只需要改 PF_SOCK30003HOST。

## 配置说明

### 必填与核心参数

- PF_LAT / PF_LON：站点经纬度，支持直接填写十进制度，也可使用 Home Assistant 自动值
- PF_SOCK30003HOST / PF_SOCK30003PORT：SBS/BaseStation 数据源地址与端口
- PF_MAXDIST：围栏半径，决定多远范围内的飞机会被视为“附近”
- PF_MAXALT：最大追踪高度
- TZ：容器时区，用于日志与通知时间显示

### 常规参数

常规参数主要用于控制显示方式、轮询间隔和记录行为，例如：

- PF_DISTUNIT：距离单位
- PF_ALTUNIT：高度单位
- PF_SPEEDUNIT：速度单位
- PF_INTERVAL：轮询间隔，建议不要低于 60 秒
- PF_NAME：站点名称
- PF_MAPURL：站点地图链接
- PF_MAPZOOM：热力图默认缩放级别
- PF_ELEVATION：站点海拔
- PF_FUDGELOC：坐标取整，用于隐私保护
- PF_CHECKROUTE：补充航线信息
- PF_SHOWIMAGES：显示飞机照片
- PF_DELETEAFTER：日志保留天数
- PF_IGNOREDUPES：忽略重复航班

### 常规参数速查表

| 参数 | 作用 |
| --- | --- |
| PF_DISTUNIT | 距离单位 |
| PF_ALTUNIT | 高度单位 |
| PF_SPEEDUNIT | 速度单位 |
| PF_INTERVAL | 轮询间隔 |
| PF_NAME | 站点名称 |
| PF_MAPURL | 站点地图链接 |
| PF_MAPZOOM | 热力图缩放级别 |
| PF_ELEVATION | 站点海拔 |
| PF_FUDGELOC | 坐标脱敏 |
| PF_CHECKROUTE | 获取航线信息 |
| PF_TRACKSERVICE | 飞机跟踪链接服务 |
| PF_SHOWIMAGES | 显示飞机照片 |
| PF_DELETEAFTER | 日志保留天数 |
| PF_IGNOREDUPES | 忽略重复航班 |
| PF_COLLAPSEWITHIN | 重复记录合并窗口 |

### 网页与可视化

Planefence 提供内置 Web UI，并支持多种页面增强功能：

- PF_TABLESIZE：表格每页显示条数
- PF_OPENAIP_LAYER：是否显示 OpenAIP 图层
- PF_OPENAIPKEY：OpenAIP API 密钥
- PF_SCREENSHOTURL：截图服务地址
- PF_SCREENSHOT_TIMEOUT：截图超时时间

### 网页参数表

| 参数 | 作用 |
| --- | --- |
| PF_TABLESIZE | Web 表格每页显示条数 |
| PF_OPENAIP_LAYER | 是否显示 OpenAIP 空域图层 |
| PF_OPENAIPKEY | OpenAIP API 密钥 |
| PF_SCREENSHOTURL | 截图服务 URL |
| PF_SCREENSHOT_TIMEOUT | 截图超时 |

### Plane-Alert

Plane-Alert 是 Planefence 的重点告警子功能，适合对特定目标、特定 squawk 代码或自定义名单进行提醒。

常用相关参数包括：

- PF_PLANEALERT：启用 Plane-Alert
- PF_PARANGE：Plane-Alert 半径
- PF_PA_SQUAWKS：告警 squawk 代码
- PF_ALERTLIST：告警名单来源
- PF_ALERTHEADER：CSV 告警名单表头规则
- PA_EXCLUSIONS：排除规则
- PA_TABLESIZE：Plane-Alert 页面每页条数

### Plane-Alert 参数表

| 参数 | 作用 |
| --- | --- |
| PF_PLANEALERT | 启用 Plane-Alert |
| PF_PARANGE | 告警半径 |
| PF_PA_SQUAWKS | 按 squawk 代码告警 |
| PF_ALERTLIST | 外部或本地告警名单 |
| PF_ALERTHEADER | 告警名单表头规则 |
| PA_HISTTIME | 告警历史保留天数 |
| PA_SILHOUETTES_LINK | 飞机剪影图标来源 |
| PA_TRACKSERVICE | Plane-Alert 跟踪链接服务 |
| PA_EXCLUSIONS | 告警排除规则 |
| PA_TABLESIZE | 告警页每页行数 |
| PA_MOTD | Plane-Alert 顶部消息 |

### 通知与发布

此加载项支持多种通知与发布方式，可按需启用：

- Discord
- Mastodon
- Telegram
- BlueSky
- MQTT
- RSS

如果只想先确认追踪是否正常，建议先不要启用这些通知渠道，待 Web UI 正常显示飞机数据后再逐项配置。

### 通知参数分组

- 通用通知参数：NOTIF_DATEFORMAT、PF_NOTIFEVERY、PF_ATTRIB、PA_ATTRIB、DISCORD_FEEDER_NAME、DISCORD_MEDIA
- Discord：PF_DISCORD、PF_DISCORD_WEBHOOKS、PF_DISCORD_COLOR、PA_DISCORD、PA_DISCORD_WEBHOOKS、PA_DISCORD_COLOR
- Mastodon：PF_MASTODON、PA_MASTODON、MASTODON_SERVER、MASTODON_ACCESS_TOKEN 等
- Telegram：TELEGRAM_BOT_TOKEN、PF_TELEGRAM_CHAT_ID、PA_TELEGRAM_CHAT_ID 等
- BlueSky：BLUESKY_HANDLE、BLUESKY_APP_PASSWORD、PF_BLUESKY_ENABLED、PA_BLUESKY_ENABLED
- MQTT：PF_MQTT_* 与 PA_MQTT_* 两组参数
- RSS：PF_RSS_* 与 PA_RSS_* 两组参数

## 高级配置

首次启动后，加载项会将完整的上游配置模板复制到以下路径：

- addon_configs/planefence/planefence.config

这个文件包含上游支持的全部参数和注释说明。对于 UI 中没有覆盖的高级功能，例如：

- 更复杂的告警规则
- 页面定制
- 地图展示细节
- 额外的过滤逻辑
- 通知格式微调

都建议直接编辑这个文件。

需要注意：加载项本身只会覆盖 UI 中暴露的那部分配置项，其他你手动写入 planefence.config 的内容通常会在重启后保留。

## 安装与配置流程

### 场景一：使用本仓库的 ADS-B Multi-Portal Feeder

1. 先安装并确认 ADS-B Multi-Portal Feeder 已正常工作。
2. 安装 Planefence。
3. 保持 PF_SOCK30003HOST 默认值不变。
4. 检查 Home Assistant 的位置与时区是否正确。
5. 启动 Planefence。
6. 等待几分钟后打开 Web UI 检查是否已有数据。

### 场景二：使用局域网中的外部接收器或 SBS 服务

1. 确认外部设备确实对外提供了 30003 端口的 SBS/BaseStation 数据。
2. 在 Planefence 中将 PF_SOCK30003HOST 改成该设备的 IP 或可解析主机名。
3. 如端口不是 30003，则同步修改 PF_SOCK30003PORT。
4. 启动后检查页面是否已有飞机记录。

### 场景三：Home Assistant 未配置位置

如果 Home Assistant 的系统位置没有设置，Planefence 无法自动获得站点坐标，这时需要手动填写：

- PF_LAT
- PF_LON
- TZ

建议优先保证这三项正确，再观察追踪结果是否符合预期。

## Web UI

当 ADS-B 数据源工作正常后，你可以通过以下方式访问 Planefence 页面：

- 加载项页面中的 Open Web UI 按钮
- Home Assistant 侧边栏面板

首次启动后，可能需要等待几分钟才会看到飞机记录出现。

## 常见问题与排错

### 页面打开了，但一直没有飞机数据

优先检查以下几项：

1. PF_SOCK30003HOST 是否填写正确
2. PF_SOCK30003PORT 是否与实际数据源一致
3. 数据源是否真的输出 SBS/BaseStation 格式数据
4. Home Assistant 与数据源之间网络是否互通

如果你使用的是外部接收器，最常见问题是地址填错，或接收器并未开放 30003 端口。

### 有数据，但“附近飞机”结果明显不对

通常是站点位置或单位设置有误。重点检查：

- PF_LAT
- PF_LON
- PF_DISTUNIT
- PF_MAXDIST
- PF_ALTUNIT
- PF_MAXALT

### 启动后没有通知

先确认 Web UI 中已经确实出现符合条件的飞机记录，然后再检查对应通知通道是否完整配置。

建议按以下顺序排查：

1. 先确认主功能正常记录飞机
2. 再确认 Plane-Alert 或通知条件是否真的被触发
3. 最后检查 Discord、Telegram、Mastodon、BlueSky、MQTT 等凭据或目标地址

### 修改高级配置后不生效

请确认你修改的是：

- addon_configs/planefence/planefence.config

同时注意：UI 中暴露的那部分参数可能会在启动时覆盖对应值，因此更适合把复杂定制放在 UI 未覆盖的参数中。

### 首次启动后找不到高级配置文件

planefence.config 通常在首次成功启动后才会复制到 addon_configs/planefence/ 目录下。
如果还没有出现，先完成一次正常启动，再重新查看该目录。

## 端口说明

- 80/tcp：Planefence Web UI

## 适合的使用流程

推荐按下面顺序配置：

1. 先确认 ADS-B 数据源可用
2. 确认站点经纬度正确
3. 保持默认参数启动加载项
4. 打开 Web UI，确认已有飞机数据进入
5. 再逐步启用 Plane-Alert、截图、通知渠道等增强功能

## 说明

这是一个社区维护的非官方加载项，与上游 docker-planefence 项目作者没有官方从属关系。

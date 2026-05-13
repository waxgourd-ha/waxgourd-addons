# 冬瓜甄选addons：✈️ Planefence


追踪在您 ADS-B 接收器附近飞行的飞机。Planefence 会记录低空及附近的飞机，生成噪声统计数据，并可通过 Discord、Mastodon、Telegram 和 BlueSky 发送警报。

此加载项封装自 kx1t / SDR-Enthusiasts 的 [docker-planefence](https://github.com/sdr-enthusiasts/docker-planefence)。

## 使用前提

在出现任何数据之前，需要先满足以下两个条件：

### 📡 1. ADS-B 数据源

Planefence 通过 TCP `30003` 端口的数据源读取 BaseStation/SBS 格式的飞机数据。可选方式如下：

- 使用本仓库中的 **[ADS-B Multi-Portal Feeder](https://github.com/MaxWinterstein/homeassistant-addons)**，通常无需额外配置，默认主机名会自动指向它。
- 使用**其他任意 SBS 数据源**（例如 [tar1090](https://github.com/sdr-enthusiasts/docker-tar1090) 实例、readsb、dump1090），此时需要将 `PF_SOCK30003HOST` 设置为对应的 IP 地址。

> **关于加载项主机名：** HA 加载项之间通过 `{repo_hash}-{slug}` 的格式互相访问（例如 `f1c878cb-adsb-multi-portal-feeder`）。从这个商店安装的用户使用相同的仓库哈希值，并且哈希与 slug 之间的下划线会被替换为连字符，以满足 DNS 命名要求。该方式仅适用于同一商店中的加载项互访；如果是外部数据源，请使用 IP 地址。

### 📍 2. 站点位置

Planefence 需要你的站点坐标，才能判断哪些飞机属于“附近”。默认会自动读取 Home Assistant 的位置设置。如果尚未配置，则需要在加载项选项中手动设置 `PF_LAT` 和 `PF_LON`。

## ⚙️ 配置

| 选项 | 默认值 | 说明 |
| ------------------ | ----------------------------------- | --------------------------------------------------------- |
| `PF_SOCK30003HOST` | `f1c878cb-adsb-multi-portal-feeder` | ADS-B 数据源的主机名或 IP（SBS/30003 端口） |
| `PF_SOCK30003PORT` | `30003` | SBS 输出端口 |
| `PF_LAT` | HA 纬度 | 站点纬度（自动从 Home Assistant 填充） |
| `PF_LON` | HA 经度 | 站点经度（自动从 Home Assistant 填充） |
| `PF_MAXDIST` | `2.0` | 与站点的最大距离（海里） |
| `PF_MAXALT` | `5000` | 最大高度（英尺） |
| `TZ` | `UTC` | 时区，例如 `Europe/Berlin` |

### 高级配置

首次启动时，加载项会将完整的上游配置模板复制到 `addon_configs/planefence/planefence.config`。这个文件包含全部可用选项及其内联注释。对于上方 UI 未覆盖的配置，例如提醒、过滤、地图定制等，请直接编辑该文件。详细说明请参阅[上游文档](https://github.com/sdr-enthusiasts/docker-planefence)。

**加载项只会覆盖上表中列出的这些选项。** 其他你手动设置的内容在重启后通常都会保留。

> **提示：** 你可以使用 [Studio Code Server 加载项](https://github.com/hassio-addons/addon-vscode)，直接在浏览器中编辑 `addon_configs/planefence/planefence.config`。

## 🌐 Web UI

当开始接收到飞机数据后，你可以通过加载项页面上的 **Open Web UI** 按钮，或通过侧边栏面板访问 Planefence 网页界面。首次启动后，可能需要等待几分钟才会出现记录。

---

> **免责声明：** 这是一个由 planefence 项目爱好者制作并维护的非官方社区加载项。它与 kx1t / SDR-Enthusiasts 没有隶属关系，也未获得其官方认可。加载项图标由 AI 生成，并非官方标志。

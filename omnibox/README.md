# 冬瓜甄选addons：OmniBox

一站式影视、直播与资源聚合媒体管理面板（OmniBox）。

## 基本信息

| 项目 | 值 |
|---|---|
| 上游项目 | [lampon/omnibox](https://hub.docker.com/r/lampon/omnibox) |
| 加载项镜像 | `r.hassbus.com/wghaos/omnibox`（基于上游官方镜像构建/转存） |
| 当前版本 | `2.1.3` |
| Web 端口 | `7023`（`http://<HA地址>:7023`） |
| 数据目录 | 容器内 `/app/data`，持久化到加载项数据目录 `/data` |
| 支持架构 | `amd64`、`aarch64` |

## 安装

1. 在「设置 → 加载项 → 加载项商店 → ⋮ → 仓库」中填入本仓库地址：

   ```
   https://gitcode.com/waxgourd/addons
   ```

2. 刷新页面，在列表中找到 **OmniBox**，点击安装（镜像较大，约 1.3 GB，请耐心等待）；
3. 安装完成后启动加载项；
4. 点击「打开 Web UI」，或直接访问 `http://<HA地址>:7023`。

> 本加载项未启用 Ingress，请通过 `7023` 端口访问。

## 配置

| 配置项 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `timezone` | str | `Asia/Shanghai` | 容器时区（IANA 名称，如 `Asia/Shanghai`、`Asia/Hong_Kong`），影响日志与媒体时间显示 |

修改配置后需要重启加载项才能生效。

## 使用

启动加载项后，通过 `http://<HA地址>:7023` 访问管理面板，首次进入按需完成初始化配置（媒体源、索引目录等）。

## 数据持久化

容器内的 `/app/data` 已链接到加载项的持久目录 `/data`：

- 首次启动时，镜像内置的默认数据会复制到 `/data`；
- 之后的配置、数据库、缓存等都保存在 `/data`，重启或升级加载项不会丢失；
- 该目录随 Home Assistant 完整备份一起保存，无需额外映射。

> 建议在升级加载项前先创建一次 Home Assistant 完整备份。

## 更新

- 应用版本与上游镜像保持一致，版本号即镜像 tag（当前 `2.1.3`）；
- 升级前建议先做一次 Home Assistant 完整备份。

## 故障排除

1. **Web 界面打不开**：确认加载项已启动且日志无报错；确认 `7023` 端口未被其他服务占用。
2. **配置修改不生效**：修改配置项后需要重启加载项。
3. **升级后数据异常**：确认 `/data` 目录未被清理；升级前建议先做一次完整备份。
4. **查看日志**：「设置 → 加载项 → OmniBox → 日志」。

## 相关链接

- 上游项目：[lampon/omnibox](https://hub.docker.com/r/lampon/omnibox)
- 版本记录：[CHANGELOG.md](CHANGELOG.md)
- 文档说明：[DOCS.md](DOCS.md)

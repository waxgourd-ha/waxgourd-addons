# Songloft

Songloft 是一个自托管本地音乐服务器，本仓库将其封装为 Home Assistant Add-on 方便直接安装和运行。

当前这个 add-on 以最小封装为主：
- 提供独立 Web UI
- 持久化运行数据到 `/data`
- 默认开放音乐目录映射，便于直接管理本地媒体文件
- 当前不启用 Home Assistant ingress，使用直连端口访问

## 安装与启动

1. 在 Home Assistant 中安装 `Songloft` add-on。
2. 启动 add-on。
3. 启动完成后，点击 add-on 页面中的 **Open Web UI**，或直接通过浏览器访问 Web 界面。

## 访问方式

- Web UI：`http://<Home Assistant 主机>:58091`
- add-on 默认暴露端口：`58091/tcp`

在本仓库当前封装中：
- `webui` 指向 `[PROTO:http]://[HOST]:[PORT:58091]/`
- 适用于 `amd64` 与 `aarch64`

## 数据与目录说明

### 持久化目录

- 应用目录：`/data/songloft`
- 数据库文件：`/data/songloft.db`

Songloft 的运行数据会保存在 add-on 的 `/data` 目录中，卸载前不会因为重启而丢失。

### 音乐目录

推荐按以下顺序使用音乐目录：
- 优先：`/media/songloft`
- 回退：`/data/music`

如果 Home Assistant 已挂载媒体目录，建议直接把音乐文件放到 `/media/songloft`；如果当前环境没有可用的 `/media`，则可改用 `/data/music`。

## 使用建议

首次启动后，建议按以下流程操作：

1. 打开 Songloft Web UI。
2. 在 Web UI 中确认或设置音乐库目录。
3. 将音乐文件放入推荐目录后，在界面中触发扫描。
4. 等待扫描完成后，再继续创建歌单、整理资料或播放。

## 当前封装说明

本仓库当前的 Songloft add-on 保持最小封装，不额外暴露复杂配置项，重点是先提供稳定可运行的 Web 音乐服务。

已知特性：
- 不启用 ingress
- 通过固定端口 `58091` 访问
- 依赖外部媒体目录或 `/data` 目录保存音乐文件与运行数据

## 源

- GitHub：<https://github.com/songloft-org/songloft>
- 官方文档：<https://songloft.hanxi.cc/>
- Docker Hub：<https://hub.docker.com/r/songloft/songloft>


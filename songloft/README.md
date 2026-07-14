# 冬瓜甄选addons：Songloft

Songloft 是一个自托管本地音乐服务器，本仓库将其封装为 Home Assistant Add-on 方便直接安装和运行。

## 功能说明

- 通过 Home Assistant Add-on 方式运行 Songloft
- 默认提供 Web 管理界面
- 将应用运行数据持久化到 Add-on 的 `/data`
- 自动准备推荐音乐目录：
  - 优先使用 `/media/songloft`
  - 如果 `/media` 不可用，则回退到 `/data/music`

## 端口

- 容器端口：`58091`
- Add-on 默认映射：`58091/tcp`
- Web UI：`http://<HomeAssistant主机>:58091`

## 目录约定

- 应用数据库：`/data/songloft.db`
- 持久化二进制：`/data/songloft`
- 推荐音乐目录：
  - 优先使用 `/media/songloft`
  - 回退使用 `/data/music`

Add-on 启动时会：

- 将 Songloft 可执行文件复制到 `/data/songloft`
- 使用 `/data/songloft.db` 作为数据库文件
- 创建推荐的音乐目录，方便你在 Songloft Web UI 中直接选择

## 安装后使用

1. 在 Home Assistant 中安装并启动本 Add-on。
2. 打开 Add-on 页面提供的 Web UI 链接。
3. 在 Songloft Web UI 中把音乐目录设置为 `/media/songloft`；如果你的环境没有 `/media`，则改为 `/data/music`。
4. 在 Songloft 中继续完成初始化配置。

## 源

- GitHub: <https://github.com/songloft-org/songloft>
- Docker Hub: <https://hub.docker.com/r/songloft/songloft>

## 已知说明

- 首版采用直连端口方式，不启用 Home Assistant ingress。
- 当前 Add-on 未暴露额外可配置项，保持最小封装，便于先验证基础运行能力。

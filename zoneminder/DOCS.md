# Zoneminder

Zoneminder 是一套功能完整的开源视频监控系统，可用于摄像头接入、录像、事件管理、运动检测和告警。

这个 Home Assistant 加载项基于 Zoneminder 容器镜像封装，提供了 Web UI 访问、存储目录映射以及额外环境变量注入能力。

## 功能概览

- 提供 Zoneminder Web 管理界面
- 支持添加和管理摄像头
- 支持录像、事件存储与回放
- 支持运动检测区域配置
- 支持通过 `env_vars` 注入更多高级参数
- 支持将图片存储目录改到自定义路径

## 使用前提

在真正开始配置前，建议先确认两件事：数据库是否可用，以及摄像头流地址是否已经准备好。

### 1. 数据库依赖

Zoneminder 依赖 MySQL / MariaDB 数据库。

当前加载项在 `services` 中声明了 `mysql:want`，这表示它期望有可用的 MySQL/MariaDB 服务。
实际使用时，建议你准备以下之一：

- Home Assistant MariaDB 加载项
- 外部 MySQL 数据库
- 外部 MariaDB 数据库

如果数据库不可用，Zoneminder 通常无法完成初始化或正常运行。

### 2. 摄像头来源

安装好加载项后，还需要在 Zoneminder Web 界面中手动添加摄像头。
这个加载项本身不会自动发现或自动创建摄像头配置。

建议你提前准备好以下信息：

- 摄像头的访问地址
- 摄像头协议类型（HTTP、RTSP 等）
- 用户名和密码
- 摄像头分辨率、编码格式或子码流信息

## 快速开始

建议按下面顺序完成首次部署：

1. 先准备好 MariaDB / MySQL 数据库。
2. 安装 Zoneminder 加载项。
3. 按需修改 `Images_location`。
4. 如果需要高级参数，通过 `env_vars` 补充。
5. 启动加载项。
6. 打开 Web UI，完成初始化。
7. 添加摄像头。
8. 配置录像策略、检测区域和告警规则。

## 配置说明

### 核心选项

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `Images_location` | str | `/config/addons_config/zoneminder/images` | 摄像头图片存储路径 |
| `env_vars` | list | `[]` | 额外环境变量列表，用于高级配置 |

这两个选项中：

- `Images_location` 是最常改的持久化参数
- `env_vars` 是高级扩展入口，适合补充 UI 没暴露的上游环境变量

### Images_location

`Images_location` 用于指定图片存储目录。

默认值：

```yaml
Images_location: /config/addons_config/zoneminder/images
```

你也可以改成其他已映射目录，例如：

```yaml
Images_location: /share/zoneminder/images
```

建议使用持久化目录，避免因容器更新或重建导致数据丢失。

如果你不确定放哪里，优先考虑以下位置：

- `/config/addons_config/zoneminder/...`
- `/share/zoneminder/...`
- `/media/zoneminder/...`

### env_vars

如果你需要设置额外的 Zoneminder 环境变量，可以使用 `env_vars`。

格式示例：

```yaml
env_vars:
  - name: TZ
    value: Asia/Shanghai
  - name: EXAMPLE_OPTION
    value: example_value
```

适合以下场景：

- 调整容器行为
- 传递上游镜像支持的高级环境变量
- 做一些 UI 没有暴露的附加配置

如果只是普通使用，通常不需要先改 `env_vars`；建议先完成基础初始化，再按需追加。

## 存储路径

根据当前加载项配置，相关路径大致如下：

- 图片目录：由 `Images_location` 控制
- 事件目录：`/var/cache/zoneminder/events2`
- 声音目录：`/var/cache/zoneminder/sounds2`
- 配置目录：`/config/addons_config/zoneminder`

当前加载项映射了以下 Home Assistant 路径：

- `config:rw`
- `media:rw`
- `share:rw`
- `ssl`

因此如果你想把图片或其他内容写到持久化位置，优先考虑 `config`、`media` 或 `share` 下的目录。

## 数据库建议

虽然当前 DOCS 不直接暴露数据库连接字段，但 Zoneminder 运行依赖数据库，因此部署时建议优先把数据库问题单独确认清楚。

推荐思路如下：

- 想少折腾：优先使用 Home Assistant MariaDB 加载项
- 已有数据库环境：使用外部 MySQL 或 MariaDB
- 摄像头数量较多：优先考虑性能更稳定的独立数据库实例

如果数据库未正确初始化，Zoneminder 的 Web UI 往往也无法正常完成后续配置。

## 访问方式

Zoneminder Web UI 可通过以下方式访问：

- Web UI 地址：`[PROTO:ssl]://[HOST]:[PORT:80]/zm`
- 默认外部端口映射：`80/tcp -> 3778`

通常你可以通过：

- Home Assistant 加载项页面中的 Open Web UI
- 或直接访问 `http://你的HA地址:3778/zm`

注意访问路径末尾通常包含 `/zm`，如果你只访问到根路径，可能会看到空白页、跳转异常或错误页面。

## 初始配置建议

首次启动后，建议按以下顺序完成配置：

1. 确认数据库可用
2. 打开 Zoneminder Web UI
3. 完成 Web UI 初始化
4. 添加第一路摄像头
5. 测试视频流是否正常
6. 配置录像与事件保存策略
7. 配置运动检测区域和告警规则

如果你是第一次使用 Zoneminder，建议先只添加一路摄像头做验证，确认预览、录像、事件都正常后，再批量添加其他摄像头。

## 常见问题

### 1. Web 页面打不开

优先检查：

- 加载项是否已成功启动
- `3778` 端口是否被占用或未映射
- Web UI 路径是否包含 `/zm`

如果通过 Ingress 可以打开，但端口访问不行，优先检查端口映射；如果两者都不行，则优先检查加载项日志。

### 2. 启动失败或初始化失败

最常见原因是数据库不可用。请检查：

- MariaDB / MySQL 是否已经运行
- 数据库连接是否已在上游环境变量或应用界面里正确设置
- 数据库权限是否足够

如果日志里出现数据库初始化、建表失败或连接超时，先把数据库问题解决，再继续配置摄像头。

### 3. 图片或事件没有持久化

请检查存储路径是否写到了持久化目录。

建议：

- 图片目录使用 `config`、`share` 或 `media` 下的路径
- 不要把重要数据只存放在容器内部临时目录中

如果你后续需要大量录像，建议同时关注磁盘容量与写入性能。

### 4. 摄像头添加后没有视频

通常需要在 Zoneminder Web UI 内进一步检查：

- 摄像头源地址是否正确
- 用户名密码是否正确
- 编码或流格式是否受支持
- 网络是否可达

这类问题大多不是加载项本身的问题，而是摄像头流地址、认证或协议兼容性问题。

### 5. 需要更多高级参数

请使用 `env_vars` 传递额外环境变量。
具体支持哪些变量，应以上游 Zoneminder 容器镜像说明为准。

## 适合的维护方式

如果你打算长期使用，建议把维护重点放在以下三件事上：

1. 数据库备份
2. 图片 / 事件目录备份
3. 升级前先验证磁盘空间和数据库状态

## 维护建议

- 升级前备份数据库和关键录像数据
- 将图片和事件尽量保存到持久化路径
- 摄像头数量较多时，注意磁盘占用与数据库性能
- 如果遇到复杂兼容性问题，优先查看加载项日志和 Zoneminder Web UI 错误信息

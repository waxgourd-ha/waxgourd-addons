# Turbo4 Documentation

## 1. 文档范围

本文档面向 Turbo4 的使用者与维护者，重点说明：

- Add-on 的运行结构
- 启动流程
- 持久化目录
- 登录认证机制
- 网络与代理相关行为
- 构建与发布流程
- 常见问题排查

如果你只是想快速了解项目和首次使用方式，请先阅读 [README.md](README.md)。

## 2. 项目定位

Turbo4 是一个 Home Assistant Add-on，提供 SingBox 的 Web 管理界面。

它由以下几部分组成：

1. **前端界面**：Vue 构建出的静态页面
2. **Go WebServer**：提供静态资源服务、认证和本地管理 API
3. **s6 服务管理**：负责初始化和守护运行流程
4. **bundled sing-box**：构建时打包到镜像中的 sing-box 二进制与默认资源

## 3. 运行结构

### 3.1 Docker 构建流程

当前镜像使用三阶段构建：

1. `node:20-alpine`：构建前端
2. `golang:1.21-alpine`：编译 `gfs-webserver`
3. `hassio-addons/base` 运行时镜像：复制前端产物、Go 二进制、rootfs，并下载默认 sing-box 资源

运行时还会安装以下依赖：

- `ca-certificates`
- `curl`
- `wget`
- `gcompat`
- `nftables`
- `iptables`

### 3.2 s6 服务结构

当前主要服务如下：

- `init-gfs`：初始化服务（oneshot）
- `gfs`：主服务（longrun）

其中：

- `init-gfs` 负责准备 `/config/data` 下的资源，并按需自动启动 sing-box
- `gfs` 负责启动 Web 管理面板
- `gfs/finish` 在 WebServer 退出时尝试清理部分 `ip rule`

## 4. 启动时会发生什么

### 4.1 数据目录初始化

Turbo4 主要使用 `/config/data` 作为持久化目录。启动时会检查并初始化：

- `/config/data/sing-box`
- `/config/data/plugins`
- `/config/data/.cache`
- `/config/data/.auth.yaml`
- `/config/data/plugins.yaml`

### 4.2 默认资源写入

`init-gfs` 会在必要时把镜像中的默认资源写入持久化目录，包括：

- `sing-box` 二进制
- `sing-box.ver`
- `plugin-node-convert.js`
- `third/node-convert/proxy-utils.esm.mjs`
- `plugins.yaml`

如果镜像内置版本与持久化目录中的版本不一致，也会自动覆盖更新。

### 4.3 启动时对现有配置的修补

如果相关文件已存在，启动脚本还会主动修改它们：

- `user.yaml`
  - 把 Plugin Hub 地址从 `raw.githubusercontent.com` 改为 `cdn.jsdelivr.net`
  - 把 `lang: en` 改为 `lang: zh`
- `profiles.yaml`
  - 把 `strict_route: true` 改成 `strict_route: false`

这意味着 Turbo4 启动时**会修改已有数据文件**，并不是纯只读运行。

### 4.4 Plugin Hub 缓存初始化

若 `/config/data/.cache/plugin-list.json` 不存在或为空，启动时会尝试从 jsDelivr 拉取：

- `generic.json`
- `gfs.json`

然后合并生成本地插件列表缓存。

## 5. `auto_start_kernel` 的行为

当 Add-on 配置中：

```yaml
auto_start_kernel: true
```

初始化脚本会在检测到 sing-box 二进制和配置文件后，自动启动 sing-box。

### 5.1 启动前配置修补

启动前会使用 `jq` 修改 sing-box 配置，包括：

- 对 `tun` 入站：
  - 强制 `strict_route = false`
  - 只保留 IPv4 地址
- 对 `mixed` 入站：
  - 强制监听到 `0.0.0.0`
- 设置：
  - `route.default_mark = 255`
  - `dns.final = "Local-DNS"`
  - `dns.fakeip.inet6_range = "fc00::/18"`
- 对包含 `GeoLocation-!CN` 的 DNS 规则，把 `server` 改为 `Fake-IP`

### 5.2 后台启动 sing-box

启动后会把相关信息写入：

- 日志：`/config/data/sing-box/sing-box.log`
- PID：`/config/data/sing-box/pid.txt`

### 5.3 路由与 DNS 修改

自动启动 sing-box 后，脚本还会尝试：

- 添加 `fwmark 255 -> main` 规则
- 为 `127.0.0.0/8` 添加回环绕行规则
- 为内网地址段添加绕行规则：
  - `10.0.0.0/8`
  - `172.16.0.0/12`
  - `192.168.0.0/16`
- 添加 `iif lo -> table 2022` 规则
- 将 `/proc/1/root/etc/resolv.conf` 和 `/etc/resolv.conf` 尝试写成：
  - `nameserver 1.1.1.1`

> 这部分行为会直接影响网络路由和 DNS，适合明确理解 TUN / 透明代理行为的用户使用。

### 5.4 停止时的清理范围

当 `gfs-webserver` 退出时，`gfs/finish` 会尝试清理部分 `ip rule`，包括：

- `fwmark 255 table main priority 100`
- `iif lo lookup 2022 priority 5000`
- 三段私网绕行规则

请注意：

- **并不是所有运行时改动都会被完整回滚**
- 文档不能将其理解为“停止后自动完全恢复网络环境”
- DNS 文件也没有对称的恢复逻辑

## 6. Web 面板与认证

### 6.1 面板监听方式

`gfs` 服务会读取 Add-on 配置中的 `panel_port`，并执行：

- `/app/gfs-webserver --port=<panel_port> --data=/config`

因此 Web 面板使用的是 **Home Assistant 主机 IP + 面板端口**。

默认端口：

- `2097`

### 6.2 健康检查

WebServer 提供：

- `/healthz`

返回 `200 OK` 和字符串 `ok`，可用于基础连通性检查。

### 6.3 默认登录信息

如果 `/config/data/.auth.yaml` 不存在，则默认使用：

- 用户名：`admin`
- 密码：`admin123`

凭据文件位置：

- `/config/data/.auth.yaml`

文件内容格式：

```yaml
username: admin
password: admin123
```

### 6.4 登录与 Token

认证流程如下：

1. 调用 `/api/auth/login`
2. 登录成功后返回 Bearer Token
3. 后续 `/api/*` 请求需要带 Token
4. Token 默认有效期为 7 天（内存中维护）

这也意味着：

- 容器重启后，旧登录态大概率失效
- 需要重新登录获取新的 Token

### 6.5 修改密码

调用 `/api/auth/change-password` 后，会把新的用户名/密码写入：

- `/config/data/.auth.yaml`

建议首次登录后立即修改默认密码。

## 7. Clash API 代理

Turbo4 提供一个反向代理入口：

- `/clash-api/{host:port}/{path}`

用途：

- 让 Web 模式下的前端访问容器内 sing-box 的 Clash API

限制：

- 只允许代理到 **loopback 地址**
- 非 loopback 地址会被直接拒绝
- 同时支持普通 HTTP 请求和 WebSocket 升级

这项限制是明确的安全边界，不应在文档中描述成“可代理任意后端”。

## 8. Add-on 配置项

当前 `config.yaml` 中实际有效的 Add-on 选项只有：

```yaml
panel_port: port
auto_start_kernel: bool
```

即用户可配置：

- `panel_port`
- `auto_start_kernel`

请不要把 `CHANGELOG.md` 里历史上提到的 `username`、`password` 当作当前 Add-on 配置项；当前 live schema 并没有暴露它们。

## 9. 主要界面模块

当前前端路由对应的主要模块包括：

- `/` → Overview
- `/profiles` → Profiles
- `/subscriptions` → Subscriptions
- `/rulesets` → Rulesets
- `/plugins` → Plugins
- `/scheduledtasks` → Scheduled Tasks
- `/settings` → Settings

这些模块覆盖的核心能力包括：

- SingBox 配置管理
- 订阅更新
- 规则集管理
- 插件管理
- 计划任务
- 日志与连接信息查看
- 部分运行控制

## 10. 构建与发布概览

### 10.1 构建过程

Dockerfile 当前执行：

1. 前端 `pnpm build`
2. Go WebServer 编译
3. 运行时镜像组装
4. 构建时下载并打包固定版本的 `sing-box`
5. 构建时下载默认插件脚本

### 10.2 发布流程

当前 GitLab CI：

- 仅在 **tag** 触发时构建
- 支持：
  - `aarch64-...`
  - `amd64-...`
  - 无前缀 tag 的多架构构建
- beta 与正式版会推送到不同目标仓库
- 非 beta 的多架构构建还会打 `latest`

## 11. 常见问题排查

### 11.1 Web 面板无法访问

检查项：

- Add-on 是否已启动
- `panel_port` 是否与访问端口一致
- 是否使用了 `http://<HA-IP>:<panel_port>` 访问
- 主机网络端口是否被占用
- `/healthz` 是否返回 `ok`

### 11.2 登录失败

检查项：

- 是否仍在使用默认账号 `admin / admin123`
- `/config/data/.auth.yaml` 是否已被修改
- 是否最近重启过容器，导致旧 Token 失效
- 是否需要重新登录获取新 Token

### 11.3 sing-box 没有自动启动

检查项：

- `auto_start_kernel` 是否为 `true`
- `/config/data/sing-box/config.json` 是否存在
- `/config/data/sing-box/sing-box.log` 是否有报错
- `jq` 修补配置是否成功

### 11.4 网络或 DNS 异常

检查项：

- 是否启用了 `auto_start_kernel`
- 是否已添加 `ip rule`
- `/etc/resolv.conf` 是否已被改写为 `1.1.1.1`
- 停止服务后是否仍残留部分路由规则

## 12. 安全与运维提示

- 默认账号密码仅适合首次引导，必须尽快修改
- 该 Add-on 使用 `host_network` 并具备 `NET_ADMIN` / `NET_RAW` 能力
- 自动启动内核与透明代理功能会影响路由和 DNS
- 面板背后不仅是静态页面，还包含本地文件和进程管理 API，应按“本地管理面板”而非“普通网页”来理解其权限范围

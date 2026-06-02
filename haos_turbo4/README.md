# 冬瓜甄选addons：Turbo4 (GUI for SingBox)

Turbo4 是一个 Home Assistant Add-on，用于提供 **SingBox Web 管理界面**。它把前端界面和本地管理后端打包到同一个插件中，便于在 HAOS 环境下管理配置、订阅、规则集、插件和计划任务。

> 当前 Add-on 名称：`Turbo4 (GUI for SingBox)`  
> 默认面板端口：`2097`  
> 默认首次登录账号：`admin` / `admin123`

## 功能概览

根据当前界面路由，Turbo4 主要提供以下模块：

- **Overview**：运行概览、连接、日志、快速控制
- **Profiles**：SingBox 配置文件管理
- **Subscriptions**：订阅管理与更新
- **Rulesets**：规则集管理
- **Plugins**：插件安装、配置与更新
- **Scheduled Tasks**：计划任务
- **Settings**：界面与运行设置

## 运行要求

当前 Add-on 配置要求如下：

- 支持架构：`aarch64`、`amd64`
- 使用 `host_network: true`
- 需要权限：`NET_ADMIN`、`NET_RAW`
- 持久化目录：`/config`（通过 add-on 配置目录映射）
- 默认不开启 HA Ingress（`ingress: false`）

这意味着该 Add-on **不仅仅是一个静态网页面板**，还具备网络管理能力，适合明确了解透明代理和路由行为的用户使用。

## 安装与使用

1. 在 Home Assistant 中添加此 Add-on 仓库并安装 `Turbo4`。
2. 启动 Add-on。
3. 通过 **Home Assistant 主机 IP + 面板端口** 访问，例如：
   - `http://<HA-IP>:2097`
4. 使用默认账号登录：
   - 用户名：`admin`
   - 密码：`admin123`
5. 首次登录后，**请立即修改密码**。

## Add-on 配置项

当前生效的 Add-on 选项只有两个：

```yaml
panel_port: 2097
auto_start_kernel: true
```

说明：

- `panel_port`：Web 管理面板监听端口
- `auto_start_kernel`：容器启动时是否自动启动 sing-box 并执行相关网络配置

## 重要提醒

### 1. 默认凭据仅用于首次引导

Web 面板在没有自定义凭据时，会使用默认账号：

- `admin`
- `admin123`

请在首次登录后立即修改，否则存在明显安全风险。

### 2. `auto_start_kernel` 会产生运行时副作用

当 `auto_start_kernel=true` 时，启动脚本会尝试：

- 自动启动 sing-box
- 修改部分 sing-box 配置内容
- 增加 `ip rule` 路由规则
- 修改 DNS 解析文件为 `1.1.1.1`

因此 Turbo4 的行为不只是“打开一个 Web 面板”，还会影响网络与代理运行方式。

### 3. 使用 host network 与特权能力

该 Add-on 使用主机网络，并声明了 `NET_ADMIN` / `NET_RAW` 能力。请仅在你了解其网络影响时启用，尤其是在 TUN/透明代理场景下。

## 目录与持久化

Turbo4 的数据主要保存在 `/config/data` 下，包括：

- sing-box 运行目录
- 插件与缓存
- 登录凭据文件
- 运行日志与 PID 文件

## 更多说明

详细的运行机制、目录结构、认证方式、网络行为、构建发布流程和排障建议，请查看：

- [DOCS.md](DOCS.md)

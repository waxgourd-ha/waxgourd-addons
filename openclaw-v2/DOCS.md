# OpenClaw 小龙虾前沿版

## 简介

OpenClaw 小龙虾前沿版是一个 Home Assistant Add-on，用于在 HA 中运行 OpenClaw 网关与管理界面，支持在 HA 面板内通过 Ingress 访问，也支持局域网访问网关端口。

## 安装与启动

1. 在 Home Assistant 的应用商店安装 OpenClaw 小龙虾前沿版。
2. 进入配置页面，按需调整参数。
3. 点击启动，等待日志出现正常启动信息。
4. 启动后可通过以下方式访问：
	 - Add-on 面板中的 Open Web UI（Ingress，默认内部端口 8099）
	 - 局域网网关地址（默认端口 18789，受绑定模式影响）

## 配置说明

以下配置项与 config.yaml 保持一致。

```yaml
# 仅通过 Ingress 访问管理 UI（8099）
ingress_only: false

# 时区
timezone: "Asia/Shanghai"

# 网关绑定模式：loopback=仅本地, lan=局域网访问
gateway_bind_mode: "lan"

# 网关端口
gateway_port: 18789

# 允许 HTTP 认证（仅在无法使用 HTTPS 时启用）
allow_insecure_auth: true

# 网关公开 URL（用于新标签页跳转）
gateway_public_url: ""

# 启用 Web 终端
enable_terminal: true

# 启用 SSH Shell（默认关闭）
enable_ssh: false
ssh_port: 22
ssh_username: "root"
ssh_password: ""

# 会话锁清理
clean_session_locks_on_start: true
clean_session_locks_on_exit: true
```

### 关键参数建议

- ingress_only：
	- true：只允许通过 HA Ingress 访问管理 UI，更安全。
	- false：允许局域网直接访问（配合 gateway_bind_mode）。
- gateway_bind_mode：
	- loopback：仅本机访问，适合只在 HA 内使用。
	- lan：局域网可访问，便于多设备接入。
- allow_insecure_auth：
	- 建议仅在内网且无法启用 HTTPS 时临时开启。
- enable_ssh：
	- 默认关闭更安全。
	- 开启后请务必设置强密码，并限制网络暴露面。

## 推荐配置

### 方案一：仅 HA 内使用（更安全）

```yaml
ingress_only: true
gateway_bind_mode: "loopback"
allow_insecure_auth: false
enable_ssh: false
```

### 方案二：局域网多设备接入

```yaml
ingress_only: false
gateway_bind_mode: "lan"
gateway_port: 18789
allow_insecure_auth: true
```

如果你有反向代理和证书，建议使用 HTTPS 对外暴露，不建议长期使用不安全的 HTTP 认证。

## 常见问题

### 1) 无法从局域网访问网关

- 检查 gateway_bind_mode 是否为 lan。
- 检查 gateway_port 是否被其他服务占用。
- 检查路由器/防火墙是否放行该端口。

### 2) 只能通过 HA 面板访问

- 这是 ingress_only=true 的预期行为。
- 如需局域网访问，请将 ingress_only 设为 false，并重启 Add-on。

### 3) 开启 SSH 后无法登录

- 确认 enable_ssh=true。
- 确认 ssh_port、ssh_username、ssh_password 配置正确。
- 若 ssh_password 为空，则密码登录会被禁用。

## 相关链接

- OpenClaw 官网：https://openclaw.ai
- OpenClaw GitHub：https://github.com/openclaw/openclaw
- OpenClaw 文档：https://docs.openclaw.ai/zh-CN


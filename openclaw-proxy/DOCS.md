# OpenClaw Proxy

## 说明

OpenClaw Proxy 是一个 Home Assistant Add-on。
它不会启动 OpenClaw 主服务，而是将已有 OpenClaw Web 服务代理到 HA Ingress 页面中，
便于在 Home Assistant 内统一访问。

## 前提条件

- 已有可用的 OpenClaw 服务实例。
- 已确认 OpenClaw 服务端口可访问（默认 `18789`）。

## 安装

1. 进入 Home Assistant 的插件商店。
2. 安装 OpenClaw Proxy。
3. 根据实际部署环境填写配置。
4. 启动插件，并在侧边栏打开 OpenClaw。

## 配置项

```yaml
target_host: ""
target_port: 18789
```

- `target_host`：目标 OpenClaw 服务地址（可选）。
- `target_port`：目标 OpenClaw 服务端口，默认 `18789`。

## 使用建议

- OpenClaw 与 Proxy 在同一网络环境时，优先使用内网地址。
- 如出现页面无法打开，先检查目标地址和端口是否可达。

## 常见问题

- 打开页面提示连接失败：
	检查 OpenClaw 服务是否正在运行，并确认 `target_host` / `target_port` 配置正确。
- 页面可打开但功能异常：
	检查 OpenClaw 主服务日志，确认服务本身状态正常。
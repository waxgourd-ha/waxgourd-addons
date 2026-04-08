# 冬瓜甄选 Add-ons: OpenClaw Proxy

## 关于

OpenClaw Proxy 用于将已运行的 OpenClaw 服务代理到 Home Assistant 页面框架中，
通过 Ingress 在 HA 内直接访问 OpenClaw Web 界面。

## 功能亮点

- 无需额外暴露端口，直接在 HA 侧边栏访问。
- 可自定义目标地址与端口，适配本机或局域网中的 OpenClaw 服务。
- 轻量代理，适合与 OpenClaw 主插件或独立部署实例配合使用。

## 快速开始

1. 在 Home Assistant 插件商店安装 OpenClaw Proxy。
2. 在插件配置中设置目标地址和端口（默认端口为 `18789`）。
3. 启动插件后，从 HA 侧边栏打开 OpenClaw 页面。

## 配置示例

```yaml
# OpenClaw 服务地址（可选）
target_host: ""

# OpenClaw 服务端口
target_port: 18789
```

## 相关链接

- Website: https://openclaw.ai
- GitHub: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai/zh-CN
 
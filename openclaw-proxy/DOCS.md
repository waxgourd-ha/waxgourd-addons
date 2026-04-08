# OpenClaw Bridge

This add-on does not run OpenClaw itself. It bridges an existing OpenClaw gateway into the Home Assistant sidebar via Ingress.

本插件不启动 OpenClaw 服务，只将已有的 OpenClaw 网关桥接到 HA 侧边栏。

---

## Before You Start / 使用前提

You need an OpenClaw instance already running — either via the OpenClaw add-on on the same machine, or a standalone deployment on your local network.

需要已有可用的 OpenClaw 实例在运行——可以是同机安装的 OpenClaw 插件，也可以是局域网内独立部署的服务。

---

## Configuration / 配置

| Option / 选项 | Default / 默认值 | Description / 说明 |
|---|---|---|
| `target_host` | _(empty = localhost)_ | Leave empty if OpenClaw is on the same machine. Set to LAN IP if it's on another device. / 同机留空，其他设备填局域网 IP。 |
| `target_port` | `18789` | OpenClaw gateway port. / OpenClaw 网关端口，未改过不需要动。 |

---

## Troubleshooting / 常见问题

**Panel fails to open / 面板打不开**
Check that OpenClaw is running and the `target_host` / `target_port` are correct.
检查 OpenClaw 服务是否在运行，以及 `target_host` / `target_port` 配置是否正确。

**Panel opens but something looks wrong / 面板打开但功能异常**
The issue is with the OpenClaw service itself, not this bridge. Check the OpenClaw add-on logs.
问题在 OpenClaw 服务端，不是 Bridge 本身，查看 OpenClaw 插件日志。

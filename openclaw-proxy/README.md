# Home Assistant Add-on: OpenClaw Bridge

Bridge your OpenClaw gateway into Home Assistant — access the panel directly from the HA sidebar, no extra ports needed.

将已运行的 OpenClaw 服务桥接到 Home Assistant 侧边栏，无需额外暴露端口，直接在 HA 内访问 OpenClaw 面板。

---

## What This Does

If you already have OpenClaw running (via the [OpenClaw add-on](https://github.com/waxgourd-ha/waxgourd-addons) or a standalone install), this add-on brings the OpenClaw panel into your Home Assistant sidebar through Ingress. No new ports. No extra setup. Just install, start, and OpenClaw appears in the sidebar.

如果你已安装 OpenClaw 插件，或在本机/局域网内独立部署了 OpenClaw，用这个插件把它接进 HA 侧边栏即可。安装启动，侧边栏立刻出现 OpenClaw 入口。

---

## Getting Started / 快速开始

1. Install **OpenClaw Bridge** from the add-on store / 在插件商店安装 **OpenClaw Bridge**
2. Start the add-on / 启动插件
3. **OpenClaw** appears in your HA sidebar — click to open / 侧边栏出现 **OpenClaw** 入口，点击打开

Default settings work for most setups. The bridge connects to `localhost:18789` by default.

默认配置适用于绝大多数场景，无需修改，启动即用。默认连接本机 `18789` 端口。

---

## Configuration / 配置说明

| Option / 选项 | Default / 默认值 | Description / 说明 |
|---|---|---|
| `target_host` | _(empty = localhost)_ | Host where OpenClaw is running. Leave empty if on the same machine. / OpenClaw 所在主机。与 HA 同机运行时留空。 |
| `target_port` | `18789` | Port of the OpenClaw gateway. / OpenClaw 网关端口。未改过端口不需要动。 |

---

## Links

- **OpenClaw** — https://openclaw.ai
- **GitHub** — https://github.com/openclaw/openclaw
- **Docs** — https://docs.openclaw.ai
- **Docs (中文)** — https://docs.openclaw.ai/zh-CN


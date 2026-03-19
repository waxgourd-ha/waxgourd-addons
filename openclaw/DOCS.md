# OpenClaw WG

## ✨ 核心能力

OpenClaw 将大模型能力无缝集成到主流即时通讯软件中，为您打造可靠、可扩展的对话式智能基础设施。

- **多渠道 Gateway 网关**：通过单个 Gateway 网关进程连接 WhatsApp、Telegram、Discord 和 iMessage。
- **插件渠道**：通过扩展包添加 Mattermost 等更多渠道。
- **多智能体路由**：按智能体、工作区或发送者隔离会话。
- **媒体支持**：发送和接收图片、音频、文档。
- **Web 控制界面**：浏览器仪表板，用于聊天、配置、会话和节点管理。
- **移动节点**：配对 iOS 和 Android 节点，支持 Canvas。

## 📥 安装与使用

- 这是一个 Home Assistant Add-on，安装后即可在 Home Assistant 中运行 OpenClaw WG。
- 在 Home Assistant 中进入：`设置 -> 应用 -> 安装应用`，搜索 `OpenClaw WG` 并安装。
- 启动 OpenClaw WG，并打开网页界面。

安装完成后，请访问 `http://<your-home-assistant-ip>:8099` 进入管理后台。

## ⚙️ 配置

```yaml
# 时区设置
timezone: "Asia/Shanghai"

# 网关绑定模式：loopback=仅本地，lan=局域网访问
gateway_bind_mode: "lan"

# 网关端口（默认 18789）
gateway_port: 18789

# 允许 HTTP 认证（仅在无法使用 HTTPS 时启用，存在安全风险）
allow_insecure_auth: true

# 网关公开 URL（用于在新标签页中打开网关 UI）
gateway_public_url: ""

# Home Assistant 长效令牌（用于 HA API 集成）
homeassistant_token: ""

# 启用 Web 终端（在 Home Assistant 内嵌的终端）
enable_terminal: true

# 清理会话锁（启动时/退出时）
clean_session_locks_on_start: true
clean_session_locks_on_exit: true
```

## 💬 聊天命令

可通过 WhatsApp / Telegram / Slack / Google Chat / Microsoft Teams / WebChat 发送以下命令（群组命令仅限所有者）：

- `/status`：显示紧凑会话状态（模型、Token，用时可显示成本）。
- `/new` 或 `/reset`：重置会话。
- `/compact`：压缩当前会话上下文（摘要）。
- `/think <level>`：`off|minimal|low|medium|high|xhigh`（仅限 GPT-5.2 + Codex 模型）。
- `/verbose on|off`：开启或关闭详细输出。
- `/usage off|tokens|full`：控制响应中的使用量信息页脚。
- `/restart`：重启网关（群组内仅限所有者）。
- `/activation mention|always`：切换群组激活模式。

## 📚 文档

- [OpenClaw WG 文档](https://openclaw-wg.readthedocs.io/zh_CN/latest/)

# OpenClaw WG


## ✨ 核心能力

OpenClaw 将大模型能力无缝集成到主流即时通讯软件中，为您打造可靠、可扩展的对话式智能基础设施。
- **多渠道 Gateway 网关** — 通过单个 Gateway 网关进程连接 WhatsApp、Telegram、Discord 和 iMessage。
- **插件渠道** — 通过扩展包添加 Mattermost 等更多渠道。
- **多智能体路由** — 按智能体、工作区或发送者隔离会话。
- **媒体支持** — 发送和接收图片、音频和文档。
- **Web 控制界面** — 浏览器仪表板，用于聊天、配置、会话和节点管理。
- **移动节点** — 配对 iOS 和 Android 节点，支持 Canvas。
## 📥 安装与使用

- 这是一个 Home Assistant Add-on，安装后即可在 Home Assistant 中运行 OpenClaw WG。
- 设置-应用-安装应用-搜索 OpenClaw WG - 安装
- 启动 OpenClaw WG (打开网页界面)

## ⚙️ 配置

```yaml
#时区设置
timezone: "Asia/Shanghai"

#网关绑定模式：loopback=仅本地, lan=局域网访问
gateway_bind_mode: "lan"

#网关端口（默认 18789）
gateway_port: 18789

#允许 HTTP 认证（仅在无法使用 HTTPS 时启用，存在安全风险）
allow_insecure_auth: true

#网关公开 URL（用于在新标签页中打开网关 UI）
gateway_public_url: ""

#Home Assistant 长效令牌（用于 HA API 集成）
homeassistant_token: ""

#启用 Web 终端（在 Home Assistant 内嵌的终端）
enable_terminal: true

#清理会话锁（启动时/退出时）
clean_session_locks_on_start: true
clean_session_locks_on_exit: true```
```
##  聊天命令

通过WhatsApp/Telegram/Slack/Google Chat/Microsoft Teams/WebChat发送这些（群组命令仅限所有者）：

- /status— 紧凑会话状态（模型 + 代币，可用时成本）
- /new或者——重置会话/reset
- /compact— 紧凑会话上下文（摘要）
- /think <level>— off|minimal|low|medium|high|xhigh（仅限GPT-5.2 + Codex模型）
- /verbose on|off
- /usage off|tokens|full—— 按响应使用页脚
- /restart— 重启网关（组内仅限所有者）
- /activation mention|always— 组激活切换（仅限组组）

## 📚 文档
- [OpenClaw WG 文档](https://openclaw-wg.readthedocs.io/zh_CN/latest/)
安装完成后，请访问 `http://<your-home-assistant-ip>:8099` 进入管理后台。
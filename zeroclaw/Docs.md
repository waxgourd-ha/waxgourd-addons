# zeroClaw

## 特性

- 🚀 **极致轻量**: &lt;5MB RAM，启动 &lt;10ms
- 🦀 **纯 Rust**: 单二进制文件，无需复杂依赖
- 🤖 **多模型支持**: OpenAI、Anthropic、OpenRouter、Ollama、Gemini 等 22+ 提供商
- 💬 **多通道**: Telegram、Discord、Slack、Matrix、WhatsApp 等
- 🧠 **本地记忆**: 内置 SQLite 混合搜索（向量+关键词）
- 🔒 **安全优先**: 沙箱、白名单、加密密钥、配对认证

## 安装

1. 添加此仓库到 Home Assistant 的 Add-on Store
2. 安装 "ZeroClaw"
3. 配置 API 密钥和提供商
4. 启动插件

## 配置

### 快速配置（推荐）

在插件配置界面设置：
- **API 密钥**: 你的 OpenRouter/OpenAI 密钥
- **提供商**: 选择模型提供商
- **自治模式**: supervised（推荐）、readonly 或 full

### 高级配置

如需更多自定义，进入容器执行：
```bash
zeroclaw onboard --interactive
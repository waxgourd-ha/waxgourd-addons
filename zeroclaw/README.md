# 冬瓜甄选addons：ZeroClaw AI Assistant

ZeroClaw AI Assistant ，提供可直接在 HA 中运行的 ZeroClaw Gateway Web UI 与配对接口。

## 当前能力

- 基于 Home Assistant add-on 运行 ZeroClaw Gateway
- 默认暴露 Web UI: `http://[HOST]:42617/`
- 支持通过 HA 配置页生成运行配置
- 支持固定字段加 `env_vars` 扩展变量
- 支持配对码鉴权与 Bearer Token 调用
- 对 `/api/channels` 返回兼容 JSON，避免前端解析错误

## 配置入口

在 HA add-on 配置页中使用以下字段：

- `provider`: 默认 provider，例如 `qwen`、`openrouter`、`openai`
- `model`: 默认模型，例如 `qwen3.6-plus`
- `gateway_host`: 对外监听地址，默认 `0.0.0.0`
- `gateway_port`: 对外端口，默认 `42617`
- `api_key`: 通用密钥输入框，会按 provider 自动映射到上游 API key 环境变量
- `env_vars`: 高级扩展变量，仅用于补充上游原生环境变量

更完整的安装、配置、配对和排障说明见 [DOCS.md](DOCS.md)。
## 源
[https://github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
# 冬瓜甄选addons：ZeroClaw AI Assistant

ZeroClaw AI Assistant ，提供可直接在 HA 中运行的 ZeroClaw Gateway Web UI 与配对接口。

## 当前能力

- 基于 Home Assistant add-on 运行 ZeroClaw Gateway
- 默认暴露 Web UI: `http://[HOST]:42617/`
- 支持通过 HA 配置页生成运行配置
- 支持固定字段加 `env_vars` 扩展变量
- 支持配对码鉴权与 Bearer Token 调用
- Web dashboard 静态资源路径固定为 `/usr/share/zeroclawlabs/web/dist`

## 配置入口

在 HA add-on 配置页中使用以下字段：

- `provider`: 默认 provider，例如 `qwen`、`openrouter`、`openai`
- `model`: 默认模型，例如 `qwen3.6-plus`
- `gateway_port`: add-on 对外暴露端口，默认 `42617`
- `api_key`: 通用密钥输入框，会按 provider 自动映射到上游 API key 环境变量
- `env_vars`: 高级扩展变量，仅用于补充上游原生环境变量

当前 add-on 通过 nginx 反向代理到 ZeroClaw 内部网关；Home Assistant 暴露的是外部端口 `42617`，内部 ZeroClaw 实际监听 `42618`。

更完整的安装、配置、配对和排障说明见 [DOCS.md](DOCS.md)。
## 源
[https://github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
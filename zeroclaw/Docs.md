# ZeroClaw AI Assistant

## 概述

快速、小型、全自主的AI个人助理基础设施

当前实现特性：

- 基于 ZeroClaw v0.6.9
- 使用 Home Assistant Debian Base 镜像封装
- 通过 s6 服务启动 ZeroClaw
- 外部监听端口默认是 `42617`
- 内部通过 nginx 代理到 ZeroClaw 实际监听端口 `42618`
- 对 `/api/channels` 提供兼容响应 `{"channels":[]}`，避免前端 JSON 解析错误

## 访问方式

启动后默认访问：

- Web UI: `http://HA_IP:42617/`
- 健康检查: `http://HA_IP:42617/health`
- 配对接口: `POST http://HA_IP:42617/pair`
- Webhook 接口: `POST http://HA_IP:42617/webhook`

## 配置说明

add-on 配置页当前固定字段如下：

```yaml
provider: qwen
model: qwen3.6-plus
gateway_host: 0.0.0.0
gateway_port: 42617
api_key: ""
env_vars: []
```

字段说明：

- `provider`
  ZeroClaw 的默认 provider，例如 `qwen`、`openrouter`、`openai`。

- `model`
  ZeroClaw 的默认模型名称，例如 `qwen3.6-plus`。

- `gateway_host`
  网关监听地址，通常保持 `0.0.0.0` 即可。

- `gateway_port`
  对外暴露端口，默认 `42617`。

- `api_key`
  配置页里的通用密钥输入框。当前 add-on 不会再把它写成 ZeroClaw 顶层 `api_key` 配置，而是按 provider 映射到对应的上游环境变量。

- `env_vars`
  高级扩展变量列表，仅建议填写 ZeroClaw 上游原生支持的环境变量。不要重复填写上面的固定字段。

## API Key 映射规则

为了避免 ZeroClaw 对 generic `api_key` 产生 schema 告警，当前 add-on 会把配置页里的 `api_key` 自动映射成 provider 对应的上游环境变量。

内置映射如下：

- `qwen` 或 `dashscope` -> `DASHSCOPE_API_KEY`
- `openrouter` -> `OPENROUTER_API_KEY`
- `openai` -> `OPENAI_API_KEY`
- `openai-compatible` -> `OPENAI_API_KEY`
- `anthropic` 或 `claude` -> `ANTHROPIC_API_KEY`
- `groq` -> `GROQ_API_KEY`

如果你使用的是其他 provider：

- 可以把配置页里的 `api_key` 留空
- 在 `env_vars` 中填写该 provider 对应的上游环境变量

示例：

```yaml
provider: openrouter
model: openai/gpt-4o-mini
gateway_host: 0.0.0.0
gateway_port: 42617
api_key: sk-or-xxxx
env_vars: []
```

或：

```yaml
provider: some-custom-provider
model: your-model
gateway_host: 0.0.0.0
gateway_port: 42617
api_key: ""
env_vars:
  - name: SOME_CUSTOM_PROVIDER_API_KEY
    value: your-key
```

## 运行配置来源

当前 add-on 的目标是尽量保持“单一真源”。正常情况下，运行配置主要来自 HA 配置页，即容器内的 `/data/options.json`。

启动脚本会：

1. 读取 HA 配置页固定字段
2. 处理 `env_vars`
3. 生成 `/config/zeroclaw/.zeroclaw/config.toml`
4. 按 provider 映射 API key 环境变量
5. 启动 ZeroClaw Gateway 与 nginx

仍保留但不建议依赖的附加来源：

- `/data/zeroclaw.env`
- `/data/runtime_env_vars.json`

收尾阶段已经验证过，当前 add-on 可以只依赖 HA 配置页完成配对和 webhook 调用。

## 配对与调用

ZeroClaw 默认启用配对。首次使用需要先获取配对码，再换取 Bearer Token。

基本流程：

1. 打开 add-on 日志，查看当前 pairing code
2. 调用 `/pair` 获取 token
3. 使用 `Authorization: Bearer <token>` 调用 `/webhook`

示例：

```bash
curl -X POST http://HA_IP:42617/pair \
  -H "X-Pairing-Code: 123456"
```

返回结果中会包含 token。随后调用：

```bash
curl -X POST http://HA_IP:42617/webhook \
  -H "Authorization: Bearer zc_xxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"hello"}'
```


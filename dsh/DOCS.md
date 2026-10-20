# Documentation

*文档*

## What this is

*这是什么*

The NextChat chat UI plus a DeepSeek Harness agent engine. The agent calls tools, reads and
writes files, keeps memory across sessions, and can read and control your Home Assistant
over MCP.

*NextChat 对话界面 + DeepSeek Harness agent 引擎。agent 会调工具、读写文件、跨会话记住
上下文，还能通过 MCP 读取和控制你的 Home Assistant。*

Two places to configure it: the **Configuration** tab for the few things that must exist
before start, and the panel itself — the wizard on first open, and the *Providers / Models*
page.

*配置分两处：**配置** 标签页放启动前必须有的少量设置；其余都在面板里 —— 首次打开的
向导，以及「运营商 / 模型配置」页。*

Engine: DeepSeek Harness SDK `0.1.5rc1`.

*引擎：DeepSeek Harness SDK `0.1.5rc1`（Python）。*

## Install

*安装*

1. **Settings → Add-ons → ⋮ → Repositories** → paste this repository URL.

   *设置 → 加载项 → ⋮ → 仓库 → 粘贴本仓库地址。*
2. Find **NextChat + DSH Agent** → **Install**.

   *找到 **NextChat + DSH Agent** → **安装**。*
3. Open the panel. The wizard asks for a key; *Later* works too.

   *打开面板。向导会问 key；点「稍后再说」也可以。*

Nothing else is required to start chatting.

*其余什么都不用准备，装完就能聊。*

## Options

*选项*

Only the key is worth a look — every other option already has a sensible default.

*只有 key 需要看一眼，其余选项都有合适的默认值。*

- `deepseek_api_key` — *(optional, empty by default)* the key the agent engine uses.
  Leave it blank and the panel wizard asks for it instead.

  *（可选，默认留空）agent 引擎用的 key。留空即可，面板向导会带你填。*

The rest — no need to touch them unless you have a reason:

*其余 —— 没有理由就别改：*

- `deepseek_base_url` — *(default `https://api.deepseek.com`)* only for a compatible gateway, e.g. `https://your-gw/anthropic`.

  *（默认 `https://api.deepseek.com`）只在指向兼容网关时改，形如 `https://your-gw/anthropic`。*
- `provider` — *(default `deepseek-official`)* the official DeepSeek adapter. Other
  providers are added in the panel, not here.

  *（默认 `deepseek-official`）官方 DeepSeek 适配器。其它运营商在面板里加，不在这里。*
- `model` — *(default `deepseek-flash`)* engine default model. The in-panel selector
  overrides it per conversation.

  *（默认 `deepseek-flash`）引擎默认模型。面板里的选择器会按对话覆盖它。*
- `profile` — *(default `sdk`)* `sdk` = full agent (tools, memory, MCP);
  `sdk-minimal` = a lighter profile.

  *（默认 `sdk`）`sdk` = 完整 agent（工具、记忆、MCP）；`sdk-minimal` = 精简档。*
- `reasoning_effort` — *(default `high`)* `off` / `low` / `high` / `max`. Higher thinks
  deeper and answers slower.

  *（默认 `high`）`off` / `low` / `high` / `max`。越高想得越深，也越慢。*
- `max_tokens` — *(default `32768`)* upper bound for one reply.

  *（默认 `32768`）单条回复的上限。*
- `permission_mode` — *(default `danger-full-access`)* lets the agent run tools without
  asking each time. Pick a stricter mode to approve every step.

  *（默认 `danger-full-access`）让 agent 直接执行工具、不逐次确认。想每步都批准就换严格模式。*
- `enable_ha_tools` — *(default `true`)* gives the agent the five Home Assistant tools
  over MCP.

  *（默认 `true`）把 5 个 Home Assistant 工具通过 MCP 交给 agent。*
- `cors_allow_origins` — *(default `*`)* origins allowed to call the agent API.

  *（默认 `*`）允许调用 agent API 的来源。*
- `log_level` — *(default `info`)* how much detail goes to the Supervisor log.

  *（默认 `info`）写入 Supervisor 日志的详细程度。*
- `default_model` — *(default empty)* leave it empty to use the first model of the current
  list. To pin one: `<provider>/<model>@<provider>`.

  *（默认空）建议留空，用当前清单的第一个。要钉死才填 `<运营商>/<模型>@<运营商>`。*
- `hide_user_api_key` — *(default `false`)* keep it off. Turning it on makes browsers that
  saved their own key fail with 401 on every message.

  *（默认 `false`）保持关闭。打开后，存过自己 key 的浏览器每条消息都会 401。*
- `ui_language` — *(default `auto`)* language of the panels this app adds. `auto` follows
  the NextChat locale.

  *（默认 `auto`）本应用额外界面的语言。`auto` 跟随 NextChat 自己的语言。*

Adding a provider: open the panel → **Providers / Models** → pick one → paste the key →
save. The model list reaches the selector immediately; no restart.

*加运营商：打开面板 → 「运营商 / 模型配置」→ 选一家 → 填 key → 保存。
模型清单会立刻同步到选择器，不用重启。*

## Permissions

*权限*

`homeassistant_api` is what lets the agent reach Home Assistant; `hassio_role: manager` is
what lets the bundled `ha` command inspect apps while debugging. No `host_network`, no
exposed ports, no privileged mode — the panel is reachable only through Ingress.

*需要 `homeassistant_api` 才能把 Home Assistant 工具交给 agent；需要 `hassio_role: manager`
是为了容器里的 `ha` 命令在排障时能查应用状态。不使用 `host_network`、不对外开端口、
不以特权模式运行 —— 面板只能从 Home Assistant 的 Ingress 进入。*

## Outside the app

*应用之外*

Nothing to set up in Home Assistant itself. To let the agent control devices, keep
`enable_ha_tools` on — the devices you exposed to Assist are the ones it can see.

*Home Assistant 这边不用额外配置。想让 agent 控制设备，保持 `enable_ha_tools` 打开；
它能看到的设备，就是你暴露给 Assist 的那些。*

## Where your data lives

*数据放在哪*

- `/mnt/data/supervisor/app_configs/nextchat_dsh/nextchat-state/` — server-side copy of the chat
  history (`chat.json`).

  *对话历史的服务端副本（`chat.json`）。*
- `…/agent-memory/` — cross-session memory and the Home Assistant tool call log.

  *跨会话记忆、Home Assistant 工具调用日志。*
- `…/dsh-workspace/` — the agent's working directory.

  *agent 的工作目录。*
- `/data/operators.json` inside the app — provider configuration, including keys.

  *应用内的运营商配置（含 key）。*

All of it is inside the Home Assistant backup scope. **Uninstalling with "remove data"
deletes it**, so back up first.

*这些都在 Home Assistant 的备份范围内。**卸载时勾选删除数据会一起清掉**，重装前先备份。*

## Known limitations

*已知限制*

- Chat history merges the browser copy with the server copy. Clearing site data is
  recoverable; losing the server copy is not.

  *对话历史是浏览器副本 + 服务端副本合并的。清空站点数据可以恢复；服务端副本丢了就真丢了。*
- The wizard appears on first open. *Later* works, but the model list and history need one
  reload to arrive.

  *首次打开会弹向导。点「稍后再说」也能用，但模型清单和历史要等一次刷新。*
- The panel is served through Ingress, so open it from the Home Assistant UI. A raw
  `/api/hassio_ingress/…` URL returns 401 once the session expires.

  *面板走 Ingress，请从 HA 界面打开；直接访问 `/api/hassio_ingress/…` 在会话过期后返回 401。*
- After a restart the panel says "The app is starting, please wait…" and then switches by
  itself. That is normal.

  *应用重启后面板会先显示「应用正在启动，请稍候…」再自己切换，这是正常的。*
- Only one NextChat app should run at a time; each keeps its own session folder.

  *两个 NextChat 应用不要同时运行，它们各有自己的会话目录。*

## Troubleshooting

*出问题怎么办*

- **Blank panel or endless spinner** — check the *Log* tab, restart the app, wait ~20 s,
  reopen the panel.

  *面板空白 / 一直转 —— 看 **日志** 标签页，重启应用，等约 20 秒再开面板。*
- **"App seems not ready, try again?"** — still booting on first start; wait and retry.

  *提示「应用似乎尚未准备就绪」—— 首次启动还在跑，等一会儿点重试。*
- **Empty model list** — no provider key yet; add one on *Providers / Models*.

  *模型列表是空的 —— 还没配运营商 key，去「运营商 / 模型配置」加一个。*
- **401 on every message** — `hide_user_api_key` was turned on, or the Ingress session
  expired; reopen the panel.

  *每条消息 401 —— `hide_user_api_key` 被打开了，或 Ingress 会话过期，重开面板。*
- **The agent cannot control devices** — `enable_ha_tools` must be `true`; the log should
  say `HA tools enabled`.

  *agent 不能控制设备 —— `enable_ha_tools` 要为 `true`；日志里应有 `HA tools enabled`。*

When reporting a bug, include the full log after a restart and the `version`.

*报 bug 时请带上重启后的完整日志和 `version`。*

## License

*许可*

This app bundles [NextChat](https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web) (MIT) and
[DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness). The glue code (shim,
Ingress proxy, self-heal script) ships with the app. Upstream components keep their own
licenses.

*本应用把 NextChat（MIT）与 DeepSeek Harness 打包在一起，胶水代码（shim、Ingress 代理、
自愈脚本）随应用分发。上游组件各自保留其许可。*

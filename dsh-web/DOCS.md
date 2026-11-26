# Documentation

*文档*

## What this is

*这是什么*

The official DeepSeek Harness web UI, running as a Home Assistant app. It is the engine's own
front-end — conversations, workspaces, plugins, scheduled tasks, a trace view — and it can read
and change things in your Home Assistant for you.

*DeepSeek Harness 官方 Web 界面，作为 Home Assistant 应用运行。它是引擎自带的前端 ——
对话、工作区、插件、定时任务、轨迹视图 —— 而且它懂你的 Home Assistant，能帮你查、帮你改。*

Two places to configure it: the **Configuration** tab for the few things that must exist
before start, and the panel itself (the UI's own settings).

*配置分两处：**配置** 标签页放启动前必须有的少量设置；其余都在面板里（界面自带的设置）。*

Engine: DeepSeek Harness `0.2.2-rc.5`.

*引擎：DeepSeek Harness `0.2.2-rc.5`。*

## Install

*安装*

1. **Settings → Add-ons → ⋮ → Repositories** → paste this repository URL.

   *设置 → 加载项 → ⋮ → 仓库 → 粘贴本仓库地址。*
2. Find **DeepSeek Harness (Web)** → **Install**.

   *找到 **DeepSeek Harness (Web)** → **安装**。*
3. Open the panel. The first start takes ~30 seconds (the engine initialises its profile);
   the panel shows a waiting page and switches over by itself.

   *打开面板。首次启动约 30 秒（引擎要初始化配置档），面板会先显示等待页，然后自己切进去。*

## Options

*选项*

Only the key is worth a look — every other option already has a sensible default.

*只有 key 需要看一眼，其余选项都有合适的默认值。*

- `deepseek_api_key` — *(optional, empty by default)* the key the engine uses. Leave it blank
  and set it in the UI's settings instead.

  *（可选，默认留空）引擎用的 key。留空即可，改在界面设置里填。*
- `workspace` — *(default `/config/dsh-workspace`)* the folder the agent works in. It lives
  in the app's own config folder, so it travels with your Home Assistant backups.

  *（默认 `/config/dsh-workspace`）agent 干活的目录。它在应用自己的配置目录里，随 HA 备份一起走。*

Nothing else to enable: the assistant can already work with your home — look things up, switch
things, run scripts, adjust automations — as soon as you start talking to it.

*不用再开什么开关：装好就能直接让它干活 —— 查状态、开关设备、跑脚本、调自动化，开口说就行。*

The rest — no need to touch them unless you have a reason:

*其余 —— 没有理由就别改：*

- `deepseek_base_url` — *(default empty)* usually left empty; the adapter fills in the endpoint
  itself. Only for a compatible gateway, e.g. `https://your-gw/anthropic`.

  *（默认空）通常留空，地址由适配器自己补。只在指向兼容网关时填，形如 `https://your-gw/anthropic`。*
- `log_level` — *(default `info`)* how much detail goes into the app log.

  *（默认 `info`）应用日志的详细程度。*

## Permissions

*权限*

It runs with the normal Home Assistant access an app needs to work with your devices, and
nothing more: no host network, no open ports, no privileged mode. The panel is only reachable
from inside Home Assistant (through the sidebar).

*它只用「能和你的设备打交道」该有的权限，多的没有：不占用宿主网络、不对外开放端口、
不以特权模式运行。面板只能从 Home Assistant 里（侧边栏）打开。*

## Where your data lives

*数据放在哪*

- `/data/dsh-home` inside the app — engine profile, sessions, attachments, workspace state.

  *应用内的引擎配置档、会话、附件、工作区状态。*
- `…/app_configs/dsh_web/dsh-workspace/` — the agent's working folder.

  *agent 的工作目录。*
- `…/app_configs/dsh_web/agent-memory/` — cross-session memory and the tool call log.

  *跨会话记忆与工具调用日志。*
- `…/app_configs/` (mounted read-write at `/app_configs`) — every app's config folder, so the
  agent can inspect or adjust them.

  *所有应用的配置目录（容器内 `/app_configs`，可写），agent 可以查看或调整。*

All of it is inside the Home Assistant backup scope. **Uninstalling the app deletes its
`/data`** (sessions included), so back up first.

*这些都在 Home Assistant 的备份范围内。**卸载会删掉应用的 `/data`**（含会话），重装前先备份。*

## Known limitations

*已知限制*

- The upstream engine is still a **preview** (0.2.x); its plugin API keeps changing.

  *上游引擎仍是**预览版**（0.2.x），插件 API 还会变。*
- First start takes ~30 seconds to initialise the profile. The panel shows a waiting page.

  *首次启动要约 30 秒初始化配置档，面板会显示等待页。*
- File browsing shows container paths, not Home Assistant's own `/config`.

  *文件浏览看到的是容器内路径，不是 HA 自己的 `/config`。*
- Open it from the Home Assistant sidebar — there is no separate port or address to remember.

  *从 Home Assistant 侧边栏打开就行，不用记端口和地址。*

## Troubleshooting

*出问题怎么办*

- **Panel stuck on the waiting page** — still starting; give it up to a minute. If it stays,
  check the *Log* tab and restart the app.

  *面板停在等待页 —— 还在启动，最多等一分钟。一直不动就看 **日志** 标签页并重启应用。*
- **The panel loads but its plugins don't** — reload once; if it keeps happening, restart the
  app and send the log.

  *面板打开了但插件没加载出来 —— 先刷新一次；一直这样就把应用重启，并把日志一起反馈。*
- **The agent cannot control devices** — restart the app; if it still cannot, send the log.

  *agent 不能控制设备 —— 先重启应用；还不行就把日志发来。*
- **No model listed** — no key yet. Set it in the Configuration tab or in the UI's settings.

  *没有可用模型 —— 还没配 key。在「配置」标签页或界面设置里填。*

When reporting a bug, include the full log after a restart and the `version`.

*报 bug 时请带上重启后的完整日志和 `version`。*

## License

*许可*

This app bundles [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness). The
Home Assistant side of it ships with the app. Upstream components keep their own licenses.

*本应用打包了 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)。
面向 Home Assistant 的那部分随应用分发。上游组件各自保留其许可。*
# NextChat + DSH Agent

*NextChat + DSH 智能助手*

A real AI agent in your Home Assistant sidebar. It does not just answer — it plans, calls
tools, reads and writes files, and can read and control your Home Assistant over MCP.

*在 Home Assistant 侧边栏里放一个能真正动手的 AI 助手。它不只回答问题 —— 它会拆任务、
调工具、读写文件，还能通过 MCP 读取和控制你的 Home Assistant。*

## What it does

*能做什么*

- **Chat that gets work done** — the agent splits a task into steps, runs tools, and hands
  back the result.

  *聊天 + 干活：agent 会拆任务、调工具，把结果交付回来。*
- **Controls Home Assistant** — five built-in MCP tools: list entities, get state, call a
  service, list services, render a template. "Dim the living room lights" is enough.

  *控制 Home Assistant：内置 5 个 MCP 工具 —— 列实体、读状态、调服务、列服务、渲染模板。
  一句「把客厅灯调暗一点」就能落地。*
- **Any provider** — DeepSeek, Kimi, Qwen, Doubao, MiniMax, OpenAI, Gemini, Groq and more.
  Paste a key on the *Providers / Models* page; no restart.

  *多运营商随意切：DeepSeek / Kimi / 通义 / 豆包 / MiniMax / OpenAI / Gemini / Groq 等，
  在「运营商 / 模型配置」页填 key 即可，改完不用重启。*
- **History that follows you** — conversations sync back to the app's own folder and travel
  with your Home Assistant backups.

  *换设备也有历史：对话记录同步回应用自己的目录，随 HA 备份一起走。*

## What you need

*需要什么*

One model API key. Nothing else.

*一个模型 API key，别的都不用。*

## Install

*安装*

1. **Settings → Add-ons → ⋮ → Repositories** — paste this repository URL.

   *设置 → 加载项 → ⋮ → 仓库 —— 粘贴本仓库地址。*
2. Find **NextChat + DSH Agent** — **Install**. It opens seconds later.

   *找到 **NextChat + DSH Agent** —— 点安装，几秒就能打开。*
3. Open the panel and paste the key when the wizard asks.

   *打开面板，按向导填入 API key。*

Optional settings, troubleshooting and the license are on the **Documentation** tab.

*可选项、故障排查和许可协议都在 **文档** 标签页。*

> Only one NextChat app should run at a time.
> *两个 NextChat 应用不要同时启动。*

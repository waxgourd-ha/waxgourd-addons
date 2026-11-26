# DeepSeek Harness (Web)

*DeepSeek Harness（官方 Web 界面版）*

The official DeepSeek Harness web UI, opened from your Home Assistant sidebar. No extra chat
front-end in between — the engine's own interface, and it can read and change things in your
Home Assistant for you.

*把 DeepSeek Harness 的官方 Web 界面放进 Home Assistant 侧边栏。中间不再套一层聊天前端 ——
就是引擎自带的界面，而且它能读写文件、也懂你的 Home Assistant。*

## What it does

*能做什么*

- **The engine's own UI** — conversations, workspaces, plugins, scheduled tasks and a
  trace view, exactly as the upstream project ships them.

  *引擎原生的界面：对话、工作区、插件、定时任务、轨迹视图，都是上游项目原本的样子。*
- **A real agent** — it plans, calls tools, reads and writes files in a workspace, and keeps
  context across sessions.

  *真正的 agent：会拆任务、调工具、在工作区里读写文件，并跨会话保留上下文。*
- **Understands your home** — ask it to look something up or change something: a sensor
  reading, turning a light on, running a script, editing an automation.

  *懂你的家：让它查个状态、开关灯、跑个脚本、改条自动化，直接说就行。*
- **Attachments and images** — paste or attach an image in the composer and ask about it.

  *附件与图片：在输入框里粘贴或上传图片，直接问它。*
- **Any provider you can reach the official UI with** — set the key in the app's options, or
  in the UI's own settings.

  *模型密钥：可以在应用选项里填，也可以在官方界面的设置里填。*

## What you need

*需要什么*

One model API key. Nothing else.

*一个模型 API key，别的都不用。*

## Install

*安装*

1. **Settings → Add-ons → ⋮ → Repositories** — paste this repository URL.

   *设置 → 加载项 → ⋮ → 仓库 —— 粘贴本仓库地址。*
2. Find **DeepSeek Harness (Web)** — **Install**. First start takes about half a minute while
   the engine prepares its profile.

   *找到 **DeepSeek Harness (Web)** —— 点安装。首次启动要半分钟左右，引擎要先准备自己的配置档。*
3. Open the panel from the sidebar and start a conversation in the pre-created workspace.

   *从侧边栏打开面板，在预先建好的工作区里直接开始对话。*

Optional settings, troubleshooting and the license are on the **Documentation** tab.

*可选项、故障排查和许可协议都在 **文档** 标签页。*

> This app runs the engine on its own. Running it next to the two NextChat apps is fine —
> they are separate apps with separate data.

> *本应用独立运行引擎。与两个 NextChat 应用同时安装没问题 —— 它们是各自独立的应用和数据。*
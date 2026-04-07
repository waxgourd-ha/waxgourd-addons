
# Home Assistant Add-on: OpenClaw

Bring OpenClaw AI into your Home Assistant — chat with your smart home, configure by conversation, and let AI and HA work as one. No command line required.

[![Add to Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fwaxgourd-ha%2Fwaxgourd-addons)

---

If you already love Home Assistant, you know how powerful it gets when everything just works together. This add-on brings OpenClaw — an AI assistant — into your HA, without needing to be a developer to use it.

**The idea is simple:** HA takes care of your home. OpenClaw takes care of the thinking. Together, they're more than the sum of their parts.

<!-- screenshot: drag your panel screenshot into the GitHub README editor to upload it, then replace the src below with the generated URL -->
<img alt="OpenClaw panel — gateway status, chat, and terminal in one place" src="https://github.com/user-attachments/assets/YOUR-IMAGE-ID-HERE" />

---

## Who This Is For

You don't need to know what a terminal is. You don't need to pick between GPT-4o and Claude. You don't need to read a 1000-line documentation page before getting started.

If you can use Home Assistant, you can use this.

---

## What Makes This Different

### Your AI dashboard, right inside HA

Once installed, OpenClaw appears in your HA sidebar. From there you can see the gateway status, restart it, open a chat session, or access the terminal — all in one place, without leaving Home Assistant.

Think of it as OpenClaw living inside HAOS as its own independent host. It starts when HA starts. It runs quietly in the background. You interact with it when you need it.

### Talk to configure, not type commands

Most OpenClaw setups require running commands in a terminal to get things working. This add-on includes a curated set of built-in skills so you can configure the most common things — connecting to HA, setting up AI channels, adjusting gateway settings — just by having a conversation with OpenClaw.

No command line. No manual config files. Just chat.

### Models ready to use, no guesswork

First time using an AI assistant? The model allowlist means you get a pre-selected set of recommended models. You don't have to choose between dozens of providers and wonder which one is worth paying for. Pick one from the list, add your API key, and you're done.

When you're more comfortable, you can expand the list however you like.

### Connects to HA the right way

This add-on follows Home Assistant's own directory conventions — `/config`, `/share`, `/media` are all available to OpenClaw. That means the AI can read your HA configuration, work with your media files, and help you with automations without any extra setup on your part.

Plus, `ha` CLI is included, so OpenClaw can actually talk to Home Assistant directly.

### Security stays inside your home network

OpenClaw runs entirely within your local network. It doesn't need to be exposed to the internet. If you do want to connect from outside, that's what [OpenClaw Bridge](https://github.com/openclaw/openclaw-proxy) is for — a dedicated proxy that keeps your HA port as the only thing facing the outside world.

Your home network is your security boundary. This add-on respects that.

---

## Getting Started

1. Add this repository to Home Assistant's add-on store
2. Install **OpenClaw**
3. Start the add-on — it will be ready in under a minute
4. Click **OpenClaw** in the sidebar
5. Add your AI provider API key in the settings panel
6. Start a conversation

That's it. OpenClaw is ready to help.

---

## What You Can Do

Once it's running, try asking OpenClaw things like:

- *"Show me all my HA automations"*
- *"What's the temperature in the living room right now?"*
- *"Help me create an automation that turns off the lights at midnight"*
- *"What skills are available?"*
- *"Install the home assistant skill"*

The more you use it with HA, the more useful it becomes.

---

## What's Inside

### Ready-to-install skills

These skills are available from the panel — install by name, no commands needed:

| Skill | What it does | Notes |
|---|---|---|
| `home-assistant` | Control devices, read states, create automations via HA REST API | Recommended first install |
| `mcp-hass` | Deeper HA integration via MCP protocol | For richer AI-HA interaction |
| `memory-manager` | Gives OpenClaw persistent memory across conversations | — |
| `skill-vetter` | Security screening before installing unknown skills | — |
| `skill-creator` | Helps you build your own custom skills | For advanced users |
| `frontend-design` | AI-assisted frontend interface creation | — |
| `clawddocs` | OpenClaw documentation assistant | — |

The recommended starting point is `home-assistant`. Once that's installed and connected, OpenClaw can see and control your HA entities.

### Bundled command-line tools

For those who like to know what's under the hood — the container includes:

| Tool | Purpose |
|---|---|
| `ha` | Home Assistant Supervisor CLI — control addons, check status, manage HA directly |
| `jq` / `yq` | JSON and YAML processors — useful for working with HA config files |
| `git` | Version control |
| `curl` / `wget` | HTTP clients |
| `vim` | Text editor |
| `python3` | Python runtime |
| `ssh` | SSH client (for connecting to other devices) |
| `ping` / `tcpdump` / `ip` | Network diagnostics |
| Node.js 22 | Runtime for OpenClaw and skill packages |
| ttyd | Powers the in-panel web terminal |

All of these are accessible from the web terminal in the panel.

---

## Going Further

The panel also includes a web terminal. If you want to dig deeper into OpenClaw — installing additional skills, checking logs, running a command — it's there when you need it. But you'll find you rarely have to use it.

As you get comfortable, you can:
- Add more AI providers and models
- Install community skills via conversation
- Use OpenClaw Bridge to access your setup from outside your home network

### Add-on update notifications

The panel checks for add-on updates automatically. When a new version is available, a banner appears at the top of the panel showing the current and latest version numbers.

Clicking the banner opens an upgrade dialog with two options:
- **One-click**: jump directly to the add-on page in HA to update from there
- **CLI fallback**: a ready-to-run `ha apps update <slug>` command if you prefer the terminal

This is especially useful when running OpenClaw as a standalone AI host — you don't need to go digging through HA settings to know when something new is available. The panel tells you, and you can act on it right there.

### Upgrading OpenClaw independently

The add-on ships with a fixed OpenClaw version. If you want to run a newer OpenClaw release without waiting for an add-on update, you can upgrade it directly from the web terminal:

```bash
npm install -g openclaw@latest
```

After upgrading, restart the gateway from the panel. The add-on itself stays the same — only the OpenClaw runtime inside it changes.

---

## About This Edition

This is the international English edition of the OpenClaw HA add-on, focused on a clean out-of-box experience for everyday HA users. It intentionally keeps things simple — no heavy toolchains, no complex setup flows — so OpenClaw and Home Assistant can complement each other without getting in the way.

**OpenClaw** — https://openclaw.ai  
**GitHub** — https://github.com/openclaw/openclaw  
**Docs** — https://docs.openclaw.ai
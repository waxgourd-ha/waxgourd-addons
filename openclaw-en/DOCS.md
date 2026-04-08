# OpenClaw — Getting Started

---

## Step 1: Start the Add-on

After installing, go to the add-on page and click **Start**. It usually takes under a minute.

Once running, **OpenClaw** appears in your Home Assistant sidebar. Click it to open the panel.

---

## Step 2: The Panel at a Glance

The panel is your OpenClaw control center — everything you need is here.

| Area | What it does |
|---|---|
| **Gateway status** | Shows whether the OpenClaw gateway is running. Use the restart button here if anything feels stuck. |
| **Chat** | Opens a conversation with OpenClaw. This is where you do most things. |
| **Terminal** | A browser-based terminal inside the container. There when you need it — skip it if you don't. |
| **Settings** | Add your AI provider API key and choose a model. Do this first before chatting. |

> **First thing to do:** Open Settings, pick a model from the list, and add your API key. Then you're ready to chat.

---

## Step 3: Install Your First Skill

Most people think of AI as a smarter search engine — you ask, it answers. OpenClaw works differently. Once you give it a skill, it doesn't just answer you — it acts. It reads your devices, creates automations, changes settings. You talk, it works.

OpenClaw also supports connecting to external chat apps — WhatsApp, Telegram, and others — so you can send it instructions from wherever you are. Those setups are covered in the [OpenClaw documentation](https://docs.openclaw.ai).

Skills are what make this possible — each one gives OpenClaw the ability to do a specific category of things.

To install the Home Assistant skill, just tell OpenClaw:

> *"Install the home-assistant skill"*

That's it. OpenClaw handles the rest. Once installed, it can see your HA entities, read sensor states, and help you build automations — all through conversation.

**Other skills you can ask about:**

| Skill | What it does |
|---|---|
| `home-assistant` | Control devices, read states, create automations via HA REST API — **start here** |
| `mcp-hass` | Deeper HA integration via MCP protocol |
| `memory-manager` | Gives OpenClaw persistent memory across conversations |
| `skill-creator` | Helps you build your own custom skills |
| `frontend-design` | AI-assisted frontend interface creation |

---

That's the quick start. Most users won't need anything else.

---

## Advanced

### Accessing the Panel from Your Local Network

The panel runs on port `8099` of the machine where Home Assistant is installed. You can open it directly from any browser on your local network:

```
http://<your-ha-ip>:8099
```

This works independently of Home Assistant — you don't need to go through the HA sidebar. It's the primary way to access the panel.

The HA sidebar entry (Ingress) is an additional convenience — it embeds the panel inside the HA interface. Both work at the same time by default.

If you want to block direct IP access and allow the sidebar only, set `ingress_only: true` in the add-on configuration.

### Configuration Reference

Default settings are safe to leave as-is. You only need to change something if you have a specific reason.

| Option | Default | When to change |
|---|---|---|
| `ingress_only` | `false` | Set to `true` to block direct LAN access to port 8099 |
| `timezone` | `UTC` | Set to your local timezone, e.g. `Asia/Shanghai` |
| `gateway_bind_mode` | `lan` | Set to `loopback` if you want gateway port 18789 invisible on LAN |
| `gateway_port` | `18789` | Change only if this port conflicts with another service |
| `allow_insecure_auth` | `true` | Set to `false` if your HA is running HTTPS |
| `gateway_public_url` | _(empty)_ | Set if you access OpenClaw via a public domain or reverse proxy |
| `enable_terminal` | `true` | Set to `false` to hide the terminal tab |
| `enable_ssh` | `false` | Set to `true` only if you need SSH access into the container |
| `ssh_port` | `22` | Change if port 22 is already in use |
| `ssh_username` | `root` | SSH login username |
| `ssh_password` | _(empty)_ | Set a strong password if SSH is enabled |
| `clean_session_locks_on_start` | `true` | Leave on — clears stale lock files at startup |
| `clean_session_locks_on_exit` | `true` | Leave on — cleans up on shutdown |

### Troubleshooting

**Add-on won't start**
Open the add-on **Log** tab. Usually it's a port conflict — check if something else is using port `8099` or `18789`.

**Panel opens but AI doesn't respond**
Go to Settings and verify your API key and model are configured. If the gateway shows as stopped, use the restart button in the panel.

**Can't reach the panel from LAN**
Check that `ingress_only` is `false` and `gateway_bind_mode` is `lan`. Also check your host firewall isn't blocking port `8099`.

**SSH not working**
Make sure `enable_ssh: true` is set and the configured `ssh_port` isn't in use by another service.

- Website https://openclaw.ai
- GitHub https://github.com/openclaw/openclaw
- Docs https://docs.openclaw.ai
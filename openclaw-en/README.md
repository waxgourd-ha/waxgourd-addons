
# Home Assistant Add-on: OpenClaw

This edition keeps core OpenClaw gateway capabilities and removes plugin installation flows by design.

## What This Add-on Provides

- OpenClaw Web UI in Home Assistant (Ingress + optional direct LAN access)
- Multi-channel gateway runtime (depends on upstream OpenClaw capabilities)
- Optional embedded terminal for maintenance
- Optional SSH shell for development scenarios

## Quick Start

1. Add and install `openclaw-en` in Home Assistant.
2. Start the add-on.
3. Open from Home Assistant sidebar (Ingress), or access `http://<HA_IP>:8099` when direct access is enabled.
4. Complete initial OpenClaw setup in the web UI.

## Configuration Overview

Most commonly used options:

- `ingress_only`: Restrict access to Home Assistant panel only
- `timezone`: Runtime timezone
- `gateway_bind_mode`: `loopback` (local only) or `lan` (LAN access)
- `gateway_port`: OpenClaw gateway port (default `18789`)
- `allow_insecure_auth`: Allow HTTP auth when HTTPS is unavailable
- `gateway_public_url`: Public URL used by UI shortcuts
- `enable_terminal`: Enable embedded web terminal
- `enable_ssh`: Enable SSH shell (disabled by default)

## Upstream Reference
 - Website https://openclaw.ai
 - GitHub https://github.com/openclaw/openclaw
 - Docs https://docs.openclaw.ai/zh-CN
# OpenClaw Documentation

This document explains how to install, configure, and operate the `openclaw-en` Home Assistant add-on.

## 1. Scope

- Add-on name: `OpenClaw`
- Slug: `openclaw-en`
- Current version: `2026.3.24`
- This is the English edition. Plugin installation flow is intentionally removed.

## 2. Installation

1. Open Home Assistant add-on store.
2. Install `OpenClaw` (`openclaw-en`).
3. Start the add-on.
4. Open UI from Home Assistant panel.

If direct access is allowed, UI is also available on:

- `http://<HOME_ASSISTANT_IP>:8099`

## 3. Access Modes

- Ingress access: embedded inside Home Assistant add-on page
- Direct LAN access: through host network and port `8099`

Use `ingress_only: true` to force panel-only access and block direct LAN access.

## 4. Configuration Reference

Example options:

```yaml
ingress_only: false
timezone: "UTC"
gateway_bind_mode: "lan"
gateway_port: 18789
allow_insecure_auth: true
gateway_public_url: ""
enable_terminal: true
enable_ssh: false
ssh_port: 22
ssh_username: "root"
ssh_password: ""
clean_session_locks_on_start: true
clean_session_locks_on_exit: true
```

Option details:

- `ingress_only`:
	Restrict web access to Home Assistant panel only.
- `timezone`:
	Runtime timezone string, for example `UTC` or `Asia/Shanghai`.
- `gateway_bind_mode`:
	`loopback` means local-only binding; `lan` allows LAN access.
- `gateway_port`:
	OpenClaw gateway service port, default `18789`.
- `allow_insecure_auth`:
	Allow HTTP authentication when HTTPS is not available. Security risk on untrusted networks.
- `gateway_public_url`:
	Public URL shown/used by gateway UI shortcuts.
- `enable_terminal`:
	Enable embedded web terminal in add-on UI.
- `enable_ssh`:
	Enable SSH shell in container (disabled by default).
- `ssh_port`, `ssh_username`, `ssh_password`:
	SSH service credentials and port.
- `clean_session_locks_on_start`, `clean_session_locks_on_exit`:
	Cleanup stale lock files to reduce startup/shutdown lock issues.

## 5. Network and Port Notes

- This add-on uses `host_network: true`.
- Ensure the following ports are not occupied by other add-ons/services:
	- `8099` (web UI)
	- `18789` (gateway default)
	- `ssh_port` when SSH is enabled

If startup fails due to port conflict, stop the conflicting service or change port settings.

## 6. Security Recommendations

- Keep `enable_ssh: false` unless required.
- If SSH is enabled, set a strong password or switch to key-based auth externally.
- Set `allow_insecure_auth: false` whenever HTTPS is available.
- Prefer `ingress_only: true` for single-panel usage in trusted HA environments.

## 7. Troubleshooting

- Add-on fails immediately after launch:
	check add-on logs first, then verify port conflicts and invalid option values.
- UI not reachable from LAN:
	confirm `ingress_only: false`, `gateway_bind_mode: lan`, and host firewall rules.
- SSH unavailable:
	verify `enable_ssh: true`, configured `ssh_port`, and no port conflict.

## 8. Upstream Reference

- Website https://openclaw.ai
- GitHub https://github.com/openclaw/openclaw
- Docs https://docs.openclaw.ai
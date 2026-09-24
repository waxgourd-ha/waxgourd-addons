# Changelog

## [22.0.6.3] - 2026-09-18

### 汉化
- 关于页面（About）changelog 汉化（5.0.0 ~ 5.0.7）

---

## [22.0.6.2] - 2026-09-18

### 汉化
- 补充 Link 节点汉化（link call 帮助面板 + link out「发送到所有/返回」模式说明）
- 修复 link/function 节点的 link call 错误消息翻译缺失（键名 error→errors）

---

## [22.0.6.1] - 2026-09-17

### 升级
- 上游基础镜像 `hassio-addons/node-red:22.0.0` → `22.0.6`（base:21.0.0 → 21.0.5）
- **Node-RED 5.0.0 → 5.0.7**
- `node-red-contrib-modbus` 5.45.2 → 5.60.2
- `node-red-node-email` 5.2.4 → 5.2.5
- `js-yaml` 4.2.0 → 5.4.2
- Node.js 24.16.0 → 24.18.1

### 汉化
- 编辑器新增「资源管理器」侧边栏面板翻译（`sidebar.explorer`）
- Modbus 14 个节点帮助面板补充新增内容（示例流程提示、IO 配置数据类型规则、响应过滤器寄存器校验、缓冲服务器说明）
- 更新 Node-RED 5.0 导览弹窗汉化（修复 4.1 遗留内容）
- 更新日志汉化补充 5.0.1 ~ 5.0.7

---

## [22.0.0.1] - 2026-06-11

### 升级
- 上游基础镜像 `hassio-addons/node-red:21.0.10` → `22.0.0`（base:20.1.1 → 21.0.0）
- **Node-RED 4.1.10 → 5.0.0**（主版本升级）
- `@node-red-contrib-themes/theme-collection` 4.1.1 → 5.0.1
- `js-yaml` 4.1.1 → 4.2.0
- `node-red-node-email` 5.2.3 → 5.2.4
- Node.js 24.14.1 → 24.16.0

### 变更
- 新增 IPv6 直连支持（`direct.gtpl`）
- 新增 `dark-modern` 主题选项（旧 `dark` 自动迁移）
- `bashio::addon.*` → `bashio::app.*` API 适配
- npm 安装参数适配：`--no-optional` → `--omit=optional`
- 移除 `node-red-dashboard`（3.6.6）及其所有汉化
- 移除 `node-red-node-twitter`（1.2.0）及其汉化

---

## [21.0.7.4] - 2026-04-29

### 升级
- 上游基础镜像 `hassio-addons/node-red:21.0.7` → `21.0.10`（base:20.1.0 → 20.1.1）
- `node-red` 4.1.8 → 4.1.10
- `node-red-node-feedparser` 1.0.5 → 1.0.7

### 汉化
- Node-RED 更新日志补充 4.1.9 ~ 4.1.10

---

## [21.0.7.3] - 2026-04-28

### 汉化
- Node-RED 更新日志汉化（覆盖 4.1.0 ~ 4.1.8）

---

## [21.0.7.2] - 2026-04-28

### 优化
- 汉化文件改为构建时固化到镜像（消除每次启动时 109 个文件的复制开销）
- 修复健康检查：动态读取 HA 分配的 ingress 端口（原硬编码 1880 导致 unhealthy）

---

## [21.0.7.1] - 2026-04-28

### 升级
- 上游基础镜像 `hassio-addons/node-red:21.0.6` → `21.0.7`（base:20.0.4 → base:20.1.0）
- `node-red-node-email` 5.2.2 → 5.2.3（依赖安全修复）

---

## [21.0.6.3] - 2026-04-28

### 修复
- nginx 启动延迟 5 分钟问题：`nginx/run` 中等待端口号与实际监听端口不一致（46836 → 46837）

### 汉化
- modbus-client 帮助文本：用 `modbus_client_patched.html` 替换主文件内联英文帮助块

---

## [1.0.0] - 2026-04-21

### 新增
- 首个汉化版本，基于 `hassio-addons/node-red:21.0.6`
- 汉化覆盖：Node-RED 核心编辑器、内置节点、第三方插件
  - node-red 核心：编辑器 UI、节点消息（nr_editor_zh.json / nr_nodes_zh_messages_patched.json）
  - node-red-contrib-modbus：所有节点帮助文本 + modbus-server/flex-sequencer 主文件内联块替换
  - node-red-dashboard：所有 UI 节点帮助文本（dash_help_ui_* / dash_html_ui_*）+ i18n JSON
  - node-red-contrib-home-assistant-websocket：全节点帮助文本（ha_ws_index.html）
  - node-red-contrib-bigtimer：帮助文本
  - node-red-contrib-moment：帮助文本
  - node-red-contrib-sunevents：帮助文本
  - node-red-node-email / feedparser / suncalc / twitter：帮助文本
  - 其他内置节点：25-serial、base64、counter、influxdb、interval_length、random、rbe、smooth、state-machine、time-range-switch、cast-to-client 等
- GitLab CI 构建流水线（`amd64-x.x.x` / `aarch64-x.x.x` / `x.x.x` tag 触发）
- 翻译注入机制：容器启动时由 `config.js` IIFE 自动将 `/etc/ha-translations/` 下文件复制到对应 node_modules 目录

### 修复
- CI：镜像源切换为国内可用源（docker.1panel.live）
- CI：GitLab Runner 拉取策略配置（if-not-present）
- fix: 恢复侧边栏 paletteLabel 为英文原文（避免与节点内部逻辑冲突）
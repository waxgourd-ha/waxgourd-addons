# Node-RED 汉化版

[Node-RED][nodered] 是一款面向物联网的可视化流程编程工具，可将硬件设备、API 和在线服务以全新方式连接起来。

它提供基于浏览器的编辑器，通过丰富的节点面板轻松构建流程，并可一键部署到运行时。

## 安装

安装方式与其他 Home Assistant 插件相同，十分简单。

1. 点击下方按钮，在你的 Home Assistant 实例中打开本插件。

   [![在 Home Assistant 中打开此插件][addon-badge]][addon]

1. 点击"安装"按钮安装插件。
1. 启动"Node-RED"插件。
1. 查看"Node-RED"的日志，确认一切正常。
1. 点击"打开网页界面"按钮进入 Node-RED。
1. 插件开箱即用，无需配置服务器！

**注意**：插件已**预配置**，无需手动添加/修改服务器连接设置！

## 配置

**注意**：_修改配置后请重启插件使其生效。_

配置示例：

```yaml
log_level: info
http_node:
  username: MarryPoppins
  password: Supercalifragilisticexpialidocious
http_static:
  username: MarryPoppins
  password: Supercalifragilisticexpialidocious
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
system_packages:
  - ffmpeg
npm_packages:
  - node-red-admin
init_commands:
  - echo 'This is a test'
  - echo 'So is this...'
```

**注意**：_以上仅为示例，请勿直接复制粘贴！请根据实际情况自行配置。_

### 选项：`log_level`

`log_level` 控制插件日志的输出级别，可根据排查问题的需要调整详细程度。可选值：

- `trace`：显示所有细节，包括所有内部函数调用。
- `debug`：显示详细的调试信息。
- `info`：正常运行时的常规事件（推荐）。
- `warning`：非错误性的异常情况。
- `error`：不需要立即处理的运行时错误。
- `fatal`：发生严重错误，插件无法正常使用。

每个级别会自动包含更高严重级别的日志，例如 `debug` 也会显示 `info` 消息。默认值为 `info`，非排查问题时建议保持默认。

### 选项：`ssl`

启用或禁用网页界面的 SSL（HTTPS）。设为 `true` 启用，`false` 禁用。

**注意**：_SSL 设置仅对直接访问有效，对 Ingress 服务无效。_

### 选项：`certfile`

SSL 使用的证书文件。

**注意**：_文件必须存放在 `/ssl/` 目录下（默认路径）。_

### 选项：`keyfile`

SSL 使用的私钥文件。

**注意**：_文件必须存放在 `/ssl/` 目录下（默认路径）。_

### 选项：`credential_secret`

Node-RED 在存储时会使用密钥对凭据进行加密。此选项用于指定你的密钥，可以是任意字符串，类似密码。请妥善保存，日后（如恢复备份时）可能需要用到。

**注意**：_一旦设置此属性，请勿修改——否则 Node-RED 将无法解密已有凭据，导致凭据丢失。_

**注意**：_如果你在 Node-RED 中手动启用了项目功能，此选项虽然必填，但会被 Node-RED 忽略。_

### 选项：`theme`

设置 Node-RED 的界面主题。当前可用选项：

- `default`
- `aurora`
- `cobalt2`
- `dark`
- `dracula`
- `espresso-libre`
- `github-dark`
- `github-dark-default`
- `github-dark-dimmed`
- `midnight-red`
- `monoindustrial`
- `monokai`
- `monokai-dimmed`
- `night-owl`
- `noctis`
- `noctis-azureus`
- `noctis-bordo`
- `noctis-minimus`
- `noctis-obscuro`
- `noctis-sereno`
- `noctis-uva`
- `noctis-viola`
- `oceanic-next`
- `oled`
- `one-dark-pro`
- `one-dark-pro-darker`
- `railscasts-extended`
- `selenized-dark`
- `selenized-light`
- `solarized-dark`
- `solarized-light`
- `tokyo-night`
- `tokyo-night-light`
- `tokyo-night-storm`
- `totallyinformation`
- `zenburn`
- `zendesk-garden`

### 选项：`http_node`

为节点定义的 HTTP 端点（`httpNodeRoot`）设置密码保护，可配置以下属性：

- `username`
- `password`

**注意**：_使用 `http_node` 需要在"网络"配置中为 Node-RED 开放端口（除 Ingress 外）。HTTP 节点将以 `/endpoint/` 路径呈现。如使用 `node-red-dashboard`，其页面同样托管在此路径下，并使用此处配置的凭据。_

### 选项：`http_static`

为静态内容（httpStatic）设置密码保护，可配置以下属性：

- `username`
- `password`

### 选项：`system_packages`

指定额外安装的 [Alpine 软件包][alpine-packages]（如 `g++`、`make`、`ffmpeg`）。

**注意**：_安装的包越多，插件启动时间越长。_

### 选项：`npm_packages`

指定额外安装的 [NPM 包][npm-packages] 或 [Node-RED 节点][node-red-nodes]（如 `node-red-dashboard`、`node-red-contrib-ccu`）。

**注意**：_安装的包越多，插件启动时间越长。_

### 选项：`init_commands`

通过 `init_commands` 进一步自定义 Node-RED 环境。在列表中添加一条或多条 Shell 命令，每次插件启动时都会执行。

### 选项：`safe_mode`

设为 `true` 时，Node-RED 将以 `--safe` 标志启动，不启动任何流程，用于故障排查。

### 选项：`leave_front_door_open`

设为 `true` 并留空用户名和密码，可禁用插件的身份验证。

**注意**：_即使插件仅在内网使用，我们也**强烈不建议**开启此选项。风险自负！_

### 选项：`max_old_space_size`

设置 Node.js V8 引擎旧内存区的最大内存（MB）。当内存占用接近上限时，V8 会加大垃圾回收力度以释放内存。

<https://nodejs.org/api/cli.html#--max-old-space-sizesize-in-megabytes>

## 配置文件夹

插件的大部分配置（包括 `flows.json`）存储在 Node-RED 的配置文件夹中。

## 时区配置

插件默认使用 Home Assistant 中配置的时区。如时区不正确，请在 Home Assistant 设置中更新时区，然后重启 Node-RED 插件使其生效。

如需单独为 Node-RED 指定时区，可在 `settings.js` 文件中配置：用文本编辑器打开该文件，在 `module.exports = {` 行上方添加：

`process.env.TZ = "Asia/Shanghai";`

根据实际环境修改时区名称，保存后重启 Node-RED 插件。

## 已知问题与限制

- 本插件内置 Node-RED Dashboard，但目前不支持通过 Ingress 访问 Dashboard，这是 Node-RED Dashboard 本身的技术限制。

- 如果无法访问 HTTP 节点或 Node-RED Dashboard，请检查"网络"配置中是否已设置端口号以启用直接访问模式。

- 访问 HTTP 节点或 Dashboard 时，URL 须以 `/endpoint/` 开头，否则 Home Assistant 身份验证会介入拦截。

- 如升级后出现以下错误：`WARNING (MainThread) [hassio.api.proxy] Unauthorized WebSocket access!`，请验证 Node-RED 中 Home Assistant 服务器的配置——双击任意 HA 节点，点击服务器名旁的铅笔图标，确保勾选了"我使用 Home Assistant 插件"选项。

## 更新日志与发布

发布记录基于 [Keep a Changelog][keepchangelog] 格式，版本号遵循 [语义化版本][semver] 规范：

- `MAJOR`：不兼容或重大变更。
- `MINOR`：向后兼容的新功能和增强。
- `PATCH`：向后兼容的错误修复和依赖更新。

## 支持

有问题？可通过以下渠道获取帮助：

- [Home Assistant 社区论坛][forum]
- [Node-RED 官方文档][nodered-docs]
- 在 [GitHub 提交 Issue][issue]

## 许可证

MIT License

Copyright (c) 2018-2026 Franck Nijhof

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_nodered&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[alpine-packages]: https://pkgs.alpinelinux.org/packages
[contributors]: https://github.com/hassio-addons/app-node-red/graphs/contributors
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-node-red/55023?u=frenck
[issue]: https://github.com/TinkeringHa/addons-hage/issues
[node-red-nodes]: https://flows.nodered.org/?type=node&num_pages=1
[nodered-docs]: https://nodered.org/docs
[nodered]: https://nodered.org
[npm-packages]: https://www.npmjs.com
[keepchangelog]: https://keepachangelog.com/zh-CN/1.0.0/
[semver]: https://semver.org/spec/v2.0.0.html

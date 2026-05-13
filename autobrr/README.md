# Home Assistant add-on: Autobrr

## 关于

---

[Autobrr](https://autobrr.com/) 是一款面向 Torrent 场景的现代化下载自动化工具。它借鉴了 trackarr、autodl-irssi、flexget 等工具的思路，目标是用一个工具覆盖完整自动化流程并提供更多能力。

本插件基于 Docker 镜像：https://github.com/autobrr/autobrr

## 安装

---

安装方式与其他 Home Assistant 插件基本一致。

1. 将我的插件仓库添加到你的 Home Assistant 实例（在 Supervisor 插件商店右上角添加）
1. 安装本插件。
1. 点击 保存 按钮存储配置。
1. 按需设置插件参数。
1. 启动插件。
1. 查看日志确认是否正常运行。
1. 打开 WebUI 调整软件选项。

## 配置

WebUI 可通过 http://homeassistant.local:7474 访问，也可通过 Ingress 入口访问。
默认账号密码：admin / password（首次登录后请立即修改）。

### 初始化步骤

1. 启动插件后访问 Web 界面
2. 修改默认登录凭据
3. 配置 RSS 索引器和下载客户端
4. 设置自动化规则与过滤器
5. 用样例发布信息进行测试

### 配置项

| 选项 | 类型 | 默认值 | 说明 |
|--------|------|---------|-------------|
| PGID | int | 0 | 文件权限使用的组 ID |
| PUID | int | 0 | 文件权限使用的用户 ID |
| TZ | str |  | 时区，例如 Europe/London |
| localdisks | str |  | 要挂载的本地磁盘，例如 sda1,sdb1 |
| networkdisks | str |  | 要挂载的 SMB 共享，例如 //SERVER/SHARE |
| cifsusername | str |  | SMB 共享用户名 |
| cifspassword | str |  | SMB 共享密码 |
| cifsdomain | str |  | SMB 域 |

### 配置示例

```yaml
PGID: 1000
PUID: 1000
TZ: "Europe/London"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/downloads"
cifsusername: "dluser"
cifspassword: "password123"
cifsdomain: "workgroup"
```

### 磁盘挂载

本插件支持挂载本地磁盘和远程 SMB 共享：

- 本地磁盘：见 https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons
- 远程共享：见 https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons

### 自定义脚本与环境变量

本插件支持自定义脚本执行和环境变量注入：

- 自定义脚本：见 https://github.com/alexbelgium/hassio-addons/wiki/Running-custom-scripts-in-Addons
- env_vars 选项：可通过 env_vars 传入额外环境变量（变量名支持大小写）。说明见 https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon-2

## 支持

如需帮助，请在 GitHub 提交 issue。

[repository]: https://github.com/alexbelgium/hassio-addons

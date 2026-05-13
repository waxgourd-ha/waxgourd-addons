# Autobrr

## 功能简介

Autobrr 是一个面向 Torrent 场景的下载自动化工具，可根据 RSS、规则和过滤条件自动处理发布信息并推送到下载客户端。

本 Home Assistant 插件为 Autobrr 提供：
- Web 管理界面
- Ingress 访问支持
- 本地磁盘和 SMB 网络共享挂载能力
- 通过环境变量进行扩展配置

## 默认访问信息

- WebUI 地址：http://homeassistant.local:7474
- 也可通过 Home Assistant Ingress 访问
- 默认账号：admin
- 默认密码：password

首次登录后请立即修改默认账号和密码。

## 配置项

可在插件配置中设置以下参数：

- PUID：运行用户 ID
- PGID：运行组 ID
- TZ：时区
- localdisks：本地磁盘挂载列表（例如 sda1,sdb1）
- networkdisks：SMB 共享地址（例如 //SERVER/SHARE）
- cifsusername：SMB 用户名
- cifspassword：SMB 密码
- cifsdomain：SMB 域

示例：

```yaml
PUID: 1000
PGID: 1000
TZ: "Asia/Shanghai"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/downloads"
cifsusername: "dluser"
cifspassword: "password123"
cifsdomain: "workgroup"
```

## 快速开始

1. 安装并启动插件。
2. 打开 WebUI，使用默认账号密码登录。
3. 修改默认登录凭据。
4. 添加索引器（Indexers）与下载客户端（Clients）。
5. 创建过滤规则（Filters）和动作（Actions）。
6. 用测试条目验证自动化流程。

## 存储与挂载

- 如需访问外部磁盘，可使用 localdisks 配置本地挂载。
- 如需访问 NAS 或共享目录，可使用 networkdisks 配置 SMB 挂载。
- 建议先验证挂载读写权限，再启用自动化规则。

参考：
- 本地磁盘挂载：https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons
- 远程共享挂载：https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons

## 自定义能力

- 可通过 env_vars 注入额外环境变量。
- 可结合自定义脚本实现启动前后扩展逻辑。

参考：
- 环境变量：https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon-2
- 自定义脚本：https://github.com/alexbelgium/hassio-addons/wiki/Running-custom-scripts-in-Addons

## 常见问题

1. 无法进入页面
- 检查插件是否已启动。
- 检查 7474 端口是否被占用。
- 优先尝试 Ingress 方式访问。

2. 登录失败
- 确认是否已修改默认账号密码。
- 若忘记密码，可清理配置后重新初始化。

3. 自动化规则不生效
- 检查 Indexer、Filter、Action 是否完整关联。
- 检查下载客户端连接状态和权限。
- 查看插件日志定位规则匹配问题。

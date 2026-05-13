# Home Assistant add-on：addons updater

## 关于

本插件可根据上游新版本发布，自动更新插件版本号。**这是一个仅面向开发者的辅助工具。** 普通用户无需使用本插件来更新插件——HA 会在有更新时自动提醒。

## 安装

安装方式与其他插件完全相同，非常简单。

1. 将我的插件仓库添加到你的 Home Assistant 实例（在 Supervisor 插件商店右上角添加）
1. 安装本插件。
1. 按照下方说明完成配置。
1. 点击 `保存` 按钮存储配置。
1. 启动插件。
1. 查看插件日志，确认一切正常。

## 配置

本插件无 Web 界面，配置分两部分进行。

### Updater.json

在你仓库中各插件目录下（即 config.json/config.yaml 所在位置）创建 `updater.json` 文件。插件将读取此文件来获取上游信息。**只有包含 updater.json 的插件才会被自动更新。**
可参考[此示例](https://github.com/alexbelgium/hassio-addons/blob/master/arpspoof/updater.json)。

文件支持以下字段：

- `github_fulltag`：`true` 时保留完整 tag（如 `v3.0.1-ls67`），`false` 时只取数字部分（如 `3.0.1`）
- `github_beta`：`true/false`，是否同时检查预发布版本
- `github_havingasset`：`true` 时要求 release 包含二进制附件
- `github_tagfilter`：只选包含指定文本的 tag
- `github_exclude`：排除包含指定文本的 tag
- `last_update`：自动维护，记录上次上游更新日期
- `repository`：来自 GitHub 的 `用户名/仓库名`
- `paused`：`true` 时暂停该插件的自动更新
- `slug`：插件的 slug 名称
- `source`：上游来源，可选 `dockerhub`/`github`/`gitlab`/`bitbucket`/`pip`/`hg`/`sf`/`website-feed`/`local`/`helm_chart`/`wiki`/`system`/`wp`/`codeberg`（Codeberg 通过其 Gitea API 支持，自动配置）
- `upstream_repo`：`用户名/仓库名`，例如 `linuxserver/docker-emby`
- `upstream_version`：自动维护，记录当前跟踪的上游版本号
- `dockerhub_by_date`：DockerHub 专用，`true` 时按最后更新时间而非版本号排序
- `dockerhub_list_size`：DockerHub 专用，检查的 tag 列表条数

### 插件配置

在此填写连接你的 GitHub 仓库所需的参数。

```yaml
repository: '用户名/仓库名'  # 来自 GitHub
gituser: 你的 GitHub 用户名
gitapi: 你的 GitHub API Token（Classic）https://github.com/settings/tokens
gitmail: 你的 GitHub 邮箱
date_iso8601: true  # 使用 ISO8601 格式（YYYY-MM-DD），否则使用 DD-MM-YYYY
verbose: 'false'
```

示例：

```yaml
repository: alexbelgium/hassio-addons
gituser: 你的 GitHub 用户名
gitapi: 你的 GitHub API Token
gitmail: 你的 GitHub 邮箱
date_iso8601: true
verbose: "false"
```

### 自定义脚本与环境变量

本插件通过 `addon_config` 映射支持自定义脚本和环境变量：

- **自定义脚本**：参见 [在插件中运行自定义脚本](https://github.com/alexbelgium/hassio-addons/wiki/Running-custom-scripts-in-Addons)
- **环境变量**：使用插件的 `env_vars` 选项，详见 [为插件添加环境变量](https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon)

[repository]: https://github.com/alexbelgium/hassio-addons
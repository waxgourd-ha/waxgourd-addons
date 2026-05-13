# Repository Updater

本插件是**面向开发者**的工具，用于自动将你的 HA 插件仓库中各插件版本号与上游源保持同步。普通最终用户无需使用本插件来更新插件。

---

## 工作原理

启动后，插件会：

1. 克隆或拉取你的 GitHub 插件仓库到本地 `/data`
2. 遍历所有包含 `updater.json` 文件的插件目录
3. 从对应上游源（GitHub、DockerHub、GitLab 等）获取最新版本号
4. 若版本有更新，自动修改 `config.yaml`、`Dockerfile` 等文件中的版本号，追加 `CHANGELOG.md` 条目
5. 将变更提交并推送回你的 GitHub 仓库

---

## 前置要求

- 一个 GitHub 账号，且对目标仓库有写入权限
- 一个 GitHub Personal Access Token（Classic），需要具备 `repo` 权限
  - 获取地址：https://github.com/settings/tokens

---

## 插件配置

在 HA 插件配置页面填写以下参数：

| 参数 | 是否必填 | 说明 |
|------|----------|------|
| `repository` | 必填 | 你的插件仓库，格式 `用户名/仓库名`，例如 `alexbelgium/hassio-addons` |
| `gituser` | 必填 | GitHub 用户名 |
| `gitapi` | 必填 | GitHub Personal Access Token |
| `gitmail` | 可选 | GitHub 邮箱，用于 git commit 署名 |
| `date_iso8601` | 可选 | 日期格式，`true` 使用 `YYYY-MM-DD`，`false` 使用 `DD-MM-YYYY`，默认 `true` |
| `dry_run` | 可选 | `true` 时只检查不提交，测试用 |
| `verbose` | 可选 | `true` 时输出更详细日志 |
| `env_vars` | 可选 | 额外环境变量列表，格式为 `name`/`value` 键值对 |

示例配置：

```yaml
repository: yourname/hassio-addons
gituser: yourname
gitapi: ghp_xxxxxxxxxxxxxxxx
gitmail: you@example.com
date_iso8601: true
verbose: false
```

---

## updater.json 配置

在每个需要自动更新的插件目录下创建 `updater.json` 文件。可参考 [template.json](template.json) 作为起点。

| 字段 | 必填 | 说明 |
|------|------|------|
| `slug` | 必填 | 插件的 slug 名称，与 `config.yaml` 一致 |
| `source` | 必填 | 上游来源，可选值见下方 |
| `upstream_repo` | 必填 | 上游仓库，格式依 source 不同而异 |
| `upstream_version` | 自动 | 当前跟踪的上游版本，由插件自动维护 |
| `last_update` | 自动 | 上次更新日期，由插件自动维护 |
| `paused` | 可选 | `true` 时跳过该插件的更新 |
| `github_beta` | 可选 | `true` 时包含预发布/beta 版本 |
| `github_fulltag` | 可选 | `true` 时保留完整 tag（如 `v3.0.1-ls67`），`false` 时只取数字部分 |
| `github_havingasset` | 可选 | `true` 时只选包含二进制附件的 release |
| `github_tagfilter` | 可选 | 只选包含此文本的 tag |
| `github_exclude` | 可选 | 排除包含此文本的 tag |
| `dockerhub_by_date` | 可选 | DockerHub 专用，`true` 时按最后更新时间而非版本号排序 |
| `dockerhub_list_size` | 可选 | DockerHub 专用，检查的 tag 列表条数，默认 `100` |

支持的 `source` 值：

- `github` / `gitlab` / `bitbucket` / `codeberg`
- `dockerhub`
- `pip` / `hg` / `sf` / `wp`
- `website-feed` / `helm_chart` / `wiki` / `system` / `local`

示例（跟踪 Docker Hub 镜像）：

```json
{
  "slug": "emby",
  "source": "dockerhub",
  "upstream_repo": "linuxserver/docker-emby",
  "upstream_version": "",
  "last_update": "",
  "paused": false,
  "github_beta": false,
  "github_fulltag": false,
  "github_havingasset": false,
  "github_tagfilter": "",
  "github_exclude": "",
  "dockerhub_by_date": false,
  "dockerhub_list_size": "100"
}
```

示例（跟踪 GitHub Release）：

```json
{
  "slug": "myapp",
  "source": "github",
  "upstream_repo": "owner/repo",
  "upstream_version": "",
  "last_update": "",
  "paused": false,
  "github_beta": false,
  "github_fulltag": false,
  "github_havingasset": false,
  "github_tagfilter": "",
  "github_exclude": ""
}
```

---

## 执行逻辑说明

- 插件以 `boot: manual` 模式运行，**每次手动启动执行一轮扫描**，完成后自动停止
- 只有存在 `updater.json` 的插件目录才会被处理
- 更新时修改的文件范围：`config.json`、`config.yaml`、`Dockerfile`、`build.json`、`build.yaml`
- 提交信息格式：`Updater bot : <slug> updated to <version>`
- 开启 `dry_run` 后，脚本结束时会清除 `/data` 下的临时拉取内容，不产生任何 git 提交

---

## 常见问题

**Q: 插件启动后立即停止，是否正常？**
是的，本插件是一次性执行工具，跑完一轮扫描就退出，属于预期行为。

**Q: 某个插件的更新暂停了怎么办？**
在对应插件的 `updater.json` 中将 `paused` 设为 `false` 即可恢复。

**Q: 安装时提示连接 ghcr.io 失败怎么办？**
这是镜像拉取阶段失败，与插件本身逻辑无关。请检查 HA 主机的 DNS 配置，推荐将 DNS 改为 `223.5.5.5` 或 `1.1.1.1` 后重试。

**Q: 想测试但不想真正推送代码怎么办？**
将配置中的 `dry_run` 设为 `true`，插件只会做检查，不会执行任何 git commit/push。

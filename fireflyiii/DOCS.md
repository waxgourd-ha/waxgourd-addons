# Firefly III

Firefly III 是一款自托管的个人财务管理工具，可用于记录收入、支出、账户与预算。
此 Home Assistant 加载项基于官方镜像运行，并提供 Ingress 访问与常见数据库配置。

## 重要提醒

首次启动前请务必修改 `APP_KEY`。

- 默认值仅用于占位，不能用于生产环境
- `APP_KEY` 初始化后与数据库绑定
- 后续如果要变更，通常需要重置数据库

建议在第一次启动前就设置一个安全且固定的 `APP_KEY`。

## 快速开始

1. 安装加载项。
2. 在配置中修改 `APP_KEY`。
3. 选择数据库类型（默认 `sqlite_internal`）。
4. 如果使用外部数据库，补全 `DB_HOST`、`DB_PORT`、`DB_DATABASE`、`DB_USERNAME`、`DB_PASSWORD`。
5. 保存并启动加载项。
6. 查看日志确认启动成功。
7. 通过 Ingress 或端口访问 Web UI，完成 Firefly III 初始化向导。

## 配置说明

### 核心参数

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `APP_KEY` | str | `CHANGEME_32_CHARS_EuC5dfn3LAPzeO` | 关键加密密钥，首次启动前必须修改 |
| `CONFIG_LOCATION` | str | `/config/addons_config/fireflyiii/config.yaml` | 附加配置文件路径 |
| `DB_CONNECTION` | list | `sqlite_internal` | 数据库类型：`sqlite_internal` / `mariadb_addon` / `mysql` / `pgsql` |
| `DB_HOST` | str | 空 | 外部数据库主机 |
| `DB_PORT` | str | 空 | 外部数据库端口 |
| `DB_DATABASE` | str | 空 | 外部数据库名 |
| `DB_USERNAME` | str | 空 | 外部数据库用户名 |
| `DB_PASSWORD` | str | 空 | 外部数据库密码 |
| `Updates` | list | 空 | 自动更新检查频率：`hourly` / `daily` / `weekly` |
| `silent` | bool | `true` | 静默模式；设为 `false` 可输出更多调试信息 |
| `env_vars` | list | `[]` | 额外环境变量列表（高级） |

### 数据库选型建议

- `sqlite_internal`：最省事，适合个人轻量使用或快速试用。
- `mariadb_addon`：与 Home Assistant MariaDB 加载项配合，适合长期稳定使用。
- `mysql` / `pgsql`：适合已有外部数据库基础设施的场景。

## 示例配置

### 1) 最小配置（内置 SQLite）

```yaml
APP_KEY: "your_32_chars_or_more_secure_key_here"
DB_CONNECTION: "sqlite_internal"
silent: true
```

### 2) MariaDB 配置示例

```yaml
APP_KEY: "your_32_chars_or_more_secure_key_here"
DB_CONNECTION: "mariadb_addon"
DB_HOST: "core-mariadb"
DB_PORT: "3306"
DB_DATABASE: "firefly"
DB_USERNAME: "firefly"
DB_PASSWORD: "strong_password"
silent: false
```

## 访问方式

- Ingress：在加载项页面点击 Open Web UI。
- 端口访问：默认映射 `8080/tcp`，可按需调整。
- 可选 SSL 端口：`8443/tcp`（如启用并配置对应环境）。

## 高级配置

除加载项 UI 暴露的参数外，你还可以通过 `env_vars` 注入更多 Firefly III 环境变量。

`env_vars` 格式示例：

```yaml
env_vars:
  - name: APP_ENV
    value: production
  - name: TZ
    value: Asia/Shanghai
```

更多可用变量可参考 Firefly III 官方 `.env.example`。

## 常见问题

### 1) 启动后页面报错或无法初始化

优先检查：

- `APP_KEY` 是否已修改
- `APP_KEY` 是否在首次启动前就已设置
- 数据库连接参数是否正确

### 2) 修改 APP_KEY 后应用异常

这通常是因为已有数据库已绑定旧密钥。
常见处理方式是恢复旧 `APP_KEY`，或清空/重建数据库后重新初始化。

### 3) 使用外部数据库连接失败

请确认：

- 数据库容器或主机可达
- 端口开放正确
- 用户名、密码、库名正确
- 数据库允许该来源地址访问

### 4) 需要更多调试信息

将 `silent` 设为 `false`，重启后查看加载项日志。

## 维护建议

- 升级前先备份数据库和关键配置。
- 固定保存好 `APP_KEY`，避免后续迁移或恢复时丢失。
- 若使用外部数据库，建议启用数据库层面的定期备份。

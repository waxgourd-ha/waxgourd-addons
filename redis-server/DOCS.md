# Redis Server

Redis 是一个开源的内存数据库，可以用作缓存、消息代理和数据存储。此插件为您的 Home Assistant 安装 Redis 服务器。

## 安装

1. 在 Home Assistant 中添加此存储库 URL 到您的插件商店
2. 安装 Redis 服务器插件
3. 启动 Redis 服务器插件

## 如何使用

安装后，Redis 服务器将在默认端口（6379）上运行，并可以通过 Home Assistant 或者网络中的其他设备连接它：

```
redis-cli -h <YOUR_HOME_ASSISTANT_IP> -p 6379
```

如果您设置了密码，可以通过以下方式连接：

```
redis-cli -h <YOUR_HOME_ASSISTANT_IP> -p 6379 -a <YOUR_PASSWORD>
```

### 配置

以下选项可在插件配置页面上设置：

```yaml
# 示例配置
port: 6379  #服务器监听端口（默认：6379）
databases: 4 #数据库数量（默认：4）
password: mypassword # 强烈建议设置密码
appendonly: true #启用持久化存储（默认：开启）
```

#### 选项 `port`

Redis 服务器的监听端口。默认是 6379。

#### 选项 `databases`

Redis 实例中的数据库数量。默认是 4。

#### 选项 `password`

可选的 Redis 认证密码。为了安全起见，强烈建议设置此选项。

#### 选项 `appendonly`

默认情况下，Redis 数据将保存在`/data`目录中。启用/禁用 AOF（Append Only File）持久化。此选项默认为启用，确保在重启后数据仍然可用。

## 高级配置

本插件支持使用完整的 Redis 配置文件进行高级配置。插件首次启动时，会在`/config/redis/redis.conf`创建一个默认的 Redis 配置文件，并通过软链接连接到`/etc/redis.conf`。

您可以通过直接编辑`/config/redis/redis.conf`文件来自定义 Redis 的所有设置。这些更改将在插件下次重启时生效。

### 配置文件路径

- 主配置文件：`/config/redis/redis.conf`
- 软链接位置：`/etc/redis.conf`

### 常用高级配置选项

以下是一些您可能需要在配置文件中调整的常用高级选项：

```
# 内存限制
maxmemory 100mb
maxmemory-policy allkeys-lru

# 快照配置
save 900 1
save 300 10
save 60 10000

# 连接限制
maxclients 1000

# 日志级别
loglevel notice
```

关于所有可用配置选项的详细说明，请参考[Redis 官方文档](https://redis.io/topics/config)。

### 注意

- 如果您在配置文件中修改了基本设置（如端口号），请确保同时更新插件的配置选项，以保持一致性。
- 建议在修改配置文件前先创建备份。
- 不当的配置更改可能导致 Redis 服务无法启动。

## 使用案例

Redis 服务器可以用于多种场景：

1. 高速缓存
2. 用于 Home Assistant 自动化规则的消息代理
3. 临时数据存储
4. 跨设备/服务的共享状态存储


## 注意事项

- 默认情况下，Redis 仅监听本地网络。
- 建议为您的 Redis 实例设置密码以增强安全性。
- 如果您修改了配置文件中的基本设置（如端口），请确保同时更新插件的配置选项，以保持一致性。

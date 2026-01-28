# kodbox 可道云企业网盘

## 关于
在线文档管理，共享文件夹
### 🛠️ 安装方法
**通过 GitHub 仓库（推荐）**
1. 进入 设置 → 加载项 → 加载项商店
1. 点击右上角菜单 → 仓库
1. 添加仓库地址：https://github.com/waxgourd/addons
1. 在商店中找到 kodbox 并点击安装

## 通过环境变量自动配置
本插件**仅通过 env_vars 配置**,kodbox容器支持通过环境变量自动配置。您可以在首次运行时预先配置安装页面上要求的所有内容。要启用自动配置，请通过以下环境变量设置数据库连接。

**MYSQL/MariaDB**:

- `MYSQL_DATABASE` 数据库名.
- `MYSQL_USER` 数据库用户.
- `MYSQL_PASSWORD` 数据库用户密码.
- `MYSQL_HOST` 数据库服务地址.
- `MYSQL_PORT` 数据库端口，默认3306

如果设置了任何值，则在首次运行时不会在安装页面中询问这些值。通过使用数据库类型的所有变量完成配置后，您可以通过设置管理员和密码（仅当您同时设置这两个值时才有效）来配置kodbox实例：

- `KODBOX_ADMIN_USER` 管理员用户名.
- `KODBOX_ADMIN_PASSWORD` 管理员密码.
- `RANDOM_ADMIN_PASSWORD` 值为·true·时生成随机密码，从日志查看.

**redis/memcached**:

- `REDIS_HOST` redis地址.
- `REDIS_PASSWORD` redis密码.

**uid/gid**:

- `PUID`代表站点运行用户nginx的用户uid
- `PGID`代表站点运行用户nginx的用户组gid

**PHP参数**

- `FPM_MAX` php-fpm最大进程数, 默认50
- `FPM_START` php-fpm初始进程数, 默认10
- `FPM_MIN_SPARE` php-fpm最小空闲进程数, 默认10
- `FPM_MAX_SPARE` php-fpm最大空闲进程数, 默认30

## 其他设置

- [自定义容器IP](https://docs.kodcloud.com/setup/docker/#ip)
- [挂载NFS卷](https://docs.kodcloud.com/setup/docker/#nfs)
- [挂载SMB卷](https://docs.kodcloud.com/setup/docker/#cifssmb)

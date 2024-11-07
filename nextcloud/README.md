# 冬瓜甄选addons：Nextcloud

## 关于

nextcloud个人专属或团队共享的私有云同步网盘，该版本在原版nextcloud中增加了Home assistant的优化调整和配置选项。

### 使用mariadb 作为主要的数据库 (感谢@amaciuc)

如果你在第一次运行webui时,注意以下警告:

```bash
Performance warning
You chose SQLite as database.
SQLite should only be used for minimal and development instances. For production we recommend a different database backend.
If you use clients for file syncing, the use of SQLite is highly discouraged.
```

解决这个问题，请遵循以下步骤:

- 1、安装 `mariadb` ，随机填写信息配置然后启动。为了在网络中能够被“nextcloud”找到，成功启动它很重要。

- 2、安装' nextcloud '插件(或者如果你已经安装了，重新启动它)，观察日志，直到你会注意到以下'警告':

  ```bash
  WARNING: MariaDB addon was found! It can't be configured automatically due to the way Nextcloud works, but you can configure it manually when running the web UI for the first time using those values :
  Database user : service
  Database password : Eangohyuchae6aif7saich2nies8xaivaejaNgaev6gi3yohy8ha2aexaetei6oh
  Database name : nextcloud
  Host-name : core-mariadb:3306
  ```

- 3、回到“mariadb”附加组件，用上面的凭据配置它并重新启动它。确保插件正在创建“netxcloud”数据库。

- 4、进入web并填写所有必需的信息。下面是一个例子:

![image](https://raw.githubusercontent.com/waxgourd-ha/waxgourd-addons/refs/heads/main/nextcloud/images/nextcloud-1.png)
## 来源

- 原始版来源：https://github.com/haberda/hassio_addons
- 加载项基于：https://github.com/linuxserver/docker-nextcloud

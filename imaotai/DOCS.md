# imaotai

## 配置说明

### 一、安装及配置 数据库

- 进入配置 - 加载项商店 找到并安装 Official add-ons中找到MariaDB。

- 安装完成后点击配置，在选项中找到“Databases”选项并输入“campus_imaotai”。

- 在Logins选项内的“- password”处输入 数据库的自定义密码。

```
- password:WaxGourdHAos
```

- 在Rights选项内最下面回车**新建一行**输入 ：
```
- database: campus_imaotai
  username: homeassistant
```
- 点击保存并启动MariaDB

### 二、安装及配置 i茅台

- 进入配置 - 加载项商店 找到并安装 i茅台。

- 安装完成后点击配置，在选项中找到''db_pass*"处输入 数据库的自定义密码。

- 点击保存并启动 i茅台

- 在日志处点击刷新直至出现“接口服务运行成功.”字样得系统启动成功。（注意：该项目使用java开发，启动慢和运行占用内存较多）

- 回到信息页中点击“打开 WEB UI”进入平台，登录即可操作。



平台配置请查看官方教程：[教程网址](https://oddfar.github.io/campus-doc/campus-imaotai/#%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)

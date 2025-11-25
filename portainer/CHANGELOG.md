## 2.33.4 (25-11-2025)
- 从portainer/portainer更新到最新版本（更改日志：https://github.com/portainer/portainer/releases)
- Home Assistant项目已经弃用了对armv7、armhf和i386架构的支持。在即将发布的家庭助理2025.12版本中，将完全放弃支持
- 添加了通过config.yaml旁边的“env_vars”附加选项配置额外环境变量的支持。看https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon-2了解详情。
## "2.35.0" (24-10-2025)
- 修正了已知错误
## 2.35.0 (24-10-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
## 2.34.0 (26-09-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
## 2.33.1 (30-08-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
### 2.33-0 (25-08-2025)
- 版本升级
### 2.32.0-7 (15-08-2025)
- 通过清除冲突的安全头信息来修复入口问题。
### 2.32.0-6 (25-07-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
### 2.31.3 (11-07-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
### 2.31.2-5 (01-07-2025)
- 修复了小错误
### 2.31.1 (23-06-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
### 2.31.0 (18-06-2025)
- 从portainer/portainer更新到最新版本 (更改日志 : https://github.com/portainer/portainer/releases)
### 2.30.1-2 (30-05-2025)
- 映射内部/config以允许自定义脚本执行和变量
- 修复无效的来源
### 2.30.1 (24-05-2025)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)
### 2.30.0 (17-05-2025)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)
### 2.29.2 (27-04-2025)
- 已知问题
 - Podman支持的已知问题
  1. Podman环境不受自动入职脚本的支持
  1. 在Docker上运行Portainer服务器时，无法通过socket添加Podman环境（反之亦然）
  1. 仅支持CentOS 9，Podman 5 rootful
- 变化
1. 撤销了github.com/gorilla/csrf库的版本升级



### 2.29.0 (19-04-2025)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)
### 2.28.1 (22-03-2025)
- 已知问题
1. Podman支持的已知问题
1. Podman环境不受自动入职脚本的支持
1. 在Docker上运行Portainer服务器时，无法通过socket添加Podman环境（反之亦然）
1. 仅支持CentOS 9，Podman 5 rootful
- 变化
1. 修复了使用CA签名的TLS证书在Kubernetes环境中可见的“无法检索命名空间”错误
- 弃用和删除的功能：
1. 弃用的功能 没有
1. 已删除功能 没有
### 2.27.1 (03-03-2025)
- 已知问题
  <hr>
  
 - Docker支持的已知问题

 1. 在Docker上首次从Git部署堆栈时，GitOps更新选项不可见（但可以在部署堆栈后进行配置）

 - Podman支持的已知问题

 1. Podman环境不受自动入职脚本的支持
 1. 在Docker上运行Portainer服务器时，无法通过socket添加Podman环境（反之亦然）
 1. 仅支持CentOS 9，Podman 5 rootful

- 变化
  <hr>

 1. 安全：已解决CVE-2024-50338

 1. 修复了未使用.env插入Compose文件的问题



### 2.27.0 (24-02-2025)

- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.26.1 (07-02-2025)

- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.25.1 (08-01-2025)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.24.1 (07-12-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.24.0 (21-11-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.23.0 (21-10-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.22.0-3 (06-10-2024)
- 警告：新安装的逻辑更改。在插件的密码中键入“空”以重置数据库并进行干净的初始设置。例如，用于还原备份

### 2.22.0 (05-10-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.21.2 (28-09-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.21.1 (26-09-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.21.0 (02-09-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.20.1 (13-04-2024)
- 从portainer/portainer更新到最新版本 (更改日志：https://github.com/portainer/portainer/releases)

### 2.20.0 (2024-03-25)

- 从 portainer/portainer 更新到最新版本

### 2.19.4-3 (2023-11-12)

- 首次推出
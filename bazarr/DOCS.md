# Bazarr NAS

## 简介

Bazarr 用于与 Sonarr、Radarr 联动，自动下载和管理字幕。

## 访问方式

- 侧边栏 Ingress
- 端口 `6767`

## 主要配置

- `PGID` / `PUID`：容器读写权限
- `TZ`：时区
- `connection_mode`：连接模式
- `localdisks`：挂载本地磁盘
- `networkdisks`：挂载 SMB 共享
- `cifsusername` / `cifspassword` / `cifsdomain`：SMB 凭据
- `env_vars`：附加环境变量

## 连接模式

- `ingress_noauth`：Ingress 开启，应用认证关闭
- `noingress_auth`：Ingress 关闭，应用认证开启
- `ingress_auth`：Ingress 和应用认证均开启

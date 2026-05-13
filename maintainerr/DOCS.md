# Maintainerr 插件文档

## 描述
基于规则的媒体清理工具，适用于 Plex、Jellyfin 和 Emby。可创建媒体库集合并选择性删除未观看的内容。

## 安装
1. 添加仓库：https://github.com/alexbelgium/hassio-addons
2. 从 Home Assistant 插件商店安装 "Maintainerr"

## 配置
- **网页界面**：访问 `http://[home-assistant-ip]:6246`
- **时区**：通过 `TZ` 环境变量设置（默认：`Europe/London`）
- **环境变量**：可在 `env_vars` 中添加自定义变量
- **设备访问**：需要访问媒体设备（视频、存储等）
- **数据存储**：配置和数据存储在 `/config` 目录

## 使用方法
1. 在 `http://[your-server-ip]:6246` 打开网页界面
2. 为您的媒体库配置清理规则
3. 设置定时任务或手动触发清理
4. 审核并确认删除未观看内容的操作

## 故障排除
- **网页界面无法加载**：确保端口 6246 已正确映射并可访问
- **设备访问问题**：验证所需设备是否正确暴露给容器
- **存储错误**：检查 `/config` 卷权限和可用空间

## 支持
如需更多帮助或报告问题，请访问 [官方 GitHub 仓库](https://github.com/alexbelgium/hassio-addons/tree/master/maintainerr)
# BleachWRT Plus

适用于旁路由管理的 Home Assistant 加载项，提供完整的旁路由功能和 Web 管理界面。

## 功能特点

- 完整的 OpenWRT 旁路由功能
- 内置 Web 管理界面
- 支持 IP 转发
- 自动网络配置
- 自动 DHCP 配置（默认禁用）
- 支持日志级别调整

## 安装方法

1. 在 Home Assistant 中添加本仓库作为自定义存储库
2. 在加载项商店中找到并安装"BleachWRT Plus"
3. 等待安装完成

## 配置选项

| 选项              | 描述                 | 默认值         |
| ----------------- | -------------------- | -------------- |
| virtual_ip        | 旁路由虚拟 IP 地址   | 192.168.68.111 |
| netmask           | 子网掩码             | 255.255.255.0  |
| gateway           | 网关地址             | 192.168.68.1   |
| enable_forwarding | 是否启用 IP 转发     | true           |
| log_level         | 日志级别(info/debug) | info           |

## 使用方法

1. 安装加载项
2. 配置虚拟 IP 和网络参数
3. 点击启动，等待约 1 分钟让服务完全启动
4. 访问 http://[虚拟 IP] 进入 Web 管理界面

默认管理员账号密码：root/password

## 常见问题

- **无法访问 Web 界面**：请检查网络配置是否正确，确保虚拟 IP 与您的网络环境匹配
- **网络连接问题**：将日志级别设置为"debug"获取更详细的诊断信息
- **DHCP 冲突**：本插件默认已禁用 DHCP 服务器功能，避免与主路由 DHCP 冲突

详细使用说明请参阅 DOCS.md 文档。

## 支持与反馈

本项目基于[openwrt](https://openwrt.mpdn.fun/?dir=lede)开发。

如有问题或建议，请在 GitHub 仓库提交 Issue。

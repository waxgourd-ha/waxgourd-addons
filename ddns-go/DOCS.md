# DDNS-GO

## 配置

### pwd

重置密码，如果为空则使用上次密码

### frequency

同步间隔时间(秒)

## 特性

- 支持Mac、Windows、Linux系统，支持ARM、x86架构

- 支持的域名服务商 阿里云 腾讯云 Dnspod Cloudflare 华为云 Callback 百度云 Porkbun GoDaddy Namecheap NameSilo Dynadot

- 支持接口/网卡/命令获取IP

- 支持以服务的方式运行

- 默认间隔300秒同步一次

- 支持同时配置多个DNS服务商

- 支持多个域名同时解析

- 支持多级域名

- 网页中配置，简单又方便，默认勾选禁止从公网访问

- 网页中方便快速查看最近50条日志

- 支持Webhook通知

- 支持TTL

- 支持部分DNS服务商传递自定义参数，实现地域解析/多IP等功能

## 使用说明

1. 安装后打开web ui（第一次设置公网无法访问，需要进入该系统关掉“禁止公网访问”）。

1. 选择DNS服务商，以阿里云为例填好相应的“AccessKey ID”和“AccessKey Secret”。

1. 填写“Domains”，例如“domain.example.com”。

1. 点击保存。

1. 去路由器将相应的端口映射到公网，访问即可。

1. 默认 用户名：admin 密码：admin1
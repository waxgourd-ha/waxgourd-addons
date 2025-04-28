# 冬瓜甄选addons：小智 AI Server 最简化版

适用于 Home Assistant 的小智 AI Server 最简化版加载项。

## 功能特点

- 基于 WebSocket 的语音识别服务
- 支持多种语音识别服务（FunASR 本地模型、豆包 ASR 在线服务、腾讯 ASR 在线服务）
- 支持大语言模型对话功能
- 自动下载模型和配置
- 支持常见架构：aarch64 和 amd64
- 使用 S6-Overlay 管理服务

## 使用方法

1. 安装加载项
2. 配置语音识别服务 (ASR) 和大语言模型 (LLM) 参数
3. 点击启动，并查看日志，等待小智客户端接入

详细使用说明请参阅 DOCS.md 文档。

## 支持与反馈

本项目基于[xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server) 开发。

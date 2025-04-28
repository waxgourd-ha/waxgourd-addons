# 冬瓜甄选addons：小智ESP32语音助手JAVA版

这是一个基于 ESP32 的语音交互助手系统，支持语音识别和播放功能，适用于智能家居控制。此插件将小智 ESP32 服务器整合为 Home Assistant 加载项，提供更简便的部署和管理方式。

## 功能特点

- **中文语音识别**：基于 VOSK 语音识别引擎，支持准确的中文语音识别
- **与 Home Assistant 集成**：完全集成到 Home Assistant 界面中，一键安装和配置
- **Web 管理界面**：提供直观的 Web 界面管理 ESP32 设备
- **内置中文语音模型**：预装中文语音识别模型，开箱即用
- **数据库自动化**：自动创建并初始化必要的数据库表结构
- **资源占用优化**：可自定义 Java 内存分配，适应不同性能的设备

## 安装方法

### 前置要求

- Home Assistant OS 或 Supervised 环境（最低版本 2023.3）
- MariaDB 插件（或外部 MySQL/MariaDB 数据库）
- 网络连接（用于初始化）

### 安装步骤

1. 在 Home Assistant 中，进入**设置** -> **加载项** -> **加载项商店**
2. 点击右上角的菜单按钮，选择**存储库**
3. 添加此仓库地址: ``
4. 点击**添加**，然后关闭存储库对话框
5. 在加载项商店中找到**小智 ESP32 语音助手**并安装

## 配置选项

| 配置项         | 默认值       | 描述                                           |
| -------------- | ------------ | ---------------------------------------------- |
| mysql_host     | core-mariadb | MySQL 数据库主机地址                           |
| mysql_port     | 3306         | MySQL 数据库端口                               |
| mysql_database | xiaozhi      | 数据库名称                                     |
| mysql_user     | xiaozhi      | 数据库用户名                                   |
| mysql_password | 123456       | 数据库密码                                     |
| java_memory    | 512m         | Java 应用内存分配，格式为 XmXg，如 512m、1g 等 |

## 使用说明

### 首次启动

1. 安装并配置 MariaDB 加载项（如果使用外部数据库则跳过此步骤）
2. 在小智 ESP32 语音助手的配置页面，设置数据库连接信息
3. 如需调整 Java 应用内存，可修改 java_memory 参数（默认 512m）
4. 点击**保存**，然后启动加载项

### 访问 Web 界面

启动加载项后，有两种方式访问 Web 管理界面：

1. 通过 Home Assistant 边栏中的**小智 ESP32**图标直接访问
2. 或访问`http://你的HomeAssistant地址:8084`

### 设备连接

在 Web 管理界面中，您可以添加和管理 ESP32 设备：

1. 进入**设备管理**页面
2. 点击**添加设备**
3. 输入设备名称、IP 地址等信息
4. 在 ESP32 设备上设置 WebSocket 服务器地址为：`ws://你的HomeAssistant地址:8091/ws/xiaozhi/v1/`

## 数据库说明

首次启动时，插件会自动：

1. 连接到配置的 MySQL/MariaDB 数据库
2. 如果指定数据库不存在，则创建数据库
3. 执行必要的 SQL 脚本初始化表结构

如果您希望手动初始化数据库，可以：

1. 使用 MySQL 客户端连接到数据库服务器
2. 创建名为"xiaozhi"（或您指定的名称）的数据库
3. 导入`/app/db/`目录下的 SQL 文件

## 内存管理

通过配置项 `java_memory` 控制分配给 Java 应用的堆内存大小，格式示例：

- `512m`（512 兆字节，适合大多数使用场景）
- `1g`（1 吉字节，适合大量设备和频繁交互场景）
- `1.5g`或更高（适合高负载场景）

**内存管理建议**：

- 默认内存分配（512MB）足够普通使用
- 对于多设备场景，建议分配 1GB 或更多内存
- 如遇内存不足问题，增加分配至 1GB 或更高

## 故障排查

如果遇到问题，请尝试以下方法：

1. **无法启动**：

   - 检查 MariaDB 服务是否正常运行
   - 确认数据库连接信息正确
   - 查看 Home Assistant 日志中是否有错误信息

2. **Web 界面无法访问**：

   - 确认端口 8084 和 8091 未被占用
   - 检查 Home Assistant 的网络设置，确保这些端口可以访问

3. **语音模型问题**：

   - 检查 `/config/models/vosk-model` 目录是否存在模型文件
   - 如果模型不存在，请手动下载并上传到该目录
   - 确保存储空间足够（至少需要 100MB 空闲空间）

4. **内存不足**：
   - 增加 java_memory 参数，分配更多内存（如从 512m 改为 1g）
   - 关闭其他不必要的加载项释放资源
   - 考虑使用性能更强的设备运行 Home Assistant

## 技术架构

本插件采用以下技术栈：

- **前端**：Vue.js + Ant Design
- **后端**：Java Spring Boot
- **语音识别**：VOSK + ONNX Runtime
- **数据库**：MySQL/MariaDB
- **容器化**：Docker + S6 Overlay

## S6 初始化系统

插件使用 S6 Overlay 作为容器初始化系统，主要初始化流程：

1. **环境变量设置**：读取 Home Assistant 配置，设置数据库连接信息等
2. **数据库初始化**：等待 MySQL 可用，创建并初始化数据库
3. **模型检查**：检查语音模型是否存在并可用
4. **Java 应用启动**：启动 Spring Boot 应用
5. **Nginx 服务**：提供静态资源服务，反向代理 API 请求

## 版权和许可

本项目基于[xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java)开发，采用 MIT 许可证。

## 参考资源

- [小智 ESP32 服务器 Java 版](https://github.com/joey-zhou/xiaozhi-esp32-server-java)
- [VOSK 语音识别系统](https://alphacephei.com/vosk/)
- [Home Assistant 开发者文档](https://developers.home-assistant.io/)
- [S6 Overlay](https://github.com/just-containers/s6-overlay)

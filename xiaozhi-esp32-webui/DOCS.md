# 小智 AI 智控台

本加载项提供小智 ESP32 语音识别服务器功能，可与 ESP32 设备配合使用实现语音识别功能。

## 安装
 1. 在 Home Assistant 的加载项商店中添加此仓库地址或复制到本地加载项目录
 1. 安装 "Redis Server" 并配置
 1. 安装 "Mysql"或"MariaDB" 并配置
 1. 安装 "小智 AI 智控台" 加载项
    
## 配置

```yaml
mysql_host: core-mariadb #MySQL/MariaDB数据库主机地址,查看方式：Home Assistant → 设置 → 加载项 → MySQL/MariaDB → 信息 → 宿主名
mysql_port: 3306 #MySQL/MariaDB数据库端口（默认: 3306）
mysql_database: xiaozhi_esp32_server #要使用的数据库名称
mysql_username: homeassistant #数据库认证用户名 
mysql_password: root #数据库认证密码 
redis_host: 0920e2ff-redis-server #Redis服务器主机地址，查看方式：Home Assistant → 设置 → 加载项 → Redis Server → 信息 → 宿主名
redis_port: 6379 #Redis服务器端口（默认: 6379）
timezone: Asia/Shanghai #设置服务器时区
```

## 使用说明

1. 启动后，点击“打开网页界面”，浏览器访问 http://homeassistant.local:8002 进入 Web 管理界面
2. 首次访问需要注册用户
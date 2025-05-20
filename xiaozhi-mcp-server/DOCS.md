# 小智 Mcp Server

## 安装
1. 安装本addons
2. 安装Mcp Server 服务器插件
3. 登录小智平台，获取Mcp接入点

## 使用说明:  
### 参数说明
1.  **小智 MCP 接入点：** 登录[小智官方]( https://xiaozhi.me/console/agents )服务器即可获取。
2.  **HA MCP SERVER 地址：** 直接安装MCP Server集成。
    * 点击此链接：[Home Assistant MCP Server 集成](https://my.home-assistant.io/redirect/config_flow_start?domain=mcp_server)直达安装
    * 或 在 Home Assistant 中，前往 **设置 > 设备和服务 > 添加集成 > Model Context Protocol Server**。
    * 默认直接确认或从列表中选择“**模型上下文协议服务器**”，并按照屏幕上的说明完成设置。
3.  **HA长效 API 令牌：** 用于授权访问你的 Home Assistant 实例。
    * 访问你的 [Home Assistant 账户配置文件设置](https://my.home-assistant.io/redirect/profile)，进入“**安全**”选项卡。
    * 创建**长期访问令牌**。
4.  **备注：** ha中的服务器地址为域写法，可以不用更改。



——————————————————————————

作者原帖：[小智AI和Ha无缝对接：官方 MCP 接入点的最佳实践](https://bbs.hassbian.com/thread-29314-1-1.html)
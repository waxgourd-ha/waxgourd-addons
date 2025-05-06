# 小智 AI 智控台

本加载项提供小智 ESP32 是智控台的docker服务，需配合其它addons一起使用，快速体验本地化小智后端服务全功能版的乐趣。

## 安装方法与次序
 1. 在加载项仓库中，另外安装配套的addons

    mariadb（在core仓库中，HA官方自带）

    redis server（在冬瓜甄选仓库中）

    小智AI server最简安装版（在冬瓜甄选仓库中）

 1. "Redis Server" 直接启动

    无需任何操作

 1. 配置"MariaDB" 并启动

    （1）在“Databases”里增加下面内容，然后回车

    ```
    xiaozhi_esp32_server
    ```

    （2）在“Logins”修改数据库密码为root，省事可用下面一行直接替换第一行

    ```
    - password: root
    ```

    （3）在“Rights”最后增加以下内容

    ```
    - database: xiaozhi_esp32_server
      username: homeassistant
    ```

    （4）保存后启动

 1. "小智 AI 智控台" （本addons）直接启动

    因为本文档开始，直接默认设置了mariadb的密码为root。redis的服务器直接设置为“冬瓜甄选仓库”中的redis服务器名。所以直接启动就行。

    （1）自己注册一个管理员并登录

    （2）进入后，点击上方的“参数管理”，复制第一行开头为“server.secret”里的“参数值”里的字符串

    （3）模型配置——配置大语音模型（建议豆包）

    （4）模型配置——配置语音合成（建议豆包）

    （5）模型配置——配置语音识别（建议豆包）

    （6）模型配置——配置意图识别（需要控制HA的话，选最后一项“Intent_function_call”，设置为"默认"）

    - 然后点击“修改”，在“函数列表”的最后面，加上以下的字符后，保存。

    ```
    ;hass_get_state;hass_set_state
    ```

1. 配置 "小智 AI Server最简安装版"

   （1）先启动一次，等默认配置生成，然后停止。

   （2）使用filebrowser等方式，修改“小智AI Server最简安装版”的，在“addon_configs”目录——“7eca76cc_xiaozhi_esp32_server”目录——“data”目录——编辑“.config.yaml”文件

   -  把http://127.0.0.1:8002/xiaozhi那一行替换成

   ```
    url: http://homeassistant.local:8002/xiaozhi
   ```

   - 把刚才复制的“server.secret”，放到最后一行替换掉，注意空格要留好。

   （3）启动“小智 AI Server最简安装版”服务。

 1. 配置"小智 AI 智控台"接口等

    上续操作等，己经能正常启动了。但是智控台中“参数管理”中

    - server.websocket

    ```
    ws://homeassistant.local:8000/xiaozhi/v1/
    ```

    

    关键己说明，可以直接开始使用，细节配置大家看一下官方的说明
## 备用的技术参考配置（可忽略）

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

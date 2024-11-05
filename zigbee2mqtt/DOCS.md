# Zigbee2MQTT 

## 配置说明

### mqtt

- 如果不使用mosquito to broker插件，请填写MQTT详细信息(使用mosquito to broker插件时可不填写)。格式可参考下面的实例

```
server: mqtt://localhost:1883
user: Mqtt的账号
password: "Mqtt的密码"
```

注意:如果密码包含某些特殊字符(由yaml规范保留)，则需要加上引号。所以我们建议如果日志显示密码错误时，优先考虑加上引号。

### serial

- 填写串口详细信息(例如USB协调器的端口)。格式可参考下面的实例

```
port: /dev/ttyUSB0
```

如果您不知道详细的端口，并且只有一个USB设备连接到您的机器，请尝试/dev/ ttyUSB0。否则，请查看“配置 - 系统 - 硬件 - 全部硬件”，在搜索上输入“tty”查看。

## 使用方法

- 点击启动（启动时长大约一分钟），进入日志页面中点击刷新，出现“Zigbee2MQTT started!”则表示启动成功。

- 启动完成后可在信息页中点击"打开 WEI UI"，或点击“在侧边栏显示”，方便以后从左侧栏快速访问。
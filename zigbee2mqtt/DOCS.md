# Zigbee2MQTT 

## 配置说明

### mqtt

- 如果不使用mosquito to broker插件，请填写MQTT详细信息(使用mosquito to broker插件时可不填写)。格式可参考下面的实例

```
server: mqtt://localhost:1883
user: mqtt
password: "123456"
```

注意:如果密码包含某些特殊字符(由yaml规范保留)，则需要加上引号。所以我们建议如果日志显示密码错误时，优先考虑加上引号。

### serial
- 端口

填写串口详细信息(例如USB协调器的端口)。格式可参考下面的实例

**USB协调器**

```
port: /dev/ttyUSB0
```

 如果您不知道详细的端口，并且只有一个USB设备连接到您的机器，请尝试/dev/ ttyUSB0。否则，请查看“配置 - 系统 - 硬件 - 全部硬件”，在搜索上输入“tty”查看。

**网络版协调器**(xzg固件示例)

```
port: tcp://xzg.local:6638
```

查看适配器的ip地址



**注意！！！**

从2.0.0开始，zigbee2mqtt引入了新的配置规则，要求必须填写适配器信息。



- 适配器

适配器的类型配置，常见的

TI的芯片（Texa Instrument）：zstack

 芯科（Silicon）：ember

还可能是deconz，zigate或者zboss。



-  示例

serial：

```
port: /dev/ttyUSB0
adapter: zstack
```
```
port: tcp://xzg.local:6638
adapter: zstack
```


```
port: /dev/ttyUSB0
adapter: ember
```




详细信息：可查看官网：https://www.zigbee2mqtt.io/guide/configuration/adapter-settings.html#basic-configuration



## 使用方法

- 点击启动（启动时长大约一分钟），进入日志页面中点击刷新，出现“Zigbee2MQTT started!”则表示启动成功。

- 启动完成后可在信息页中点击"打开 网页界面"，或点击“在侧边栏显示”，方便以后从左侧栏快速访问。

## 自定义转换器
如果 Z2M Addons 官方显示不支持你的设备，别慌，可以自定义转换器，操作如下：
先打开调试模式，能查看到更多调试信息：使用 FileBroswer 打开 homeassistant/zigbee2mqtt/configuration.yaml 文件，
并添加或修改log_level: debug

#### 第一步：打开zigbee2mqtt，点击开发控制台，找到 JS 代码，复制并保存到本地，命名为 **[ 设备型号 ].js** （此处将 **[ 设备型号 ]** 替换为你真实的设备信息）；

如果这里的js没有生成有效文件或者生成的文件在调试过程中没有很好的效果，需要从官方已经存在的转换器（https://github.com/Koenkk/zigbee-herdsman-converters）查找相关设备类型的代码，多次修改调试验证。

#### 第二步：将 **[ 设备型号 ].js** 通过 FileBroswer 拖拽上传到目标目录
```homeassistant/zigbee2mqtt/external_converters```

zigbee2mqtt 2.0.0 之后的版本文件存放位置（**如果没有external_converters 这个文件夹，请手动创建** ）

简单参考一个js：
```python3
const {} = require('zigbee-herdsman-converters/lib/modernExtend');
const fz = require('zigbee-herdsman-converters/converters/fromZigbee');
const exposes = require('zigbee-herdsman-converters/lib/exposes');
const reporting = require('zigbee-herdsman-converters/lib/reporting');
const e = exposes.presets;
const definition = {
    zigbeeModel: ['FNB56-ZRC06FB2.0'],
    model: 'NZRC106W-M2',
    vendor: 'Feibit',
    description: 'Security controller',
    extend: [],
    fromZigbee: [fz.command_arm, fz.battery],
    toZigbee: [],
    exposes: [e.battery(), e.action(['panic', 'disarm', 'arm_day_zones', 'arm_all_zones'])],
    configure: async (device, coordinatorEndpoint) => {
    const endpoint = device.getEndpoint(1);
    await reporting.bind(endpoint, coordinatorEndpoint, ['genBasic']);
    },
    onEvent: async (_, data) => {
    if (data.type === 'commandArm' && data.cluster === 'ssIasAce') {
    await data.endpoint.defaultResponse(0, 0, 1281, data.meta.zclTransactionSequenceNumber);
    }
    },
};

module.exports = definition;
```


#### 第三步：点击 “允许添加新设备”，等待设备连接完成就好了，然后就是测试功能。

验证过程：

- 查看 z2m 界面新加入的设备是否已经不显示 不支持了，如果还显示，说明匹配失败或 JS 文件有问题。

- 重启 z2m 加载项，点击 日志，ctrl+F，搜索步骤二中添加的 JS 文件名，出现 Load xxx.js ，并下面没有出现 error 相关字样，表示成功加载且 JS 内容正确。
然后 在日志中查看 MQ 消息，验证设备发送和接收的消息的正确性是否符合预期。如果不满意效果，就需要调整 JS 内容并重启 z2m 加载项，查看日志，重复此过程达到满意即可。



- 如果确定 JS 没问题，但设备还是没有接入成功或者设备按钮效果不符合预期，可能是设备固件需要升级或者固件本身和 z2m 兼容性不好。咨询设备厂商或客服烧录最新固件，再次调试。

接入完成之后，关闭调试，减少日志输出提高 z2m 性能，```log_level: debug``` 改为 ```log_level: info```


### 参考：

官方接入自定义设备参考

https://www.zigbee2mqtt.io/advanced/support-new-devices/01_support_new_devices.html#_2-3-using-modern-extend

升级到 2.0.0+的说明

https://github.com/Koenkk/zigbee2mqtt/discussions/24198

### 如果需要贡献给官方，步骤如下：

- fork 官方转换器仓库，https://github.com/Koenkk/zigbee-herdsman-converters

- clone 你 fork 的仓库

- 找到你设备对应的文件，比如：src/devices/feibit.ts

- 将你测试通过的 JS 代码按照格式添加到官方文件中，根据官方 README 按照步骤操作，提交到你 fork 的仓库，注意提交的 message 按照如下格式：feat(add): xxxx(新的设备型号)，更多请参考官方历史提交日志记录

- 然后提交 PR，等待官方审核，等待审核同时准备好设备照片：512*512 背景透明

- 同样 fork 官方平台仓库：https://github.com/Koenkk/zigbee2mqtt.io

- clone 你 fork 的仓库

- 在位置public/images/devices添加你的设备图片，提交到你 fork 仓库，提交 PR，等待审核
# KNXD daemon

## 安装

按照以下步骤在您的系统上安装插件:

 1. 在您的家庭助理前端导航到**主管**->**插件商店**。

 1. 如果您还没有将此附加存储库添加到您的主管，请单击右上角的菜单图标，选择**存储库**，添加`https://github.com/da-anda/hass-io-addons` 作为新存储库，然后再次关闭对话框。

 1. 找到“KNXD”插件并单击它。

 1. 点击“安装”按钮。

## 配置

附加组件配置：

```yaml
    "address": "0.0.1",
    "client_address": "0.0.2:8",
    "interface": "tpuart",
    "device": "/dev/ttyACM0",
    "usb_filters": "",
    "custom_config": ""
```

### 选项:
这些选项的描述部分复制自“knxd”[文档][documentation](https://githubcom/knxd/knxd/blob/master/doc/inifile.rst)。
您将在那里找到更多示例和详细信息。

#### 选项: `address`

knxd deamon本身的KNX地址。例如，用于源自组缓存的请求。

#### 选项: `client_address`

要分配给客户端连接的地址范围。请注意，长度参数表示要分配的地址数量。

例如: 1.2.3:5 (示例：1.2.3:5（这将地址1.2.3到1.2.7分配给knxd的客户端。）)

#### 选项: `interface`

驱动程序“knxd”应用作与KNX总线通信的接口。此插件的典型用例中最常见的是：

- `tpuart` (用于基于UART的KNX接口，如Busware.de中的接口)
- `usb` (用于商用USB KNX接口)

有关所有可能选项的完整列表，请参阅knxd文档的驱动程序部分。

#### 选项: `device` (某些接口可选)

nux中适配器的物理设备地址。例子：:

- **TPUART interface**: `/dev/ttyACM0` ### 物理设备地址 ; 实体装置位址
- **USB interface**: 可以尝试将此留空，以便`knxd`自动检测您的设备。如果空白时不起作用，请尝试指定一个设备地址，如“/dev/ttyAMA0”。

请注意，这些地址仅为示例，可能因您的设备而异。要找出设备地址，您必须通过SSH连接到主机操作系统（**不是**主管！），并检查连接到那里的设备。

#### 选项: `usb_filters` (optional)

使用USB接口时，您可以指定要使用的其他过滤器。请参阅[过滤器部分](https://github.com/knxd/knxd/blob/master/doc/inifile.rst#filters) 官方“knxd”文件。

#### 选项: `custom_config` (optional)

允许您编写自己的自定义“knxd”ini配置，而不是使用此插件中准备好的模板，该模板使用了上述所有其他配置选项。

您的自定义配置将替换此插件提供的默认配置，因此上述所有其他配置选项都将被忽略。请参阅[knxd文档](https://github.com/knxd/knxd/blob/master/doc/inifile.rst)对于所有可能的配置选项。


## 支持

如果您有任何问题，请随时加入HomeAssistant社区，并在[附加线程]中提问(https://community.home-assistant.io/t/knxd插件将knx usb接口转换为ha/38108/38可以使用的ip接口).

如果你发现了一个bug，请随时在 [Github](https://github.com/da-anda/hass-io-addons/issues)
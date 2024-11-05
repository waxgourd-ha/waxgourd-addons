# 小米体脂称

## 支持的电子秤

支持类型:
Name | Model | Picture
--- | --- | ---
[Mi Smart Scale 2](https://www.mi.com/global/scale) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | XMTZC04HM | <img alt="Mi Scale_2" src="https://raw.githubusercontent.com/lolouk44/xiaomi_mi_scale/master/Screenshots/Mi_Smart_Scale_2_Thumb.png" width="150">
[Mi Body Composition Scale](https://www.mi.com/global/mi-body-composition-scale/) | XMTZC02HM | <img alt="Mi Scale" src="https://raw.githubusercontent.com/lolouk44/xiaomi_mi_scale/master/Screenshots/Mi_Body_Composition_Scale_Thumb.png" width="150">
[Mi Body Composition Scale 2](https://c.mi.com/thread-2289389-1-0.html) | XMTZC05HM | <img alt="Mi Body Composition Scale 2" src="https://raw.githubusercontent.com/lolouk44/xiaomi_mi_scale/master/Screenshots/Mi_Body_Composition_Scale_2_Thumb.png" width="150">

## 配置说明
配置项 | 类型 | 必填项 | 说明
--- | --- | --- | ---
HCI_DEV | string | 否 | 蓝牙地址。默认为 `hci0` 
BLUEPY_PASSIVE_SCAN | bool | 否 | 如果像在 Raspberry Pi 上出现错误 `Bluetooth connection error: Failed to execute management command ‘le on’` ，请尝试设置为 true。默认为  `false` 
MISCALE_MAC | string | 是 | 秤的 MAC 地址 
MQTT_PREFIX | string | 否 | MQTT 主题前缀，默认为`miscale` 
MQTT_HOST | string | 是 | MQTT 服务器，默认为`127.0.0.1` 
MQTT_USERNAME | string | 否 | MQTT 服务器的用户名（如果不需要，则注释掉） 
MQTT_PASSWORD | string | 否 | MQTT 服务器的密码（如果不需要，则注释掉） 
MQTT_PORT | int | 否 | MQTT 服务器的端口，默认为 1883 
MQTT_DISCOVERY | bool | 否 | 是否要 Home Assistant 的 MQTT 发现，默认为 `true` 
MQTT_DISCOVERY_PREFIX | string | 否 | Home Assistant 的 MQTT 发现前缀，默认为 `homeassistant` 
DEBUG_LEVEL | string | 否 | 日志记录级别。可能的值：`CRITICAL`、`ERROR`、`WARNING`、`INFO`、`DEBUG`，默认为`INFO` 
USERS | List | 是 | 要添加的用户列表，请参见下文 


自动性别选择/配置：用于创建计算，例如 BMI、水/骨量等。以下是用于为用户分配测量权重的逻辑：
- 如果权重在用户定义的 GT 和 LT 值范围内，则会将其分配（发布）给该用户。
- 如果权重与两个单独的用户范围匹配，则只会将其分配给匹配的第一个用户。所以不要创建重叠的范围！

用户选项 | 类型 | 必填项 | 说明 
--- | --- | --- | ---
GT | int | 是 | 大于 - 权重必须大于此值;这将是用户体重范围的下限 
LT | int | 是 | 小于 - 重量必须小于此值;这将是用户体重范围的上限 
SEX | string | 是 | 用户的性别（男/女） 
NAME | string | 是 | 用户名称 
HEIGHT | int | 是 | 用户的身高（厘米） 
DOB | string | 是 | 用户的出生日期（格式 yyyy-mm-dd ） 

注意：重量定义必须与体重秤的单位相同（kg、Lbs 或 jin）。


## configuration.yaml配置
在块中 `mqtt:` ，输入与环境变量中配置的用户数一样多的块。如果您已经有一个 `mqtt:` and/or `sensor:` 块，请不要创建另一个块，而只需在相关块头下添加“缺失”位。注意：只有权重实体才会通过 MQTT 发现自动添加。


```yaml
mqtt:
  sensor:
    - name: "Example Name Weight"
      state_topic: "miscale/USER_NAME/weight"
      value_template: "{{ value_json['weight'] }}"
      unit_of_measurement: "kg"
      json_attributes_topic: "miscale/USER_NAME/weight"
      icon: mdi:scale-bathroom
      # Below lines only needed if long term statistics are required
      state_class: "measurement"

    - name: "Example Name BMI"
      state_topic: "miscale/USER_NAME/weight"
      value_template: "{{ value_json['bmi'] }}"
      icon: mdi:human-pregnant
      unit_of_measurement: "kg/m2"
      # Below lines only needed if long term statistics are required
     state_class: "measurement"
```

<img align="center" alt="Example of the Lovelace card in HA" src="https://raw.githubusercontent.com/lolouk44/xiaomi_mi_scale/master/Screenshots/HA_Lovelace_Card.png" width="250"> 

<img align="center" alt="Example of the details of the Lovelace card in HA" src="https://raw.githubusercontent.com/lolouk44/xiaomi_mi_scale/master/Screenshots/HA_Lovelace_Card_Details.png" width="250"> 
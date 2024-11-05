# eWeLink Smart Home

---

## 疑难解答

- 解决“调用服务xxxxx/xxxxxxxx失败”的问题。找不到服务。`问题，使用“文件编辑器”编辑“configuration.yaml”。将以下信息附加到文件末尾：

```
switch:
  - platform: template
    switches:
      ewelink_virtual_switch:
        turn_on:
          service: switch.turn_on
        turn_off:
          service: switch.turn_off

cover:
  - platform: template
    covers:
      ewelink_virtual_cover:
        open_cover:
          service: cover.open_cover
        close_cover:
          service: cover.close_cover
        stop_cover:
          service: cover.stop_cover
        set_cover_position:
          service: cover.set_cover_position

fan:
  - platform: template
    fans:
      ewelink_virtual_fan:
        value_template: "{{ states('input_boolean.state') }}"
        turn_on:
          service: fan.turn_on
        turn_off:
          service: fan.turn_off
        set_preset_mode:
          service: fan.set_preset_mode

light:
  - platform: template
    lights:
      ewelink_virtual_light:
        turn_on:
          service: light.turn_on
        turn_off:
          service: light.turn_off
```
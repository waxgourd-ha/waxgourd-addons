# Cpolar

## 配置项

- Authtoken：https://dashboard.cpolar.com/auth

- 9200/tcp：9200

## 使用方法

cpolar教程：https://www.cpolar.com/docs

### 注
浏览器 **`400: Bad Request`** 错误解决方案

- 编辑配置文件：/homeassistant/configuration.yaml

追加内容：
```json
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 192.168.68.1
```

- 重启 Home Assistant Core 后生效

参考地址：https://www.cpolar.com/blog/how-to-build-a-home-assistant-smart-home-system-and-remotely-control-home-devices-through-intranet-penetration 的第5. 公网访问Home Assistant 步骤

 
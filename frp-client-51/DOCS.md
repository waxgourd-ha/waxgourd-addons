# FRP Client 0.51.0

## 配置说明

1、 按照实际情况填写相关"配置",自定义二级域名必填。

2、 用File editor修改Home Assistant `configuration.yaml` 最后一行添加：

```yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 127.0.0.1
```
3、 修改之后，重启HA
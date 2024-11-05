# WGHAOS SSH 配置器

## 使用方法

- 启动前请关闭保护模式，启动后可通过查看日志来检查是否正常启动。

- 点击“打开WebUI”进行操作。

- 将自己的公钥粘贴到对文本栏中，保存并应用即可立即生效。

  注：执行保存、删除、恢复出厂设置按钮后，需要点击“应用”按钮后才可生效

- 公钥示例：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGTlRAfhm9BIV6l6sOubRgeCY0wRhYQVfB3QBWFl2ELpeAnTHwRYY+4pSP1Nu7FuZqAzDyZkssmFkbXHJGqi6EAnAkRLsKhzvDKo5WSXfEQdl2kSN5bgU/e37GfwqG4ChEfY56gwu+tdHtt4eIrplcLjBB9Y43SFjth/Ouke+DVGaBO2LYNc8U0S4EiHT6KdRXS4iIwYjXMw6SEsT7eP9IWQObQ4ZgyG0cHO/6ArxJ0fyOcAI29sLzM9466ID0mTaJWHriTRf6Lxhpdd/S30VTG0JMTdo/Fj  root@HLAB-A17

```

   注：冬瓜为了方便开发调试，默认了两个wghaos的测试秘钥，使用时可以自行删除。
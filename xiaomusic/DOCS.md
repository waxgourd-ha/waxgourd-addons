# XiaoMusic无限听歌，解放小爱音箱

## 👋 配置说明

```yaml
song_media: music2 #<选>Media可存放音乐目录/media下,请手动填写自定义目录
song_share: music3 #<选>Share可存放音乐目录/share下,请手动填写自定义目录
song_download: download #<选>Download下载音乐目录/media下,请手动填写自定义目录
```

## 🔩 安装说明

加载项一键安装和更新

> 端口：58090  # 8090/tcp: 58090
>
> 访问：[PROTO:http]://[HOST]:[PORT:58090]/ 例如：192.168.68.123:58090/


## 🛠️ 已测试支持的设备

| 型号   | 名称                                                                                             |
| ---- | ---------------------------------------------------------------------------------------------- |
| L06A | [小爱音箱](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.l06a)             |
| L07A | [Redmi小爱音箱 Play](https://home.mi.com/webapp/content/baike/product/index.html?model=xiaomi.wifispeaker.l7a)                     |
| S12/S12A/MDZ-25-DA | [小米AI音箱](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.s12)            |
| LX5A | [小爱音箱 万能遥控版](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.lx5a)       |
| LX05 | [小爱音箱Play（2019款）](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.lx05)  |
| L15A | [小米AI音箱（第二代）](https://home.mi.com/webapp/content/baike/product/index.html?model=xiaomi.wifispeaker.l15a#/) |
| L16A | [Xiaomi Sound](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.l16a)     |
| L17A | [Xiaomi Sound Pro](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.l17a) |
| LX06 | [小爱音箱Pro](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.lx06)          |
| LX01 | [小爱音箱mini](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.lx01)         |
| L05B | [小爱音箱Play](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.l05b)         |
| L05C | [小米小爱音箱Play 增强版](https://home.mi.com/baike/index.html#/detail?model=xiaomi.wifispeaker.l05c)   |
| L09A | [小米音箱Art](https://home.mi.com/webapp/content/baike/product/index.html?model=xiaomi.wifispeaker.l09a) |
| LX04 X10A X08A | 已经支持的触屏版 |
| X08C X08E X8F | 需要设置【型号兼容模式】选项为 true |
| M01/XMYX01JY | 小米小爱音箱HD 需要设置【特殊型号获取对话记录】选项为 true 才能语音播放|

型号与产品名称对照可以在这里查询 <https://home.miot-spec.com/s/xiaomi.wifispeaker>

> 如果你的设备支持播放，请反馈给我添加到支持列表里，谢谢。
> 目前应该所有设备类型都已经支持播放，有问题随时反馈。
> 其他触屏版不能播放可以设置【型号兼容模式】选项为 true 试试。

## 🎵 支持音乐格式
<Hr>

 - mp3
 - flac
 - wav
 - ape
 - ogg
 - m4a

> 本地音乐会搜索目录下上面格式的文件，下载的歌曲是 mp3 格式的。
> 已知 L05B L05C LX06 L16A 不支持 flac 格式。
> 如果格式不能播放可以打开【转换为MP3】和【型号兼容模式】选项。

## 🌏 网络歌单功能

  可以配置一个 json 格式的歌单，支持电台和歌曲，也可以直接用别人分享的链接，同时配备了 m3u 文件格式转换工具，可以很方便的把 m3u 电台文件转换成网络歌单格式的 json 文件，具体用法见


## ⚠️ 安全提醒

1. 如果配置了公网访问 xiaomusic ，请一定要开启密码登陆，并设置复杂的密码。且不要在公共场所的 WiFi 环境下使用，否则可能造成小米账号密码泄露。
1. 强烈不建议将小爱音箱的小米账号绑定摄像头，代码难免会有 bug ，一旦小米账号密码泄露，可能监控录像也会泄露。

## 🤔 高级篇
- 自定义口令功能 [105](https://github.com/hanxi/xiaomusic/issues/105)
- 缺少一篇教程 如何写自定义插件[如何写自定义插件](https://github.com/hanxi/xiaomusic/issues/105)
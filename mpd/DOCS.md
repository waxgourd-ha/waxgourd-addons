# MPD

## 配置说明：

- 下面是插件作者的建议：

```yaml
media_folder: /media/mpd/media
playlist_folder: /media/mpd/playlists
volume_normalization: false
httpd_output: false
```

### 音量标准化

- 启用内置的音量标准化功能。

### httpd输出 

- 启用 httpd 音频输出。

### 媒体文件夹

- 此选项允许你指定自定义媒体文件夹。

### 播放列表文件夹

- 此选项允许你指定自定义播放列表文件夹。

### 详细 (可选项)

- `MPD` 详细日志参数。

### 自定义配置 (可选项)

**如果指定此选项，则忽略所有其他选项。**

- 此选项允许你为 MPD 指定自定义配置文件。
- 为了将所有 MPD 文件保存在一个位置，己将路径前缀限制为“/share/MPD ”。
- 请使用插件的默认 [MPD.conf](https://github.com/poeschl/hassio-addons/blob/main/mpd/root/etc/mpd.conf )作为参考。
- 如果你的配置有问题，请查阅官方文档[MPD Docs](https://www.musicpd.org/doc/html/user.html#configuration)，找解决方法。

## 故障排除

```
RTIOThread could not get realtime scheduling, continuing anyway: sched_setscheduler
```

A：此错误显示在任何非 glibc 系统（如 Alpine Linux）上。MPD 应该在没有它的情况下工作。
更多请看这里： [MPD Issue](https://github.com/MusicPlayerDaemon/MPD/issues/218)

```
Failed to open '/data/database/mpd.db': No such file or directory
```

A：当数据库不存在时，此错误在第一次启动时显示。它将在第二次运行时出现。

## 作者提醒

要从HA连接，请使用以下配置：

```yaml
media_player:
  - platform: mpd
    host: 243ffc37-mpd
    port: 6600
```
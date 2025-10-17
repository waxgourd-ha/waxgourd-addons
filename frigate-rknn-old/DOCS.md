# Frigate-rknpu-old版
配置参考：[https://docs.frigate.video/configuration/reference](https://docs.frigate.video/configuration/reference)

## 使用方法:  
- 方法一：直接启动，启动完成之后，点击`打开webui`，点击`config`，进行编辑之后，点击`Save Only`，然后再重启本应用
- 方法二：使用 Filebrowser 编辑`homeassistant/frigate.yaml`，然后启动本应用
- 方法三：进入 [ip]:7681 导航到`/mnt/data/supervisor/homeassistant/`，使用命令行工具编辑`frigate.yaml`，然后启动本应用

`frigate.ayml`默认内容

```yaml
mqtt:
  enabled: false  # 如果要用请修改成 true
  host: core-mosquitto
  port: 1883
  client_id: gzbdi3
  #topic_prefix: frigate
  user: ''        # 改成mqtt登录账号
  password: ''    # 改成mqtt登录密码

ffmpeg:
  input_args: preset-rtsp-restream
  hwaccel_args: preset-rk-h264
  output_args:
    record: preset-record-generic-audio-aac

cameras:
  video:  # 多路视频，请从此复制
    ffmpeg:
      inputs:
        - path: ''    # 填写你的rtsp视频流地址，比如：rtsp://username:password@192.168.1.100:554/Streaming/Channels/101
          input_args: preset-rtsp-restream
          roles:
            - detect

detectors:
  rk-detector:
    type: rknn

model:
  width: 320
  height: 320
  input_tensor: nhwc
  input_pixel_format: bgr

detect:
  width: 1280
  height: 720
  fps: 6
  enabled: True

objects:
  track:
    - person
  filters:
    person:
      min_score: 0.2

snapshots:
  enabled: true
  bounding_box: true
  clean_copy: true
  retain:
    default: 15

record:
  enabled: True
  expire_interval: 60
  retain:
    days: 0
    mode: active_objects
  events:
    pre_capture: 2
    post_capture: 3
    objects:
      - person
    required_zones: [ ]
    retain:
      default: 2
      mode: active_objects
      objects:
        person: 15

logger:
  default: info
  logs:
    frigate.event: debug
    frigate.mqtt: debug
    detect: debug
```

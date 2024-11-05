# Frigate-rknpu版

## 准备工作

1、确保系统为启用RKNN功能的冬瓜版HAOS 12.3或以上版本。

​      包含机型：

- Green（支持RKNN功能的硬件代号为ngreen）
- panther-x2(从12.3开始为默认开启RKNN，直接升级即可)
- X88pro20（从OS12.3开始，默认开启RKNN，硬件代号x88pro20）

2、目前仅支持瑞芯微RK3566及以上CPU（支持RKNN功能的）。

   注：此版本只测过冬瓜HAOS下使用，其它未测试过。

3、确认摄像头支持rtsp。



## 使用方法

1、进入冬瓜版HAOS >  配置 > 加载项 > 加载项商店 > Add-ons by waxgourd，安装**frigate-rknpu**（容量较大，请耐心等待）。

2、**frigate-rknpu**的信息页面中关闭**保护模式**并**启动**。

3、正常启动则可以在**信息**页面中**打开 WEB UI**。

4、进入**FRIGATE**内找到**CONFIG**，按照注释更改信息。

a、如果不需要开启`mqtt`则不需要更改该配置。如安装的是**mosquitto**，只需要将`enabled`改为`true`，填写mosquitto设置的用户名和密码即可。

b、找到`cameras`下的`path`配置项，将后面的地址改为你摄像头的地址。多摄像添加格式按照提示进行配置，建议不要超过四个。太多会影响HA的性能。

​	格式：rtsp://{账号}:{密码}@{IP地址}:554/Streaming/Channels/{通道号}

​	例如：rtsp://rtsp:123456@192.168.68.148:554/Streaming/Channels/101

5、编辑完成后点击**SAVE & RESTART**保存并重启。注：他自己不能重启，只能进入页面再次点击**启动**。再次进入则可以看到图像了。



## 其他技巧

### 1、人体识别存储保留周期

a、在**Config**中找到**record** > **events** > **retain** > **objects** > **person**，**person**的值就是触发报警后的存储周期，默认为15天。



解锁更多玩法请查看[官方网站](https://docs.frigate.video/)
# 小智 AI Server 极速版

本加载项提供虾哥小智AI音箱的HA本地服务器功能，让大家简单玩转AI语音设备控制。 

## 安装

1. 安装"小智 AI Server 极速版"加载项
3. 配置加载项

## 使用说明（快速入门）

使用之前先做如下的准备：

1. 更换成小智AI音箱（HA专用固件）

   （1）烧录专用固件，固件烧录地址：https://xzfw.wghaos.com/

   （2）配置网络

2. 火山引擎

   （1）注册并认证火山引擎：https://www.volcengine.com/

   （2）LLM（大语言模型服务）模型名称及API密钥的获取：

   - 打开以下网址，开通的服务搜索Doubao-pro-32k，开通它

     开通改地址：https://console.volcengine.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&OpenTokenDrawer=false

   - 免费额度500000token

   - 开通后，进入这里获取密钥：https://console.volcengine.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D

   （3）TTS（文本转语音）和语音识别模型（ASR）的语音识别APPID和语音合成令牌的获取：

   注：TTS和ASR可以使用同一个。

   - 在后面链接申请相关Key等信息，https://console.volcengine.com/speech/app
   - 填写相应的appid和access_token
   - 语音合成音色，可以填"BV001_streaming"

3. 填写homeassistant令牌

   点击左下角的用户头像，选择**安全**，向下滚动到长期访问令牌部分，点击创建令牌，生成后复制并保存（关闭后无法再次查看）

4. 启动体验



### 支持

详细错做说明，请查看www.wghaos.com或者https://bbs.hassbian.com查看

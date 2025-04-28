# 小智 AI Server 最简化版

本加载项提供小智 ESP32 语音识别服务器功能，可与 ESP32 设备配合使用实现语音识别功能。

## 安装

1. 在 Home Assistant 的加载项商店中添加此仓库地址或复制到本地加载项目录
2. 安装"小智 AI Server 最简化版"加载项
3. 配置加载项

## 配置参数

| 参数                                 | 描述                              |
| ------------------------------------ | --------------------------------- |
| timezone                             | 时区设置                          |
| server.auth.enabled                  | 是否启用设备认证（可选）          |
| server.auth.tokens                   | 设备认证令牌列表（可选）          |
| log_level                            | 日志级别 (INFO/DEBUG)             |
| llm.type                             | 大语言模型类型                    |
| model_name                           | 大语言模型名称                    |
| llm.api_key                          | 大语言模型 API 密钥               |
| tts.type                             | 语音合成服务类型                  |
| tts.appid                            | TTS 服务应用 ID (DoubaoTTS 需要)  |
| tts.access_token                     | TTS 服务访问令牌 (DoubaoTTS 需要) |
| tts.voice                            | TTS 音色 (DoubaoTTS 可选)         |
| asr.type                             | 语音识别服务类型                  |
| asr.appid                            | ASR 服务应用 ID（在线服务需要）   |
| asr.access_token                     | ASR 服务访问令牌（在线服务需要）  |
| asr.secret_key                       | ASR 服务密钥（腾讯 ASR 需要）     |
| plugins.get_weather.api_key          | 和风天气 API 密钥                 |
| plugins.get_weather.default_location | 默认天气查询位置                  |
| plugins.home_assistant.base_url      | Home Assistant 地址               |
| plugins.home_assistant.api_key       | Home Assistant 长期访问令牌       |
| plugins.home_assistant.devices       | Home Assistant 设备列表           |

## 使用说明

安装并启动后，服务器会在 8000 端口启动 WebSocket 服务。您可以通过 ESP32 设备连接到此服务进行语音识别。

### 配置方式说明

本加载项支持两种配置方式：

1. **通过 Home Assistant 加载项页面配置**：在 Home Assistant -> 设置 -> 加载项 -> 小智 AI Server 最简化版 中配置基本参数

   - 这些配置会自动应用到服务器的.config.yaml 文件中
   - 每次重启加载项时，Home Assistant 配置会自动覆盖相应的.config.yaml 设置

2. **手动编辑配置文件**：
   - 配置文件位于: `/config/data/.config.yaml`（通过文件编辑器访问）
   - 适合进行高级配置调整，如不在加载项页面提供的参数

**注意**：所有需要的 ASR 和 LLM 参数都应当在 Home Assistant 加载项配置页面中设置，这是推荐的配置方法。修改后需要重启加载项才能生效。

### 具体配置路径

1. **加载项配置页面**:

   - Home Assistant → 设置 → 加载项 → 小智 AI Server 极速版 → 配置
   - 在此页面可以设置所有主要参数，包括 ASR 类型、appid、access_token、LLM 类型、model_name 和 api_key 等

2. **通过文件编辑器**:
   - Home Assistant → 设置 → 加载项 → 文件编辑器
   - 导航到 `/config/data/.config.yaml` (加载项配置文件)
   - 此文件包含更详细的配置，但每次重启加载项后会被加载项配置页面的设置覆盖

### 模型文件

使用 FunASR 模型时，需要使用 SenseVoiceSmall 模型文件才能正常工作。系统会自动下载模型文件并放置在以下位置：

```
/config/models/SenseVoiceSmall/model.pt
```

如果自动下载失败，您需要手动下载并放置模型文件。

### 语音识别服务 (ASR)

本插件支持以下语音识别服务：

1. **FunASR**：本地语音识别模型，需要下载模型文件。无需配置 API 密钥。
2. **DoubaoASR**：豆包 ASR 服务，需要配置 appid 和 access_token。
3. **TencentASR**：腾讯云 ASR 服务，需要配置 appid、access_token 和 secret_key。

**注意**：如果您选择 DoubaoASR 或 TencentASR，但未提供完整的配置信息，系统将无法启动相应服务。请确保提供所有必要的参数。

### 大语言模型服务 (LLM)

本插件支持以下大语言模型服务：

1. **DoubaoLLM**：豆包大语言模型服务
2. **ChatGLMLLM**：智谱 AI 大语言模型服务
3. **DeepSeekLLM**：DeepSeek 大语言模型服务

每种 LLM 服务都需要配置相应的 model_name 和 api_key。

### 如何获取各服务的配置信息

#### DoubaoASR (豆包语音识别)

- **获取地址**: [火山引擎语音服务](https://console.volcengine.com/speech/app)
- **appid**: 申请开通火山引擎语音合成服务后获取的 appid
- **access_token**: 开通后获取的访问令牌

#### TencentASR (腾讯云语音识别)

- **密钥申请**: [获取密钥](https://console.cloud.tencent.com/cam/capi)
- **免费资源**: [领取免费资源](https://console.cloud.tencent.com/asr/resourcebundle)
- **appid**: 腾讯云语音识别服务应用 ID
- **secret_id**: 获取的腾讯云语音识别 SecretID
- **secret_key**: 获取的腾讯云语音识别 SecretKey

#### DoubaoLLM (豆包大语言模型)

- **开通地址**: [开通服务](https://console.volcengine.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&OpenTokenDrawer=false)
- **获取密钥**: 开通后，进入[这里](https://console.volcengine.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D)获取
- **适用模型**: 推荐模型名 `doubao-pro-32k-functioncall-241028`
- **免费额度**: 开通后提供 500000 token 的免费额度

#### ChatGLMLLM (智谱 AI 大语言模型)

- **获取密钥**: [智谱 AI 平台](https://bigmodel.cn/usercenter/proj-mgmt/apikeys)
- **推荐模型**: `glm-4-flash` (免费模型，但需要注册并填写 API 密钥)
- **API 访问**: 模型通过 `https://open.bigmodel.cn/api/paas/v4/` 接口访问

#### DeepSeekLLM (DeepSeek 大语言模型)

- **获取密钥**: [DeepSeek 平台](https://platform.deepseek.com/)
- **模型名称**: 如 `deepseek-chat`
- **访问地址**: https://api.deepseek.com

### 语音合成服务 (TTS)

本插件支持多种语音合成服务：

#### EdgeTTS (微软 Edge 浏览器 TTS)

- **无需 API 密钥**: 免费使用的本地 TTS 服务
- **默认语音**: `zh-CN-XiaoxiaoNeural`，中文女声

#### DoubaoTTS (豆包/火山引擎 TTS)

- **配置参数**: 需要设置`tts.appid`、`tts.access_token`和`tts.voice`（可选）
- **获取地址**: [火山引擎语音合成](https://console.volcengine.com/speech/service/8)
- **购买建议**: 建议购买付费服务，起步价 30 元可获得 100 并发，免费版本只有 2 个并发
- **特色音色**: 湾湾小何音色可在[此处开通](https://console.volcengine.com/speech/service/10007)
- **音色设置**: 默认使用`BV001_streaming`，湾湾小何音色设置为`zh_female_wanwanxiaohe_moon_bigtts`
- **开通说明**: 购买服务后，可能需要等待约半小时才能使用
- **验证要求**: 系统会在启动时验证 appid 和 access_token，如果缺少将无法启动

### FunASR 才会使用下面模型文件

您可以通过以下方式下载模型文件（正常情况下会自动下载）：

1. 线路一：[阿里魔塔下载 SenseVoiceSmall](https://www.modelscope.cn/models/iic/SenseVoiceSmall/summary)
2. 线路二：[百度网盘下载 SenseVoiceSmall](https://pan.baidu.com/s/1HW_UmfLiXhWwMjzS0GIpWg?pwd=qvna) 提取码：`qvna`

下载后，请将模型文件放置在上述路径中，或通过文件编辑器上传到 addon 配置目录的 models/SenseVoiceSmall 文件夹中。

### 配置文件

配置文件位于加载项配置目录：

```
/config/data/.config.yaml
```

如果未找到配置文件，系统会自动创建默认配置文件。首次运行时，会提示您修改配置文件中的 API 密钥等重要信息。

### 初次运行

首次启动插件时，会出现以下流程：

1. 检查模型文件，不存在则自动下载
2. 检查配置文件，不存在则自动创建
3. 提示您修改配置文件中的 API 密钥和其他设置
4. 配置好后需重启插件应用更改

这些提示只会在首次运行时显示，后续启动不会重复提示。

## 技术实现

本插件基于以下技术实现：

1. 使用 Home Assistant 标准加载项结构
2. 采用 S6-Overlay 进行服务管理，提高稳定性和可靠性
3. 使用 addon_config 目录存储配置和模型文件，符合 Home Assistant 最佳实践
4. 自动同步 Home Assistant 加载项配置到服务器配置

## 连接 ESP32 设备

1. 确保 ESP32 设备与 Home Assistant 在同一网络
2. WebSocket 服务地址：`ws://<您的Home Assistant IP>:8000/xiaozhi/v1/`
3. 将 ESP32 设备配置为连接上述 WebSocket 地址

## 故障排除

如果遇到以下问题，请参考处理方法：

1. **语音识别出现韩文、日文、英文**：检查模型文件是否正确加载
2. **TTS 任务出错或超时**：检查网络连接和配置文件设置
3. **连接问题**：确保 ESP32 设备与 Home Assistant 在同一网络
4. **无法自动下载模型**：网络问题或服务器故障，请尝试手动下载
5. **配置问题**：如果在加载项页面修改的配置未生效，请重启加载项并检查日志
6. **ASR 配置不完整错误**：确保您选择的 ASR 服务（如 DoubaoASR 或 TencentASR）已配置所有必要的参数
7. **TTS 配置不完整错误**：当选择 DoubaoTTS 时，确保已配置 appid 和 access_token

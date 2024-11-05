# Nextcloud

## 配置说明

### 全文索引

### OCR

- 设置为true以安装tesseract-ocr功能。

### OCR语言

- 任何语言都可以从这个页面设置(总是三个字母) [查询点击这里](https://tesseract-ocr.github.io/tessdoc/Data-Files#data-files-for-version-400-november-29-2016)

### PGID

- 允许设置用户。

### PUID

- 允许设置用户。

### TZ

- 时区

### 附加应用程序

- 指定要安装的其他apk文件;用逗号分隔。

### 证书

- ssl证书，必须位于本地ssl

###  cifs域

- cifs域

### cifs密码

- 可选项， smb密码，与smb shares密码相同

### cifs用户名

- 可选项， smb用户名，与smb shares用户名相同

### 默认电话区域

- 定义默认电话区域 https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements

### 禁用更新

- 防止插件自动更新应用程序。

### elasticsearch服务器

- elasticsearch服务器url

### 启用缩略图

- 为媒体文件启用几代缩略图(在旧系统中禁用)。

### env_memory_limit

- nextcloud可用内存限制(默认为512M)。

### env_post_max_size

- nextcloud post文件大小 (默认为512M)。

### env_upload_max_filesize

- nextcloud上传大小(默认为512M)。

### 密钥

- ssl密钥，必须位于本地的ssl。

### 本地磁盘

- 用逗号分隔要挂载的驱动器的硬件名称或其标签。例如sda1, sdb1, MYNAS…

### 网络磁盘

- 可选，要挂载的smbv2/v3服务器列表，以逗号分隔

### 信任域

- 允许选择信任域。不在此列表中的域将被删除，除了初始配置中使用的第一个域。

### 使用自己的证书

- 如果为true，则使用指定的certfile和keyfile。
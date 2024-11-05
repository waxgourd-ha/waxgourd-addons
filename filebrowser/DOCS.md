# Filebrowser

## 配置说明

### 无认证运行模式:

- 启用/停用ssl。

### 初始文件夹:

- 可选项，默认值 /。

### 证书文件:

- ssl证书文件。

### cifs域：

- cifs域。

### cifs用户名：

- 可选项，smb用户名，与smb shares用户名相同。

### cifs密码：

- 可选项，smb密码，与smb shares密码相同。

### 密钥：

- sl密钥。

### 本地磁盘：

- 用逗号分隔要挂载的驱动器的硬件名称或其标签。例如sda1, sdb1, MYNAS等。

### 网络磁盘：

- 可选，要挂载的smbv2/3服务器列表，以逗号分隔。

### 禁用缩略图：

- True /false(设置禁用缩略图为True或false;速度默认为true)。

### ssl：

- 启用/禁用ssl。

## 使用方法

- 可以通过浏览器页面访问 <http://homeassistant:port> （端口号默认8080）

- 默认用户名: "admin" 密码: "admin"

- 网络磁盘挂载到 `/share/storagecifs`下。
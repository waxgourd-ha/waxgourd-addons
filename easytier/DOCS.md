# Easytier

## 关于

基于 EasyTier 的高性能虚拟组网工具，支持三种组网模式：快速组网、官方 Web 控制台、自建 Web 控制台。通过纯环境变量配置，提供简洁安全的用户体验。

### 🚀 功能特性
 - ✅ 三模式支持：快速组网 / 官方 Web 控制台 / 自建 Web 控制台
 - ✅ 纯环境变量配置：通过 ET_* 环境变量管理所有参数，无需复杂 UI
 - ✅ 多架构兼容：支持 aarch64、amd64（覆盖树莓派、x86 服务器）
 - ✅ Alpine Linux 优化：使用 #!/bin/sh，镜像体积最小化
 - ✅ 安全第一：自动清理环境变量首尾空格，防止配置错误
 - ✅ 优雅关闭：正确处理 SIGTERM/SIGINT 信号，确保资源正确释放
 - ✅ 完整参数支持：支持 EasyTier 所有配置参数（60+ 个环境变量）

### 🛠️ 安装方法
**方式一：通过 GitHub 仓库（推荐）**
1. 进入 设置 → 加载项 → 加载项商店
1. 点击右上角菜单 → 仓库
1. 添加仓库地址：https://gitcode.com/waxgourd/addons
1. 在商店中找到 EasyTier 并点击安装

### 🛠️ 配置说明
**核心配置方式**

本插件**主要通过 `env_vars`** 配置所有参数，同时保留 `username` 作为 Web 控制台模式的快捷输入方式。

#### username 快捷方式

对于 **Web 控制台模式**，可直接在插件配置界面填写 `username`，无需通过 `env_vars` 设置 `ET_CONFIG_SERVER`。

** 示例 **：
```yaml
username: "myuser"  # 等价于 env_vars.ET_CONFIG_SERVER=myuser
```
**注意**：username 仅用于 Web 控制台模式，不能与 ET_CONFIG_SERVER 同时设置。

### 快速组网必需参数

| 参数                  | 说明     | 是否必需              |
| ------------------- | ------ | ----------------- |
| `ET_NETWORK_NAME`   | 网络名称   | ✅ 必须              |
| `ET_NETWORK_SECRET` | 网络密码   | ⚠️ 强烈推荐（允许空，但有警告） |
| `ET_PEERS`          | 对等节点地址 | ⚠️ 推荐（允许空，但有警告）   |
| `ET_DHCP`           | DHCP模式 | ❌ 可选（默认`false`）   |


###
**三种运行模式**

**模式一：快速组网（推荐新手）**

通过公共节点 + 密码快速打通多设备。

**必须参数：**
- ET_NETWORK_NAME：网络名称
- ET_NETWORK_SECRET：网络密码（强烈推荐）
- ET_PEERS：对等节点地址（如 tcp://public.easytier.cn:11010）

**配置示例**
```yaml
env_vars:
  - name: "ET_NETWORK_NAME"
    value: "myhome"
  - name: "ET_NETWORK_SECRET"
    value: "secure-password"
  - name: "ET_DHCP"
    value: "true"
  - name: "ET_PEERS"
    value: "tcp://public.easytier.cn:11010"
```
**模式二：官方 Web 控制台**

通过 https://easytier.cn/web 统一管理节点

**必需参数：**
- ET_CONFIG_SERVER：用户名（在官网注册）

**配置示例：**
```yaml
env_vars:
  - name: "ET_CONFIG_SERVER"
    value: "myuser"
  - name: "ET_CONSOLE_LOG_LEVEL"
    value: "info"
```
或者使用快捷方式：

```yaml
username: "myuser"
```
**模式三：自建 Web 控制台**

**必需参数：**
- ET_CONFIG_SERVER：自建服务器 URL（如 http://192.168.1.100:22020/myuser）

**配置示例：**
```yaml
env_vars:
  - name: "ET_CONFIG_SERVER"
    value: "http://myserver:22020/myuser"
  - name: "ET_MACHINE_ID"
    value: "server-01"
```

### 完整配置选项
可使用 `easytier-core --help` 查看全部配置项。

### 基础设置
#### 配置服务器

**完整列表参考**：https://easytier.cn/guide/network/configurations.html

### 🌟 高级配置示例
**示例1：家庭多设备互通（快速组网 + 子网代理）**
```yaml
env_vars:
  - name: "ET_NETWORK_NAME"
    value: "home-network"
  - name: "ET_NETWORK_SECRET"
    value: "my-secure-key"
  - name: "ET_DHCP"
    value: "true"
  - name: "ET_PEERS"
    value: "tcp://public.easytier.cn:11010"
  - name: "ET_PROXY_NETWORKS"
    value: "192.168.10.0/24,192.168.20.0/24"
  - name: "ET_MACHINE_ID"
    value: "ha-main-server"
```
**示例2：企业私有网络（自建控制台 + 高级日志）**
```yaml
env_vars:
  - name: "ET_CONFIG_SERVER"
    value: "http://config.internal:22020/myuser"
  - name: "ET_CONSOLE_LOG_LEVEL"
    value: "debug"
  - name: "ET_FILE_LOG_DIR"
    value: "/config/easytier-logs"
  - name: "ET_DISABLE_UDP_HOLE_PUNCHING"
    value: "false"
  - name: "ET_SOCKS5"
    value: "1080"
```
**示例3：最小化配置（官方控制台）**
```yaml
env_vars:
  - name: "ET_CONFIG_SERVER"
    value: "myuser"
```
### 🔍 故障排查
**问题1：插件启动失败**

**现象**：容器不断重启

**解决**：
1. 检查日志：**加载项 → EasyTier → 日志**
1. 确认 ET_CONFIG_SERVER 或 ET_NETWORK_NAME 已配置
1. 验证 env_vars 格式正确（name/value 均为字符串）

**问题2：节点无法互通**

**检查步骤**：
- **防火墙**：确认路由器/系统防火墙放行了相关端口
- **对等节点**：检查 ET_PEERS 是否正确配置
- **网络名称**：所有节点的 ET_NETWORK_NAME 必须完全相同
- **网络密钥**：所有节点的 ET_NETWORK_SECRET 必须完全相同

**问题3：配置包含空格**

**现象**：配置值异常或无法识别

**解决：**
本插件**自动清理**所有环境变量 name 和 value 的首尾空格。但请避免在值**中间**添加不必要的空格

**错误示例**：
```yaml
  - name: "ET_PEERS"
    value: " tcp://1.1.1.1:11010, udp://2.2.2.2:11011 "  # ❌ 首尾空格
```
**正确示例**：
```yaml
  - name: "ET_PEERS"
    value: "tcp://1.1.1.1:11010,udp://2.2.2.2:11011"  # ✅ 无多余空格
```

**问题4：Web 控制台不显示节点**

**检查**：
1. 确认 ET_CONFIG_SERVER 用户名正确
1. 检查 ET_FILE_LOG_LEVEL=debug 日志，确认连接到 web.easytier.cn
1. 等待 30-60 秒，Web 控制台有延迟

**问题5：日志文件找不到**
**解决**：
```yaml
env_vars:
- name: "ET_FILE_LOG_DIR"
  value: "/config/logs"  # 使用 /config 目录确保持久化
```
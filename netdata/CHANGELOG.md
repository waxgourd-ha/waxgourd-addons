### 1.47.4 (2024-10-14)

- 版本升级

### 1.47.0 (2024-08-23)

- 版本升级

### 1.46.3 (2024-07-30)

- 版本升级

### 1.46.2 (2024-07-12)

Netdata v1.46.2 是一个补丁版本，用于解决自 v1.46.1 以来发现的问题。

此修补程序版本提供了以下错误修复和更新：

 - 将 uid/gid/egid 设置为 0 以提高与 root 所需命令 （ndsudo） 的兼容性。
 - 改进了 ksm/swap/cma/zswap 指标的收集：现在仅在启用该功能时收集（proc/vmstat、proc/meminfo）。
 - 将 netdata.spec 中的 Golang 版本与 go.mod  对齐。
 - 添加了对 go.d.plugin lm_sensors 的弱依赖 （netdata.spec/plugin-go）。
 - 修复了 Prometheus“prometheus_all_hosts”导出格式，在“instance”标签前添加缺少逗号。
 - 通过切换到微秒 （proc/diskstats） 提高了平均 IO 操作时间指标的准确性。
 - 修复了在 Docker 容器 （diskspace.plugin） 中运行 Netdata 时对主机挂载点的监控 。
 - 本机软件包安装（deb、rpm）现在包括 netdata-updater 服务和计时器，用于在没有 cron 的系统上自动更新。
 - 警报原型：为清楚起见，计算中的默认“after”值设置为 -600（10 分钟）。
 - 通过处理 HTTP/1.0 200 连接建立响应，修复了通过代理的云连接。
 - 通过强制执行供应商包括排序来确保正确的库使用，从而改进了构建。
 - 由于缺乏支持，在打包过程中默认禁用了 logsmanagement 插件。
 - 将到期警告前的默认天数与文档一致 （30/15） （go.d/whoisquery）。
 - 过期时间现在以天而不是秒为单位显示（whoisquery 和 x509check 警报）。
 - 通过遵守 DOCKER_HOST 环境变量 （go.d.plugin） 改进了 Docker 容器中的功能。
 - 改进了ping_host_reachable警报计算以提高可靠性 。

### 1.46.1 (2024-06-26)

- 版本升级

### 1.45.4 (2024-05-17)

- 版本升级

### 1.45 (2024-03-25)

- 版本升级

### 1.44.1 (2024-01-02)

- 首次推出
## 20260601
- 版本升级
## 20260529
### Added
- 初始版本：将 gfs-webmode（SingBox GUI Web 版）打包为 HAOS Addon
- Slug: `turbo4`，默认端口 2097
- 3 阶段 Dockerfile：Node.js 前端构建 → Go webserver 构建 → hassio-addons/base 运行时
- s6-overlay 服务：`init-gfs`（oneshot）+ `gfs`（longrun）
- Q2 实现：addon 配置 `auto_start_kernel=true` 时，init 阶段自动后台启动 sing-box
- addon 配置项：`panel_port`, `username`, `password`, `auto_start_kernel`

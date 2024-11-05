### 1.5.3 (2024-10-14)

1. [修复] Docker管理器 分页下开启关闭容器控制串页、异常的问题
1. [优化] Docker管理器 容器启动失败错误原因提醒
1. [优化] Docker管理器 取消分页并支持按容器名称排序
1. [优化] Docker管理器 页面优化

### 1.5.2 (2024-09-02)

1. [增强] 自定义页脚支持 <script> js的代码和引用外部js文件
1. [增强] docker 容器列表在部分设备上加载速度
1. [增强] 项目卡片数据支持本地缓存，提升加载过程
1. [增强] 公开模式下可以切换搜索引擎（仅限当次访问有效，页面刷新后恢复原搜索引擎）
1. [优化] 在 iframe 框架中本页打开时，将使用父窗口打开1.
1. [优化] docker 管理器样式、移动端显示效果
1. [优化] do'"cker 卡片绑定的容器在更新后会自动匹配更新同名容器（为安全考虑，仅在登录状态下生效）
1. [优化] 一些细节更新
1. [修复] 搜索栏在 Mac OS 下 Safari 浏览器中文输入兼容性问题
1. [JS插件] 侧栏目录插件 （需自行安装）

### 1.5.1 (2024-07-12)

1. v1.5.0 所有功能
1. [修复] 普通图标卡片因鼠标中键新窗打开地址导致无法拖动排序
1. [修复] 风格设置搜索栏组件默认文字颜色为空的问题

### 1.5.0 (2024-05-14)

1. docker版本从v1.3.0及之前升级到此版本前请务必先阅读更新说明

1. 如果要在容器中查看docker状态，挂载时需加：-v /var/run/docker.sock:/var/run/docker.sock

1. [修复] v1.5.0-beta24-05-10 系统状态添加磁盘项无效的问题

### v1.5.0-beta24-05-10 beta (2024-05-10)

1. docker版本从v1.3.0及之前升级到此版本前请务必先阅读更新说明
1. 如果要在容器中查看docker状态，挂载时需加：-v /var/run/docker.sock:/var/run/docker.sock
1. [新增] 简单的docker管理器（非PRO可查看状态，不支持开启和关闭容器）
1. [新增] 重构图标卡片，增加docker应用和内置应用图标卡片
1. [优化] 分组风格支持独立设置，并可以设置公开模式隐藏
1. [优化] 增加可配置的登录过期时长（并将原72小时过期改为168小时，仍延续自动续期机制）
1. [优化] 内置应用启动器等按钮移至右上角

### 1.4.0 (2024-04-26)

1. [新增] OpenAPI开放接口beta功能，开发者可以通过调用API接口来实现一些功能 
1. [新增] 全局站点设置：自定义站点标题 PRO、自定义站点图标 PRO、自定义登录页面背景图
1. [新增] 在线编辑全局自定义 index.js 和 index.css 文件 PRO（非PRO用户依旧可以从程序安装目录中修改）
1. [新增] 背景图支持heic、avif格式上传 [ #77 ]（仅对avif进行测试了）
1. [修复] v1.4.0-beta24-04-12 旧版用户升级不兼容在线编辑js、css的问题
1. [优化] 禁用referrer 。解决部分网站跳转后（例：qBittorrent）无法打开 
1. [优化] 获取三方网站图标
1. [优化] 编辑项目时网址检测未以 http/https 开头并进行提醒
1. [优化] 修改系统状态[详情图标]显示格式，包含硬盘和内存的信息格式[已使用量/总量]
1. [其他] docker版本精简挂载目录为一个 ./conf 具体参考 [（说明）](https://github.com/hslr-s/sun-panel/discussions/98)
1. [其他] 更多可以参考之前 v1.4.0-beta* 版本更新日志

### 1.3.0 (2024-03-23)

- 首次推出
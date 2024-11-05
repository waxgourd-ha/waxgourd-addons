# 小雅Alist

## 配置说明

1. 软路由盒子类似 n1 等，具有 openwrt环境 （可以终端上一键配置）
2. NAS 等具有docker插件 （无法或很难登入终端，需要图形化自行配置）
3. 云服务器也就是俗称的 vps （可以终端上一键配置）

### 注：
  1. 在配置中【定时清理设置】，此处的设置顺序：分 时 天 月 周； 默认设置的是（20 05 * * *）此处代表是每天凌晨5:20
  2. 不清理设置需将此处键入空格，然后保存，并重启 即可


## 安装说明

加载项一键安装和更新

端口：5678
访问： http://xxxxx:5678/ （xxxx 为你alist所在设备的 IP）

使用webdav连接方式：  
地址：http://xxxxx:5678/dav  
webdav 账号密码  
用户: guest 密码: guest_Api789

重启就会自动更新数据库及搜索索引文件   
推荐打开自动更新，保证自动同步，防止列表获取失效

---

获取阿里云盘信息方式：

token: [https://alist.nn.ci/zh/guide/drivers/aliyundrive.html#%E5%88%B7%E6%96%B0%E4%BB%A4%E7%89%8C](https://alist.nn.ci/zh/guide/drivers/aliyundrive.html#%E5%88%B7%E6%96%B0%E4%BB%A4%E7%89%8C)

刷新token: [https://alist.nn.ci/zh/guide/drivers/aliyundrive_open.html#%E5%88%B7%E6%96%B0%E4%BB%A4%E7%89%8C](https://alist.nn.ci/zh/guide/drivers/aliyundrive_open.html#%E5%88%B7%E6%96%B0%E4%BB%A4%E7%89%8C)

文件夹id：
转存 [https://www.aliyundrive.com/s/rP9gP3h9asE](https://www.aliyundrive.com/s/rP9gP3h9asE)  到自己网盘（选择资源盘），然后浏览器打开转存后的目录，浏览器的url
https://www.aliyundrive.com/drive/file/resource/640xxxxxxxxxxxxxxxxxxxca8a 最后一串就是，记得这个目录不要删，里面的内容可以定期删除

# CUPS AirPrint

## 使用方法

- CUPS管理员登录：print，密码：print（可以在Dockerfile中更改）



**驱动安装方法**

以惠普1020打印机为例：按以下步骤安装hplip驱动的插件。

1. 浏览器打开下载地址：https://www.openprinting.org/download/printdriver/auxfiles/HP/plugins/

2. 找到和版本号对应的两个.run和.run.asc文件，以及不区分版本的.plugin文件，例如：
  ```json
   hp_laserjet_1020.plugin（不区分版本）、
   hplip-3.22.10-plugin.run（3.22.10版本）、	
   hplip-3.22.10-plugin.run.asc（3.22.10版本）
``` 
3. 通过Filebrowser打开addon_configs/xxxxxx_opencups/upload目录，将上面三个文件拷贝进去。

4. 成功放进去后，使用命令进入插件的安装，浏览器打开http://homeassistant.local:7681 进入终端：
输入命令行
```shell
login
```
第二步，进入docker容器内部
```shell
wgha d cups -S /bin/bash
```
第三步，执行命令
```shell
sudo hp-plugin -p /config/upload/
```
5. 完成插件的安装，期间会询问是否同意许可协议，按“y”同意。

6. 到此驱动添加完毕，addons webui打开 CUPS-AirPrint即可使用。


参考地址：https://blog.csdn.net/inthesun29/article/details/127143638

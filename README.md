# Aria2 一键安装管理脚本 增强版
增强版脚本整合了 [Aria2 完美配置](https://github.com/P3TERX/aria2.conf)，在安装 Aria2 的过程中会下载这套配置方案，这套方案包含了配置文件、附加功能脚本等文件，用于实现 Aria2 功能的增强和扩展，提升 Aria2 的下载速度与使用体验，解决 Aria2 在使用中遇到的 BT 下载无速度、文件残留占用磁盘空间、任务丢失、重复下载等问题。

## 功能特性

- 使用 [Aria2 完美配置](https://github.com/P3TERX/aria2.conf)方案
    * BT 下载率高、速度快
    * 重启后不丢失任务进度、不重复下载
    * 删除正在下载的任务自动删除未完成的文件
    * 下载错误自动删除未完成的文件
    * 下载完成自动删除控制文件(`.aria2`后缀名文件)
    * 下载完成自动删除种子文件(`.torrent`后缀名文件)
    * 下载完成自动删除空目录
    * BT 下载完成自动清除垃圾文件(文件类型过滤功能)
    * BT 下载完成自动清除小文件(文件大小过滤功能)
    * 有一定的防版权投诉、防迅雷吸血效果
    * 更好的 PT 下载支持

## 配置文件说明：
|   文件  |   说明  |
| --- | --- |
|  aria2.conf   |   Aria2 配置文件。建议配合 1.35.0 及以上版本使用。内附可能比官方文档还详细的中文注释说明和修改建议，在不了解的情况下随意修改可能导致本方案的特性失效。| 
|   script.conf  |   Aria2 附加功能脚本配置文件。  |
|   core  |   Aria2 附加功能脚本核心文件。所有脚本都依赖于此文件运行。  |
|clean.sh|文件清理脚本。在下载完成后执行(on-download-complete)，自动清理控制文件(*.aria2)、种子文件(*.torrent)和空目录。（默认启用）|
|delete.sh|文件删除脚本。在下载停止后执行(on-download-stop)，当下载错误或删除正在下载的任务后自动删除相关文件，并自动清理控制文件(*.aria2)、种子文件(*.torrent)和空目录，防止不必要的磁盘空间占用。（默认启用）|
|upload.sh|文件上传脚本。在下载完成后执行(on-download-complete)，自动调用 RCLONE 上传(move)下载完成的文件到网盘，并自动清理控制文件(*.aria2)、种子文件(*.torrent)和空目录。（默认不启用）|
|rclone.env|RCLONE 环境变量文件。配合upload.sh使用，用于配置 RCLONE 的选项参数。|
|move.sh|文件移动脚本。在下载完成后执行(on-download-complete)，自动将下载完成的文件移动到指定目录，并自动清理控制文件(*.aria2)、种子文件(*.torrent)和空目录。（默认不启用）|


- 使用 [Aria2 Pro Core](https://github.com/P3TERX/Aria2-Pro-Core) 项目最新静态编译二进制文件
    - 单服务器线程数最大值无上限（已破解线程数限制）
    - 防掉线程优化
    - 最新依赖库，下载更安全、稳定、快速
    - 持续更新最新版本
- 支持新一代互联网协议 IPv6
- 定时自动更新 BT tracker 列表（无需重启）

## 使用说明

* 为了确保能正常使用，请先安装基础组件`wget`、`curl`、`ca-certificates`，以 Debian 为例子：
```
apt install wget curl ca-certificates
```

* 下载脚本
```
wget -N https://raw.githubusercontent.com/dasima4396/aria2.sh/master/aria2.sh && chmod +x aria2.sh
```

* 运行脚本
```
./aria2.sh
```

* 选择你要执行的选项
```
 Aria2 一键安装管理脚本 增强版 [v2.7.4] by P3TERX.COM
 
  0. 升级脚本
 ———————————————————————
  1. 安装 Aria2
  2. 更新 Aria2
  3. 卸载 Aria2
 ———————————————————————
  4. 启动 Aria2
  5. 停止 Aria2
  6. 重启 Aria2
 ———————————————————————
  7. 修改 配置
  8. 查看 配置
  9. 查看 日志
 10. 清空 日志
 ———————————————————————
 11. 手动更新 BT-Tracker
 12. 自动更新 BT-Tracker
 ———————————————————————

 Aria2 状态: 已安装 | 已启动

 自动更新 BT-Tracker: 已开启

 请输入数字 [0-12]:
```

## 其他操作

启动：`/etc/init.d/aria2 start` | `service aria2 start`

停止：`/etc/init.d/aria2 stop` | `service aria2 stop`

重启：`/etc/init.d/aria2 restart` | `service aria2 restart`

查看状态：`/etc/init.d/aria2 status` | `service aria2 status`

配置文件路径：`/root/.aria2c/aria2.conf` （配置文件有中文注释，若语言设置有问题会导致中文乱码）

默认下载目录：`/root/downloads`

RPC 密钥：随机生成，可使用选项`7. 修改 配置文件`自定义

### Trackers 来源

[XIU2/TrackersListCollection](https://github.com/XIU2/TrackersListCollection)

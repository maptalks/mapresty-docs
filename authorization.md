---
layout: docs
title: 授权
permalink: /authorization/
---

# 授权

Mapresty安装完毕后, 会为操作系统的命令行终端生成一个全局命令: `mapresty`。

* 获取SystemId
```bash
$ mapresty sid /path/to/instance/config.json"
```

* 申请授权文件

将SystemId发送到`auth@maptalks.org`。    

* 放置授权文件

将从Maptalks获取的授权文件`license.lic`，放入Mapresty安装目录下的`licenses/`文件夹中。

* 启动Mapresty
```bash
$ mapresty start /path/to/config.json
```

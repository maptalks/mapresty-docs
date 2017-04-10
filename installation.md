---
layout: docs
title: 安装
permalink: installation/
---

# 安装

MapResty的安装非常简单，只需要从[此处](https://github.com/MapTalks/mapresty/releases)下载压缩包，
并解压到想安装的目录即可。

有两种形式的压缩包：
* 平台相关。压缩包中附带了平台相关的JRE和Node.js
* 平台无关。需要额外安装[JRE(Java 7及以上)][1]和[Node.js(5.0及以上)][2]

[1]: http://www.oracle.com/technetwork/java/javase/downloads/
[2]: https://nodejs.org

选择平台无关的压缩包时，在安装完JRE和Node.js后，可能需要为运行MapResty的用户设置系统路径，
以确保可以在系统路径中优先找到安装的JRE和Node.js。

假设安装的目录是`C:\mapresty`，那么可以将`C:\mapresty\bin`也加入系统路径。
之后即可直接在CLI里运行`mapresty`来启动/停止MapResty。


# 运行

`mapresty`命令用法：

## 运行目录初始化

运行目录存放了`mapresty`所需的配置文件、示例数据、www服务的静态资源(例如客户端地图程序maptalks.js)等。

```bash
$ mapresty init /path/to/instance
```

初始的运行目录结构如下：

{% highlight bash %}

    $ tree /path/to/instance
    .
    |- www
    |   |-maptalks.js
    |   |-maptalks.css
    |   |-images+
    |- db
    |   |-default.db
    |- logs
    |- tile
    |   |- sample
    |- config.json
{% endhighlight %}

在进行一些[配置](configuration.html)之后，即可启动服务了。

## 启动服务

```bash
$ mapresty start /path/to/instance/config.json
```

## 停止服务

```bash
$ mapresty stop /path/to/instance/config.json
```

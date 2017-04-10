---
layout: docs
title: 安装
permalink: /configuration/
---

# 配置

MapTalks 允许在一台服务器上运行多个MapTalks 服务实例， 每个服务实例各自拥有独立的运行目录。

运行目录可以用 `mapresty init [dir]` 生成， 例如：

```bash
mapresty init /path/to/instance
# 运行目录结构
    .
    |- static
    |   |-maptalks.js
    |   |-maptalks.css
    |   |-images+
    |- db
    |   |-default.db
    |- logs
    |- tile
    |   |- sample
    |- config.json
```

## config.json配置说明

每个MapTalks运行目录中只有一个配置文件， 即根目录下的 `config.json`

初始的config.json内容如下：

```javascript
{
    "server" : {
        "listen": "0.0.0.0",
        "port" : 8090,
        "logLevel": "INFO",
        "logPath" : "./logs",
        "staticPath" : "./static"
    },
    "database" : {
        "instances": [
            {
                "name": "default",
                "type": "sqlite",
                "database": "./db/default.db"
            }
        ],
        "pool": {
            "initialSize": 2,
            "maxActive": 20,
            "maxWait": 60000,
            "timeBetweenEvictionRunsMillis": 60000,
            "minEvictableIdleTimeMillis": 300000,
            "validationQuery": "SELECT 'x'",
            "testWhileIdle": true,
            "testOnBorrow": false,
            "testOnReturn": false,
            "poolPreparedStatements": true,
            "maxPoolPreparedStatementPerConnectionSize": 20
        }
    },
    "rest" : {
        "enable" : true,
        "listen": "localhost",
        "port": 11215,
        "logLevel" : "INFO",
        "logPath"  : "./logs"
    },
    "tile" : {
        "enable"   : true,        
        "listen": "localhost",
        "port": 11214,
        "logLevel" : "INFO",
        "logPath"  : "./logs",
        "sources": [
            {
                "name": "sample",
                "uri": "template+file://./sample?filetype=png"
            }
        ]
    },
    "snap": {
        "enable": false,
        "listen": "localhost",
        "port": 11219,
        "logLevel": "INFO",
        "folder": "./snapshots"
    }
}
```

### 配置项说明

日志级别： "ERROR", "WARN", "INFO", "DEBUG"

根路径： 配置中相对路径的根路径为运行参数中config.json所在目录

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Module</th>
      <th>Setting</th>
      <th>
        <span class="option">Options</span> and <span class="flag">Flags</span>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class="setting">
      <td rowspan="5">
        <p class="name"><strong>server</strong></p>
        <p class="description"><strong>主服务</strong></p>
      </td>
      <td>
        <p class="name"><strong>端口</strong></p>
        <p class="description">主服务端口</p>
      </td>
      <td class="align-center">
        <p><code class="option">"port" ： 8090</code></p>
        <p class="description">默认 : 8090</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>监听地址</strong></p>
        <p class="description">主服务的监听地址， 即只响应指定地址的网络请求</p>
      </td>
      <td class="align-center">
        <p><code class="option">"listen" ： "0.0.0.0"</code></p>
        <p class="description">默认 : "0.0.0.0"，即不做限制</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>日志级别</strong></p>
        <p class="description">主服务日志级别</p>
      </td>
      <td class="align-center">
        <p><code class="option">"logLevel" ： "INFO"</code></p>
        <p class="description">默认 : "INFO"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>日志文件夹</strong></p>
        <p class="description">主服务日志的文件夹</p>
      </td>
      <td class="align-center">
        <p><code class="option">"logPath" ： "./logs"</code></p>
        <p class="description">默认 : "./logs"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>静态资源文件夹</strong></p>
        <p class="description">静态资源文件夹路径</p>
      </td>
      <td class="align-center">
        <p><code class="option">"staticPath" ： "./static"</code></p>
        <p class="description">默认 : "./static"</p>
      </td>
    </tr>
    <tr class="setting">
      <td rowspan="2">
        <p class="name"><strong>database</strong></p>
        <p class="description"><strong>数据库配置</strong></p>
      </td>
      <td>
        <p class="name"><strong>默认连接池配置</strong></p>
        <p class="description">设置默认的数据库连接池配置，连接池采用了<a href="https://github.com/alibaba/druid">Druid</a>， 可参考其<a href="https://github.com/alibaba/druid/wiki/DruidDataSource%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7%E5%88%97%E8%A1%A8">连接池参数说明</a></p>
      </td>
      <td class="align-center">
        <p><code class="option">"pool" ： KEY-VALUE</code></p>
        <p><code class="javascript">
        {            
            "initialSize": 2,
            "maxActive": 20,
            "maxWait": 60000,
            "timeBetweenEvictionRunsMillis": 60000,
            "minEvictableIdleTimeMillis": 300000,
            "validationQuery": "SELECT 'x'",
            "testWhileIdle": true,
            "testOnBorrow": false,
            "testOnReturn": false,
            "poolPreparedStatements": true,
            "maxPoolPreparedStatementPerConnectionSize": 20
        }
        </code>
        </p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>数据库连接配置</strong></p>
        <p class="description">配置多个数据库连接实例， 供rest服务等依赖数据库的模块服务使用。</p>
      </td>
      <td class="align-center">
        <p><code class="option">instances ： [KEY-VALUE]</code></p>
        <p class="description">详细的数据库连接实例配置说明请参考<a href="configuration-db.html">这里</a></p>
      </td>
    </tr>
    <tr class="setting">
      <td rowspan="4">
        <p class="name"><strong>rest</strong></p>
        <p class="description"><strong>服务配置</strong></p>
      </td>
      <td>
        <p class="name"><strong>是否启用</strong></p>
        <p class="description">是否启用rest模块</p>
      </td>
      <td class="align-center">
        <p><code class="option">"enable" : true</code></p>
        <p class="description">true : 启用; false : 禁用</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>端口</strong></p>
        <p class="description">rest服务端口</p>
      </td>
      <td class="align-center">
        <p><code class="option">"port" : 11215</code></p>
        <p class="description">默认: 11215</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>监听地址</strong></p>
        <p class="description">服务监听地址， 即只响应指定地址的网络请求</p>
      </td>
      <td class="align-center">
        <p><code class="option">"listen" : "localhost"</code></p>
        <p class="description">默认: "localhost"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>日志级别</strong></p>
        <p class="description">服务日志级别</p>
      </td>
      <td class="align-center">
        <p><code class="option">"logLevel" ： "INFO"</code></p>
        <p class="description">默认 : "INFO"</p>
      </td>
    </tr>
    <tr class="setting">
      <td rowspan="5">
        <p class="name"><strong>tile</strong></p>
        <p class="description"><strong>服务配置</strong></p>
      </td>
      <td>
        <p class="name"><strong>是否启用</strong></p>
        <p class="description">是否启用tile模块</p>
      </td>
      <td class="align-center">
        <p><code class="option">"enable" : true</code></p>
        <p class="description">true : 启用; false : 禁用</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>端口</strong></p>
        <p class="description">tile服务端口</p>
      </td>
      <td class="align-center">
        <p><code class="option">"port" : 11215</code></p>
        <p class="description">默认: 11215</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>监听地址</strong></p>
        <p class="description">服务监听地址， 即只响应指定地址的网络请求</p>
      </td>
      <td class="align-center">
        <p><code class="option">"listen" : "localhost"</code></p>
        <p class="description">默认: "localhost"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>日志级别</strong></p>
        <p class="description">服务日志级别</p>
      </td>
      <td class="align-center">
        <p><code class="option">"logLevel" ： "INFO"</code></p>
        <p class="description">默认 : "INFO"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>tile服务数据源配置</strong></p>
        <p class="description">为tile服务配置数据源，支持 <a href="https://github.com/MapTalks/mapresty-tile">mapresty-tile</a> 所支持的所有数据源.</p>
      </td>
      <td class="align-center">
        <p><code class="option">"sources" ： [KEY-VALUE]</code></p>
        <p class="description">更详细的tile数据源配置说明请参考<a href="https://github.com/MapTalks/mapresty-tile/blob/master/README.md">这里</a></p>
      </td>
    </tr>
    <tr class="setting">
      <td rowspan="5">
        <p class="name"><strong>snap</strong></p>
        <p class="description"><strong>服务配置</strong></p>
      </td>
      <td>
        <p class="name"><strong>是否启用</strong></p>
        <p class="description">是否启用snap模块</p>
      </td>
      <td class="align-center">
        <p><code class="option">"enable" : true</code></p>
        <p class="description">true : 启用; false : 禁用</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>端口</strong></p>
        <p class="description">snap服务端口</p>
      </td>
      <td class="align-center">
        <p><code class="option">"port" : 11219</code></p>
        <p class="description">默认: 11219</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>监听地址</strong></p>
        <p class="description">服务监听地址， 即只响应指定地址的网络请求</p>
      </td>
      <td class="align-center">
        <p><code class="option">"listen" : "localhost"</code></p>
        <p class="description">默认: "localhost"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>日志级别</strong></p>
        <p class="description">服务日志级别</p>
      </td>
      <td class="align-center">
        <p><code class="option">"logLevel" ： "INFO"</code></p>
        <p class="description">默认 : "INFO"</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>截图目录</strong></p>
        <p class="description">截取的图片的存储目录</p>
      </td>
      <td class="align-center">
        <p><code class="option">"folder"： "./snapshots"</code></p>
        <p class="description">默认 : "./snapshots"</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

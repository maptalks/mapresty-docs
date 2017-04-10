---
layout: docs
title: 安装
permalink: configuration-db/
---

# 数据库配置

MapTalks具备将数据存入空间数据库， 和在空间数据库上进行空间查询的能力。

MapTalks目前支持将以下数据库或数据文件作为空间库：

* File (只读)
    * Shapefile
    * GeoJSON
* SQLite/Spatialite
* MySQL
* PostgreSQL/PostGIS
* MongoDB
* MicroSoft SQL Server
* Oracle
* DB2

## config.json

空间数据库配置在[config.json](configuration.html)中的`database`配置项， 如下所示：

```javascript
...
"database" : {
    //数据库连接实例配置
    "instances": [
        //第一个数据库连接实例
        {
            //实例名称， 供查询程序引用
            //default是一个特殊的实例名称， 如果查询程序中没有指明数据库实例， 则默认访问default实例
            "name": "default",
            //数据库类型，这里为sqlite
            "type": "sqlite",
            //sqlite数据文件
            "database": "./db/default.db"
            //sqlite不需要配置数据库连接池
        }, 
        //第二个数据库连接实例
        {
            //实例名称， 供查询程序引用   
            "name": "file",
            //数据库类型，这里为sqlite
            "type": "file",
            //sqlite数据文件
            "database": "./db/filedb"
            //sqlite不需要配置数据库连接池
        },        
        //第三个数据库连接实例
        {
            "name": "mysql",
            //数据库类型，这里是mysql
            "type": "mysql",
            //主机
            "host": "localhost",
            //端口
            "port": 3306,
            //数据库名称
            "database": "testdb",
            //jdbc连接参数
            "parameters": "?useUnicode=true&characterEncoding=utf-8",
            //用户名
            "username": "root",
            //访问密码
            "password": "root",
            //连接池配置
            //这里设置的参数会覆盖默认连接池配置中的相应参数
            "pool" : {
                "initialSize": 5,
                "maxActive": 50
            }
        }
    ],
    //默认连接池配置
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
}
...
```

各类数据库在MapTalks中的配置说明如下：

## File

MapTalks支持基于文件系统的空间库， 文件空间库是一个本地文件夹， 其中包含了:
* 一个JSON格式的空间库配置文件db.json
* 图层数据文件， 支持shapefile和GeoJSON数据

文件空间库只支持file_shp和file_geojson类型图层， 不支持其他的图层类型。

[Shapefile](https://en.wikipedia.org/wiki/Shapefile)是[ESRI](http://www.esri.com/)公司发布的空间数据文件格式， 其采用二进制形式存储， 是目前最流行的空间数据存储文件格式。
[GeoJSON](http://www.geojson.org)是一个基于JSON格式的空间数据格式，其采用文本形式存储，是http服务中最流行的空间数据交换格式。

一个典型的文件空间库文件夹结构
```bash
    .
    |- db.json
    |- shp
    |   |- layer1.shp # shapefile空间数据文件
    |   |- layer1.dbf # shapefile属性数据文件
    |- geojson
    |   |- layer2.geojson # geojson数据文件
```

### db.json示例
```javascript
{
    // 空间库的crs
    "crs" : "gcj02",
    // 版本
    "version" : "1.0",
    // 图层列表
    "layers" : [
        {
            // 图层id
            "id"        : "layer1",
            // 图层类型， shapefile类型图层
            "type"      : "file_shp",
            // 数据文件路径， 只支持当前目录内的文件
            "source"    : "shp/layer1.shp",
            // file_shp图层的配置属性
            "properties": {
                // 文件编码， 默认是UTF-8
                "encoding" : "UTF-8",
                // 载入的DBF属性列表， 字符串类型， 以逗号(,)分隔
                "property" : "prop1, prop2, prop3"
            }
        },
        {
            // 图层id
            "id"        : "layer2",
            // 图层类型， geojson类型图层
            "type"      : "file_geojson",
            // 数据文件路径， 只支持当前目录内的文件
            "source"    : "geojson/layer2.geojson",
            // file_shp图层的配置属性
            "properties": {
                // 文件编码， 默认是UTF-8
                "encoding" : "UTF-8"
            }
        }
    ]
}
```

## SQLite/Spatialite

SQLite和Spatialite是基于文件系统的嵌入式数据库， 很适合数据量不大、用户量不大应用场景。

例如演示系统、一些内部地图系统等。

另因为SQLite和Spatialite数据文件的便携性， 也很适合用于数据的导入导出、分发和备份等。

SQLite/Spatialite的配置方法:

```javascript
{
    //实例名称， 供查询程序引用
    //default是一个特殊的实例名称， 如果查询程序中没有指明数据库实例， 则默认访问default实例
    "name": "sqlite",
    //数据库类型
    "type": "sqlite",
    //sqlite的数据文件路径
    //如果是相对路径， 跟路径为config.json的所在目录
    "database": "./db/default.db"
    //sqlite不需要配置数据库连接池
}
```

## MySQL

```javascript
{
    "name": "mysql",
    //数据库类型
    "type": "mysql",
    //主机
    "host": "localhost",
    //端口, 3306为mysql的默认端口
    "port": 3306,
    //数据库名称
    "database": "testdb",
    //jdbc连接参数
    "parameters": "?useUnicode=true&characterEncoding=utf-8",
    //用户名
    "username": "root",
    //访问密码
    "password": "root",
    //连接池配置
    //这里设置的参数会覆盖默认连接池配置中的相应参数
    "pool" : {
        "initialSize": 5,
        "maxActive": 50
    }
}
```

## PostgreSQL/PostGIS
```javascript
{
    "name": "mysql",
    //数据库类型
    "type": "postgresql",
    //主机
    "host": "localhost",
    //端口, 5432为PostgreSQL的默认端口
    "port": 5432,
    //数据库名称
    "database": "testdb",
    //jdbc连接参数
    "parameters": "8",
    //用户名
    "username": "postgresql",
    //访问密码
    "password": "postgresql",
    //连接池配置
    //这里设置的参数会覆盖默认连接池配置中的相应参数
    "pool" : {
        "initialSize": 3
    }
}
```
## MongoDB
```javascript
{
    "name": "mongo",
    //数据库类型
    "type": "mongo",
    //主机
    "host": "localhost",
    //端口, 27017为MongoDB的默认端口
    "port": 27017,
    //数据库名称
    "database": "testdb",
    //jdbc连接参数
    "parameters": "",
    //用户名
    "username": "mongo",
    //访问密码
    "password": "mongo"
    //MongoDB无需设置连接池
}
```
## MicroSoft SQL Server
```javascript
{
    "name": "mssql",
    //数据库类型
    "type": "mssql",
    //主机
    "host": "localhost",
    //端口, 1433为SQL Server的默认端口
    "port": 1433,
    //数据库名称
    "database": "testdb",
    //jdbc连接参数
    "parameters": "",
    //用户名
    "username": "sa",
    //访问密码
    "password": "sa",
    //连接池配置
    //这里设置的参数会覆盖默认连接池配置中的相应参数
    "pool" : {
        "initialSize": 3
    }
}
```
## Oracle
```javascript
{
    "name": "oracle",
    //数据库类型
    "type": "oracle",
    //主机
    "host": "localhost",
    //端口, 1521为Oracle的默认端口
    "port": 1521,
    //Oracle数据库的SID
    "database": "orcl",
    //jdbc连接参数
    "parameters": "",
    //用户名
    "username": "orcluser",
    //访问密码
    "password": "orcluser",
    //连接池配置
    //这里设置的参数会覆盖默认连接池配置中的相应参数
    "pool" : {
        "initialSize": 3
    }
}
```
## DB2

DB2存在多种JDBC驱动， 不同的情况需要不同的JDBC驱动， [这里](http://www-01.ibm.com/support/docview.wss?uid=swg21363866)参阅相关说明

```javascript
{
    "name": "db2",
    //数据库类型
    "type": "db2",
    //主机
    "host": "localhost",
    //端口, 50000为DB2的默认端口
    "port": 50000,
    //Oracle数据库的SID
    "database": "testdb",
    //jdbc连接参数
    "parameters": "",
    //用户名
    "username": "db2admin",
    //访问密码
    "password": "db2admin",
    //连接池配置
    //这里设置的参数会覆盖默认连接池配置中的相应参数
    "pool" : {
        "initialSize": 3,
        "driverClassName" : "com.ibm.db2.jcc.DB2Driver"
    }
}
```

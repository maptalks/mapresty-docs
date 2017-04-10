---
layout: docs
title: 安装
permalink: /docs-cn/spatial-db/
---

# 空间数据库的使用

MapTalks的空间数据库功能包括：

* 空间数据库的初始化
* 图层的创建、删除、修改和查询
* 空间数据的插入、删除、修改和查询
* 结合空间条件与属性条件的数据查询

MapTalks中由rest模块来负责空间数据库的所有功能。

## 典型的空间数据库应用过程

以下以最常用的SQL数据库为例， 列举空间数据库的一个典型应用过程：

* 初始化空间库，载入必须的配置表和图层表。
* 创建一个图层， 图层有很多种类型， 最常用的类型是db_table，即用一个数据库表作为图层。
* 为图层添加自定义属性，这些属性可用来查询， 在db_table类型图层中， 自定义属性就是数据表列。
* 向图层插入空间数据
* 根据业务系统需要， 根据空间查询条件和业务属性查询条件查询空间数据
* 返回数据并展现

## 空间数据库功能的调用方式

MapTalks在rest模块中用HTTP RestFul API接口的形式提供服务。

实际应用中可以通过以下几种方式调用：

* 通过HTTP接口直接调用， 例如通过浏览器的Ajax请求、各语言的HTTP客户端程序等。
* 通过客户端SDK开发包
    * [JAVA客户端](https://github.com/MapTalks/maptalks.java)
    * [Javascript(Browser/Node.js)客户端](https://github.com/MapTalks/maptalks.client.js)

## 空间库类型

目前MapTalks支持下表中几种空间库类型，从文件系统到MongoDB(未来会扩展更多的数据源)， 经过MapTalks的封装在使用上没有太大的区别。

但不同类型空间库的属性查询条件语法会有不同， 具体如表中所示。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>类型</th>
      <th>
         说明
      </th>
      <th>
         查询语句语法
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class="setting">
      <td>
        <p class="name">File</p>
        <p class="description">本地文件</p>
      </td>
      <td class="align-center">
        <p class="description">基于本地文件系统的空间数据库， 只读</p>
      </td>
      <td class="align-center">
        <p class="description">javascript</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name">SQL</p>
        <p class="description">SQL数据库</p>
      </td>
      <td class="align-center">        
        <p class="description">基于SQL数据库的空间数据库， 支持：</p>
        <p class="description">SQLite/Spatialite, MySQL, PostgreSQL/PostGIS, MS SQL Server, Oracle, DB2</p>
      </td>
      <td class="align-center">
        <p class="description">SQL</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name">Mongo</p>
        <p class="description">MongoDB数据库</p>
      </td>
      <td class="align-center">        
        <p class="description">基于MongoDB数据库的空间数据库</p>        
      </td>
      <td class="align-center">
        <p class="description">MongoDB</p>
      </td>
    </tr>
   </tbody>
</table>
</div>

## 功能说明

### 空间库初始化

空间库初始化的目的是在数据库中创建必要的配置表, 包括:
* 包含版本号, 坐标参考系(CRS)等必要配置属性的配置表
* 记录图层的图层表

例如我们想在MySQL数据库中创建一个空间库， 步骤如下：

* 在MySQL中创建一个数据库， 例如 testdb
```sql
CREATE DATABASE testdb;
```
* 参考[这里](configuration-db.html)， 在config.json配置文件中增加对testdb的连接实例
* 调用MapTalks的rest服务接口， 初始化空间库， 以调用java sdk为例：
```java
//host MapTalks服务的主机
//port MapTalks服务的端口号
//空间库， 即config.json中数据库连接实例的name
MapDatabase db = new MapDatabase("localhost",8090,"testdb");
//采用GCJ02作为默认的坐标参考系
db.install(new InstallSettings(CRS.GCJ02));
```

### 图层管理

图层， 是一个空间数据的集合， 空间库中的空间数据都通过图层来组织。

图层有多种类型， 可能是只读或者可读写， 如下表所示：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>类型</th>
      <th>说明</th>
      <th>空间库类型</th>
      <th>性质</th>
    </tr>
  </thead>
  <tbody>
    <tr class="setting">
      <td>
        <p class="name">db_table</p>
        <p class="description">数据表图层</p>
      </td>
      <td class="align-center">
        <p class="description">最常用的图层， 在SQL数据库中为数据表， 在MongoDB中为Collection</p>
      </td>
      <td class="align-center">
        <p class="description">SQL数据库, MongoDB</p>        
      </td>
      <td class="align-center">        
        <p class="description">读写</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name">db_view</p>
        <p class="description">视图图层</p>
      </td>
      <td class="align-center">        
        <p class="description">基于SQL数据库的空间数据库， 支持：</p>
        <p class="description">SQLite/Spatialite, MySQL, PostgreSQL/PostGIS, MS SQL Server, Oracle, DB2</p>
      </td>
      <td class="align-center">
        <p class="description">SQL</p>
      </td>
      <td class="align-center">        
        <p class="description">只读</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name">db_spatial_table</p>
        <p class="description">空间索引表图层</p>
      </td>
      <td class="align-center">
        <p class="description">如果数据库支持空间索引技术，可利用其内建的空间索引表作为图层表</p>
      </td>
      <td class="align-center">
        <p class="description">支持空间索引技术的SQL数据库, MongoDB</p>
      </td>
      <td class="align-center">        
        <p class="description">读写</p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name">db_spatial_view</p>
        <p class="description">空间索引视图图层</p>
      </td>
      <td class="align-center">
        <p class="description">和空间索引表图层一样，只是图层基于视图建立， 是只读的</p>
      </td>
      <td class="align-center">
        <p class="description">支持空间索引技术的SQL数据库</p>
      </td>
      <td class="align-center">        
        <p class="description">只读</p>
      </td>
    </tr>
   </tbody>
</table>
</div>

---
layout: docs
title: RestFul接口
permalink: /rest-api/
---

输入数据编码格式（针对POST、PUT方法）: x-www-form-urlencoded

# 空间数据库 #

## 获取空间库信息 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>GET</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "data": {
                    "version": 1.0,
                    "crs": {
                        "type": "proj4",
                        "properties": {
                            "proj": "+proj=longlat +datum=GCJ02"
                        }
                    }
                }
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 安装配置空间库 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}?op=install</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>settings=[string]: 设置参数<code>
                <br>
                例如：
                <code>
                {
                    "crs": {
                        "type": "proj4",
                        "properties": {
                            "proj": "+proj=longlat +datum=GCJ02"
                        }
                    }
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 获取图层列表信息 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>GET</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "id": "id",
                        "name": "name",
                        "type": "db_table",
                        "source": "source",
                        "fields": [
                            {
                                "fieldName": "field name",
                                "fieldsize": 20,
                                "dataType": "VARCHAR",
                                "decimalSize": 0,
                                "notNull": 1
                            }
                        ]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 创建图层 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers?op=create</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>data=[string]: 图层参数<code>
                <br>
                例如：
                {
                    "id": "id",
                    "name": "name",
                    "type": "db_table",
                    "source": "source",
                    "fields": [
                        {
                            "fieldName": "field name",
                            "fieldsize": 20,
                            "dataType": "VARCHAR",
                            "decimalSize": 0,
                            "notNull": 1
                        }
                    ]
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 获取图层信息 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>GET</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
                {
                    "success": true,
                    "count": 1,
                    "data": [
                        {
                            "id": "id",
                            "name": "name",
                            "type": "db_table",
                            "source": "source",
                            "fields": [
                                {
                                    "fieldName": "field name",
                                    "fieldsize": 20,
                                    "dataType": "VARCHAR",
                                    "decimalSize": 0,
                                    "notNull": 1
                                }
                            ]
                        }
                    ]
                }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 更新图层 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}?op=update</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
       </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>data=[string]: 图层参数<code>
                <br>
                例如：
                {
                    "id": "id",
                    "name": "name",
                    "type": "db_table",
                    "source": "source",
                    "fields": [
                        {
                            "fieldName": "field name",
                            "fieldsize": 20,
                            "dataType": "VARCHAR",
                            "decimalSize": 0,
                            "notNull": 1
                        }
                    ]
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 删除图层 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}?op=remove</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 获取图层字段列表信息 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/fields</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>GET</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "fieldName": "field name",
                        "fieldsize": 0,
                        "dataType": "INT",
                        "decimalSize": 8,
                        "notNull": 1
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 创建图层字段 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/fields?op=create</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>data=[string]: 图层字段参数<code>
                <br>
                例如：
                {
                    "fieldName": "field name",
                    "fieldsize": 20,
                    "dataType": "VARCHAR",
                    "decimalSize": 0,
                    "notNull": 1
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 更新图层字段 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/fields/{field}?op=update</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
            <p>
                <code>field=[string]: 字段名</code>
                <br>
                例如：field1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>data=[string]: 图层字段参数<code>
                <br>
                例如：
                {
                    "fieldName": "field1",
                    "fieldsize": 50,
                    "dataType": "VARCHAR",
                    "decimalSize": 0,
                    "notNull": 0
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 删除图层字段 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/fields?op=remove</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
            <p>
                <code>field=[string]: 字段名</code>
                <br>
                例如：field1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 增加图层数据 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=create</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>crs=[json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=GCJ02"
                    }
                }
                </code>
            </p>
            <p>
                <code>data=[json|json array]: 数据的JSON表达</code>
                <br>
                例如：
                <code>
                {
                    "type": "Feature",
                    "geometry": {
                        "type": "Polygon",
                        "coordinates": [[
                            [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                        ]]
                    }
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 查询图层数据 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=query</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>condition=[string]: 查询条件</code>
                <br>
                例如：prop1='hello'
            </p>
            <p>
                <code>spatialFilter=[json]: 空间过滤条件</code>
                <br>
                例如：
                <code>
                {
                    // RELATION_WITHIN
                    relation: 5,
                    geometry: {
                        type: 'Polygon',
                        coordinates: [
                            [ [-120.0, 84.0], [120.0, 84.0], [120.0, -84.0], [-120.0, -84.0], [-120.0, 84.0] ]
                        ]
                    }
                }
                </code>
            </p>
            <p>
                <code>fields=[string]: 返回字段列表</code>
                <br>
                例如：prop1,prop2
            </p>
            <p>
                <code>returnGeometry=[bool]: 是否返回Geometry，默认true</code>
                <br>
                例如：false
            </p>
            <p>
                <code>resultCRS=[string|json]: 返回数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
            <p>
                <code>page=[int]: 页编号，从0开始</code>
            </p>
            <p>
                <code>count=[int]: 每页数量</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "data": [
                    {
                        "type": "Feature",
                        "id": "fid",
                        "geometry": {
                            "type": "Polygon",
                            "coordinates": [[
                                [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                            ]]
                        }
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 查询图层数据数量 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=count</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>condition=[string]: 查询条件</code>
                <br>
                例如：prop1='hello'
            </p>
            <p>
                <code>spatialFilter=[json]: 空间过滤条件</code>
                <br>
                例如：
                <code>
                {
                    // RELATION_WITHIN
                    relation: 5,
                    geometry: {
                        type: 'Polygon',
                        coordinates: [
                            [ [-120.0, 84.0], [120.0, 84.0], [120.0, -84.0], [-120.0, -84.0], [-120.0, 84.0] ]
                        ]
                    }
                }
                </code>
            </p>
            <p>
                <code>fields=[string]: 返回字段列表</code>
                <br>
                例如：prop1,prop2
            </p>
            <p>
                <code>returnGeometry=[bool]: 是否返回Geometry，默认true</code>
                <br>
                例如：false
            </p>
            <p>
                <code>resultCRS=[string|json]: 返回数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 0,
                "data": 145
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 删除图层数据 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=remove</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>condition=[string]: 查询条件</code>
                <br>
                例如：id='fid'
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 删除所有图层数据 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=removeAll</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 更新图层数据 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=update</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>crs=[json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=GCJ02"
                    }
                }
                </code>
            </p>
            <p>
                <code>condition=[string]: 查询条件</code>
                <br>
                例如：id='fid'
            </p>
            <p>
                <code>data=[json]: 数据的JSON表达</code>
                <br>
                例如：
                <code>
                {
                    "type": "Feature",
                    "id": "fid",
                    "geometry": {
                        "type": "Polygon",
                        "coordinates": [[
                            [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                        ]]
                    }
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 更新图层数据属性 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/sdb/databases/{db}/layers/{layerid}/data?op=updateProperties</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>
            <p>
                <code>db=[string]: 数据库名字</code>
                <br>
                例如：db1
            </p>
            <p>
                <code>layerid=[string]: 图层ID</code>
                <br>
                例如：layer1
            </p>
        </td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>condition=[string]: 查询条件</code>
                <br>
                例如：id='fid'
            </p>
            <p>
                <code>data=[json]: 新的属性</code>
                <br>
                例如：
                <code>
                {
                    "prop1": "new string",
                    "prop2": 99
                }
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {"success": true}
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

# 空间计算 #

## 计算空间关系 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/relation</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>source=[json]: 源Geometry</code>
                <br>
                例如：
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                    ]]
                }
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                    ]]
                }
                ]
                </code>
            </p>
            <p>
                <code>relation=[int]: 空间关系</code>
                <br>
                <ul>
                    <li>0: INTERSECT</li>
                    <li>1: CONTAINS</li>
                    <li>2: DISJOINT</li>
                    <li>3: OVERLAP</li>
                    <li>4: TOUCH</li>
                    <li>5: WITHIN</li>
                    <li>100: INTERCT NOT CONTAIN</li>
                    <li>101: CONTAIN CENTER</li>
                    <li>102: CENTER WITHIN</li>
                </ul>
                <br>
                例如：
                <code>
                0
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [true]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算缓冲区域 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/buffer</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>distance=[int]: 缓冲距离(米)</code>
                <br>
                例如：100
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "Polygon",
                        "coordinates": [
                            [
                                [-5.000901746702559, -4.999999999999995],
                                [-5.000901746702559, 15.000000000000009],
                                [-5.000884419892522, 15.00016992758842],
                                [-5.000833105322004, 15.000333324827546],
                                [-5.000749774981172, 15.000483912475017],
                                [-5.000637631208292, 15.00061590356473],
                                [-5.000500983625666, 15.000724225791759],
                                [-5.00034508352326, 15.000804716432302],
                                [-5.00017592205458, 15.00085428230896],
                                [-5.0, 15.000871018654735],
                                [15.000000000000002, 15.000871018654735],
                                [15.00017592205458, 15.00085428230896],
                                [15.000345083523259, 15.000804716432302],
                                [15.000500983625665, 15.000724225791759],
                                [15.000637631208292, 15.00061590356473],
                                [15.000749774981173, 15.000483912475017],
                                [15.000833105322004, 15.000333324827546],
                                [15.000884419892524, 15.00016992758842],
                                [15.00090174670256, 15.000000000000009],
                                [15.00090174670256, -4.999999999999995],
                                [15.000884419892524, -5.000175252594602],
                                [15.000833105322004, -5.000343770286034],
                                [15.000749774981173, -5.000499077041541],
                                [15.000637631208292, -5.000635204520962],
                                [15.000500983625665, -5.0007469214350415],
                                [15.000345083523259, -5.000829934578821],
                                [15.00017592205458, -5.000881053815117],
                                [15.000000000000002, -5.000898314667969],
                                [-5.0, -5.000898314667969],
                                [-5.00017592205458, -5.000881053815117],
                                [-5.00034508352326, -5.000829934578821],
                                [-5.000500983625666, -5.0007469214350415],
                                [-5.000637631208292, -5.000635204520962],
                                [-5.000749774981172, -5.000499077041541],
                                [-5.000833105322004, -5.000343770286034],
                                [-5.000884419892522, -5.000175252594602],
                                [-5.000901746702559, -4.999999999999995]
                            ]
                        ]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算相交性 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/intersection</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>source=[json]: 源Geometry</code>
                <br>
                例如：
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                    ]]
                }
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, 10.0], [10.0, 10.0], [10.0, -5.0], [-5.0, -5.0], [-5.0, 10.0]
                        ]]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算凸包 ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/convexhull</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0], [-5.0, -5.0]
                        ]]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算Union ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/union</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>source=[json]: 源Geometry</code>
                <br>
                例如：
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                    ]]
                }
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [10.0, -5.0], [10.0, -10.0], [-10.0, -10.0], [-10.0, 10.0],
                            [-5.0, 10.0], [-5.0, 15.0], [15.0, 15.0], [15.0, -5.0], [10.0, -5.0]
                        ]]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算Difference ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/difference</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>source=[json]: 源Geometry</code>
                <br>
                例如：
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                    ]]
                }
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [10.0, -5.0], [10.0, -10.0], [-10.0, -10.0], [-10.0, 10.0],
                            [-5.0, 10.0], [-5.0, -5.0], [10.0, -5.0]
                        ]]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

## 计算SymDifference ##
<div>
<table><tbody>
    <tr>
        <td>URL</td>
        <td>/rest/geometry/symdifference</td>
    </tr>
    <tr>
        <td>请求方法</td>
        <td>POST</td>
    </tr>
    <tr>
        <td>路径参数</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>数据参数</td>
        <td>
            <p>
                <code>source=[json]: 源Geometry</code>
                <br>
                例如：
                {
                    "type": "Polygon",
                    "coordinates": [[
                        [-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, 10.0]
                    ]]
                }
            </p>
            <p>
                <code>targets=[json array]: 目标Geometry数组</code>
                <br>
                例如：
                <code>
                [
                    {
                        "type": "Polygon",
                        "coordinates": [[
                            [-5.0, -5.0], [15.0, -5.0], [15.0, 15.0], [-5.0, 15.0]
                        ]]
                    }
                ]
                </code>
            </p>
            <p>
                <code>crs=[string|json]: 数据的CRS</code>
                <br>
                例如：
                <code>
                {
                    "type": "proj4",
                    "properties": {
                        "proj": "+proj=longlat +datum=BD09"
                    }
                }
                </code>
                <br>
                或者：
                <code>
                BD09
                </code>
            </p>
        </td>
    </tr>
    <tr>
        <td>请求成功的回应</td>
        <td>
            <code>
            {
                "success": true,
                "count": 1,
                "data": [
                    {
                        "type": "MultiPolygon",
                        "coordinates": [
                            [
                                [
                                    [10.0, -5.0], [10.0, -10.0], [-10.0, -10.0], [-10.0, 10.0], [-5.0, 10.0], [-5.0, -5.0], [10.0, -5.0]
                                ]
                            ],
                            [
                                [
                                    [10.0, -5.0], [10.0, 10.0], [-5.0, 10.0], [-5.0, 15.0], [15.0, 15.0], [15.0, -5.0], [10.0, -5.0]
                                ]
                            ]
                        ]
                    }
                ]
            }
            </code>
        </td>
    </tr>
    <tr>
        <td>请求失败的回应</td>
        <td>
            <code>
            {"success": false}
            </code>
        </td>
    </tr>
</tbody></table>
</div>

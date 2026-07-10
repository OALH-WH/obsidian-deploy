---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/sonic-mgmt-common/translib architecture/translib/","dg-note-properties":{}}
---

1. 常用API

1. BulkRequest：批量操作

1. 创建DB

1. 通过redisClients(db.go: 全局变量),数据库名（host,asic1,asic2...），数据库索引（4：configDB, 6: stateDB）获取一个对应redis客户端连接

1. 开启转换

1. 

1. 遍历所有删除请求

1. 遍历所有替换请求

1. 遍历所有更新请求

1. 遍历所有创建请求

1. 获取请求负载和请求路径

1. 通过路径和请求中的版本来获取AppModule（例如wss_app.go中的内容），返回一个appInterface and appInfo

1. appInfo通过appMap(app_interface.go: 全局变量)遍历查找path来获取

1. 判断客户侧请求版本是否和服务器兼容（version.go）

1. 底层逻辑

1. 在version.go: init函数中通过文件获取基础版本以及后续最后更新版本

1. 判断客户端请求版本是否在这个区间

1. 获取appInterface, 通过appInfo中的app类型

1. 根据app类型，用reflect创建一个app实例

1. 通过app实例得到他的接口函数

1. AppModule初始化

1. 执行app初始化操作

1. 

1. 提交转换
---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/sonic-mgmt-common/translib architecture/db/","dg-note-properties":{}}
---

1. 初始化所有redis客户端

1. clients

1. host

1. configDB: 4

1. stateDB: 6

1. counterDB: 2

1. historyDB: 10

1. asic

1. 常用结构体

1. Key

1. comp []string //存储redis2key获取到的键名，一般只有一个，即只会用到index=0

1. TableSpec

1. Name string

1. CompCt int

1. noDelete bool

1. DB

1. *redis.Client

1. *Options

1. *_txState

1. []_txCmd

1. *cvl.CVL

1. []cvl.CVLEditConfigData

1. redisClients map[string]map[DBNum]*DB

1. MDB map[string][MaxDB]*DB

1. NumberDB map[string]*DB

1. 常用API

1. db.go

1. startTx

1. 设置Tx状态为Watch

1. commitTx

1. GetKeys: 通过表名获取所有键

1. key2redis:通过表名和键连接成redis中完整的键值

1. GetEntry: 获取字段：值对

1. arg1: 表名

1. arg2:键名

1. doCVL：批处理hash字段值

1. 值列表和操作标识列表长度不相同会报错返回

1. 遍历操作列表，判断操作走不通逻辑

1. 更新or创建

1. 把要操作的数据添加到cvlEditConfigData中

1. 删除

1. 把要操作的数据添加到cvlEditConfigData中

1. 判断数据是否有效

1. doWrite：

1. 判断这个db是否支持写，不支持返回错误

1. 

1. ModEntry

1. 如果value为空，删除指定ts的key

1. 不为空则更新数据

1. dbs.go

1. NewNumberDB

1. 从redisClients(全局变量)获取redis连接客户端

1. 并通过numberDB直接指定，获取所有DBName的同一个n	umberDB的客户端连接

1. StartNumberDBTx

1. 调db.go: startTx

1. 
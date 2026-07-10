---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/OCM层/板卡适配之OCM层/","dg-note-properties":{}}
---

1. 预设板卡配置

1. MIB配置

1. slot mib添加新的板卡类型（需要改）

1. SLOT配置

1. 更改预设板卡类型为新板卡：设置slot 表的slotrequiredcardtype字段

1. 端口配置

1. 初始端口配置

1. ...

1. ocm module.c： port_table_add_default_cfg4slot函数中负责获取板卡端口配置，并初始化配置（需要改）

1. 获取板卡信息

1. 在ocm module.c: gOcmCardModel中添加对应板卡类型的端口配置（需要改）

1. 发生了创建端口表一条数据（设置了adminstatus和portmode）的事件

1. 根据端口表的设置，设置otuk表 //ocm otuk.c: otuk table port set（可能需要改，即端口模式有新增）

1. 根据端口表的设置，设置odukp表 //ocm odukp.c: odukp table port set	

1. 根据端口模式获取odu类型 //ocm odukp.c: getOduTypeFromPortType （可能需要改，即端口模式有新增）

1. 添加snc默认配置 //ocm model.c: add default cfg （需要改）

1. 后续端口配置

1. 如果端口模式发生更改，根据端口模式来更改其他配置比如odu，otu，snc等等

1. ODU默认配置

1. 根据端口表的设置，设置odukp表 //ocm odukp.c: odukp table port set

1. 添加一个odukp tp(时隙) （需要改）

1. 线路侧可能要添加子时隙（可能需要改，即需要解复用）

1. index

1. 机框，一般默认

1. 槽道

1. 子槽道，一般默认

1. 端口

1. 子端口，一般默认

1. 高odu类型

1. 高odu id

1. 低odu类型

1. 低odu id

1. SNC默认配置

1. 添加snc默认配置 //ocm model.c: 新板卡 add default cfg（需要改）

1. 新板卡 add port cfg //根据线路侧端口号添加

1. 添加默认SNC配置（需要改）

1. OTUK默认配置

1. 

1. 实际板卡配置
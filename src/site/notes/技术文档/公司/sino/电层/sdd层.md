---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/电层/sdd层/","dg-note-properties":{}}
---

1. sdd层负责模块(主要是linux线卡会走这个逻辑)

1. 板卡信息管理

1. sdd层管理板卡信息

1. sdd层中包括各个板卡类型的pollchanges

1. 

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E7%94%B5%E5%B1%82/images/WEBRESOURCE749474e46203e1b1e49abcd1ade992dcimage.png)

1. 全局变量

1. gpSddBoardData

1. dwPortNum：端口数量(sdd init.c: SDD_InitCard函数中获取，由cdh_main.c: CDH_InitCard中定义)

1. dwFPGABaseAddr: 板卡FPGA基地址

1. dwCPLDBaseAddr:板卡CPLD基地址

1. sPortCfp

1. bCfpMP：pollingchange中获取

1. eCfgPortMode: 端口模式

1. 文件

1. sdd_card.c：负责把对应板卡的配置和获取数据API集合跟gpSddBoardData[端口]->psCallback对应起来

1. sdd_main.c:sdd层主函数

1. sdd_SfpProcess:sfp模块相关进程

1. sdd_PollTask：死循环周期性获取模块信息

1. sdd_plugmodel.c：模块相关

1. sdd_plugSfpalarmprocess:sdd层告警上报相关函数（会调用sdd_plugSfpmismatch）

1. sdd_plugSfpmismatch:判断模块是否mismatch，并把结果放到gpSddBoardData全局变量中
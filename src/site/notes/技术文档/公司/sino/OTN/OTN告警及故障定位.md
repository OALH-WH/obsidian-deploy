---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/OTN/OTN告警及故障定位/","dg-note-properties":{}}
---

1. AIS（alarm indication signal）：告警指示信号

1. 层级：OTU、ODU、OAC：SDH业务

1. 主要目的：传递告警信息

1. 即上游业务失效的信息传递给下游

1. 或者是将服务层信号失效的信息传递给客户层

1. 特点：是要在所有层中透传的

1. 范围：也就是说从产生之初开始一直到所在层结束，都会有AIS告警

1. ODU AIS插入条件

1. 光层：LOS

1. OTU层：AIS、LOF、LOM、TTI失配

1. ODU层：LOF、LOM

1. 故障定位方法

1. 本业务方向失效

1. 故障点不在本检测点而应顺着业务流向向上游查找

1. 告警传递示例

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEf1859b01641cc39620d45f295d81c7e7image.png)

1. OCI（optical channel disconnect indication）：断开连接指示

1. 层级：ODU、OPU...

1. 主要目的：指示交叉连接的断开

1. 故障定位方法

1. 说明本业务的路径上游没有配交叉\交叉错误

1. 告警传递示例

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE3f4bcc06635ac0e50369ac02038f43d1image.png)

1. BDI（）：后向缺陷指示

1. 主要目的：指示反方向业务有失效的情况

1. 特点

1. 本方向业务是好的

1. 反方向业务失效了

1. OTU BDI插入条件

1. 

1. ODU BDI插入条件
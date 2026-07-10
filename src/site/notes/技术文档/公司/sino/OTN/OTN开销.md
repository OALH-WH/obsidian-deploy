---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/OTN/OTN开销/","dg-note-properties":{}}
---

1. OTU层

1. 开销组成

1. 7字节的开销（ODU层、OPU层也有）

1. 具体开销内容

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEbf435eab045b49cf94bfe0fdeee73fb4image.png)

1. 分析

1. SM：段检视开销

1. TTI（1 byte）：路径踪迹标示符

1. BIP-8（1 byte）：比特间插校验码

1. BEI\BIAE（4 bit）：后向差错指示\后向输入定位错误指示

1. BDI（1 bit）：后向缺陷指示

1. IAE（1 bit）：输入定位错误

1. RES（2 bit）：预留

1. GCC0：通用通信通道

1. RES：预留段

1. FEC纠错开销

1. 不做重点

1. ODU层

1. 开销组成（一共3*14字节组成）（最为重要的有两组，即3 bytes PM段， 3 bytes TCMi）

1. PM、TCMi开销示意图

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEae02c162b0b9591a357bc268f65a2bbdimage.png)

1. PM

1. TCMi

1. OPU层

1. 开销组成

1. PT：代表不同的业务映射类型

1. PSI

1. 与级联相关的开销

1. 与客户信号映射到OPUk相关的开销构成
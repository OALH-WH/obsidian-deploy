---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/光模块/标准文档/CMISS5/DPSM/","dg-note-properties":{}}
---

# 背景
## 缩写
- DP: Data Path
# DPInitialized State
- 这个状态是一个稳定状态
- 在这个状态下Data Path所有的功能资源都已经初始化了, 但是一个或者更多的Tx media lanes DP 停留在DPinitialized的输出要么被主机消除要么被disable, 所以DP 无法ready来传输流量
# OutputDisableTx
## TxDisablesModuleWide
- 0, 0x01, 151, bit 0, value: 0
	- Tx output disable is controlled per lane // 输出开关光由每条lane决定
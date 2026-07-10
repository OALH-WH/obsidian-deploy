---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/常见板卡/T4QEH(P350C)/常见标准配置和性能/link state/","dg-note-properties":{}}
---

# 背景
- **link down**
	- 物理link down
		- 交换机和客户侧模块之间物理链路一种状态
	- 协议link down
		- 就是此link state所表示的一种状态
# 状态     
- 软件自定义状态, 表示业务的好坏, 不依赖模块寄存器
- 值的类型 (open config定义)
	- up
		- 阿里需求: 无业务告警
	- down
		- 阿里需求: 有业务告警
	- testing
		- **阿里需求**: 配置了PRBS的状态
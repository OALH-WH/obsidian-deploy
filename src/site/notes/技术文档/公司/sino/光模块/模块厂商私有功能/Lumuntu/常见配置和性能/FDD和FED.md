---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/光模块/模块厂商私有功能/Lumuntu/常见配置和性能/FDD和FED/","dg-note-properties":{}}
---

# 背景
- 针对性能 `Pre-FEC-ber`的阈值, 参考[[技术文档/业内知识/光通信/常见配置和性能/Pre-FEC-Ber (前向纠错前误码率)\|Pre-FEC-Ber (前向纠错前误码率)]]
- `fdd`: 用于表示FEC检测到的media侧接收到ber劣化阈值, 参考[[技术文档/公司/sino/光模块/模块厂商私有功能/Lumuntu/告警/FLEXO RX FEC SD告警\|FLEXO RX FEC SD告警]]
- `fed`: 用于表示FEC检测到的media侧接收到ber过度劣化阈值, 参考[[技术文档/公司/sino/光模块/模块厂商私有功能/Lumuntu/告警/FLEXO RX FEC SF告警\|FLEXO RX FEC SF告警]]
# 参考
- [[技术文档/公司/sino/光模块/模块厂商私有功能/Lumuntu/参考文档/寄存器文档\|寄存器文档]]
- `page 30h, addr 160-168`
# 注意
- 配置FDD和FED时, 要确保FedEnable和FddEnable是打开的
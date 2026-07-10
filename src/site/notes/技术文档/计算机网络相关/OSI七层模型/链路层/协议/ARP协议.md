---
{"dg-publish":true,"permalink":"/技术文档/计算机网络相关/OSI七层模型/链路层/协议/ARP协议/","dg-note-properties":{}}
---

# 背景
全称`Address Resolution Protocal`, 地址解析协议
用来向局域网广播`ARP`帧, 在本地动态维护一个`ARP`表

# 作用
- **数据包转发**：交换机、路由器依靠ARP表确定将数据帧转发到哪个物理端口。
- **网络诊断**：`arp`命令可用于排查IP地址冲突或MAC地址异常问题。
- **安全风险（ARP欺骗）**：攻击者可以伪造ARP响应，篡改ARP表，将流量劫持到自己的机器（中间人攻击）。防护方法包括使用静态ARP条目或部署ARP防护软件。
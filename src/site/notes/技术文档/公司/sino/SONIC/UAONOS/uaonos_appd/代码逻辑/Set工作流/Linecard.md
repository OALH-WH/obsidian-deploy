---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/UAONOS/uaonos_appd/代码逻辑/Set工作流/Linecard/","dg-note-properties":{}}
---

# 基本步骤
- 检测redis config db变化
- 调用注册在下述位置的函数进行对应的处理
	- linecard.cpp: Linecard::Linecard(): REGISTER_HANDLER(...);
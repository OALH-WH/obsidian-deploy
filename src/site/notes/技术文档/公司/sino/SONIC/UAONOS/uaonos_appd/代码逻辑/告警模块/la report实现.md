---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/UAONOS/uaonos_appd/代码逻辑/告警模块/la report实现/","dg-note-properties":{}}
---

# 背景
# 实现
## `la.cpp:la::report()`
### 第一个流程
- 如果 `flag`有NALM, 则 `goto done`
- 如果 `flag`有FORCE, 则 直接进入report流程
- 如果 `flag`有SUPPRESSING
	- 如果 `flag`有SHOULD_REPORT
	- 如果 `flag`有ACTIVE, 则走done流程
### report流程
### done流程
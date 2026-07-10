---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/UAONOS/uaonos_appd/代码逻辑/告警模块/la check实现/","dg-note-properties":{}}
---

# 背景
- `la.cpp`: 提供具体的告警check实现
	- `eg. la_int_singular::check()`
	- `eg. la_threshold::check()`
# 实现
## `la_int_singular::check()`
### 作用
- 判断 `int_get_`指向的函数结果是否和 `expect_`相等
	- 相等: 不上报
	- 不相等: 上报
---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/系统相关/系统时间相关/date命令/","dg-note-properties":{}}
---

# 基本格式
`date [OPTIONS] [+<FORMAT>]`

**参数**

**格式符**
- `%s`: 小写, 表示时间戳
- `%S`: 大写, 表示秒数
- `%Y`: `year`, 表示年份
- `%m`: `month`, 表示月份
- `%d`: `day`, 表示天数

**示例**
- `eg. date "+%Y-%m"`
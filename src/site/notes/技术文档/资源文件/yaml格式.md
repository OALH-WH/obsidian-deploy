---
{"dg-publish":true,"permalink":"/技术文档/资源文件/yaml格式/","dg-note-properties":{}}
---

# 参考
- [yaml](https://www.runoob.com/w3cnote/yaml-intro.html)
# 基本语法
 - 大小写敏感
- 使用缩进表示层级关系
- 缩进不允许使用 tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- # 表示注释
- : 号后面要加空格
# YAML数据类型
## YAML对象
### 基本格式
- `key: value`
## YAML数组
### 基本格式
```YAML
- A
- B
- C
# 或者
[A, B, C]
```

## YAML纯量
纯量是最基本的，不可再分的值，包括：
- 字符串
- 布尔值
- 整数
- 浮点数
- Null
- 时间
- 日期

---
{"dg-publish":true,"permalink":"/技术文档/资源文件/json格式/","dg-note-properties":{}}
---

1. 常用工具

1. jq命令

1. 语法

1. 用.表示当前对象

1. 实例

1. 把多个json文件合成一个

1. jq -s ‘add’ file1 file2... > tar_file

1. 向json中添加元素

1. eg. jq ' .LINECARD.LINECARD += {"test": "123"}' < config.json > config.json.temp
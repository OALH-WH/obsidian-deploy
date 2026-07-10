---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/脚本工具/compile_command文件生成/","dg-note-properties":{}}
---

# 通过源码自带生成脚本实现
## 步骤
- 源码根目录下执行下述命令
	- `python3 ./scripts/gen_compile_commands.py`
- 源码根目录会生成`compile_commands.json`
# bear命令实现
## 步骤
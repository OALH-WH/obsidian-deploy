---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/Shell配置相关/set命令/","dg-note-properties":{}}
---

# 作用
- 设置或取消设置`shell`的选项和位置参数的值
# 参数
- `-o`
- `+o`
# 实例
## 关闭vi的Esc响应
- 配置
	- `set +o vi`
- 查看
	- `set -o | grep vi` 
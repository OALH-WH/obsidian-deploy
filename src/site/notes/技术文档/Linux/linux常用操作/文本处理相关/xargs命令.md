---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文本处理相关/xargs命令/","dg-note-properties":{}}
---

# 背景
- `|`管道符的作用
# 基本格式
- `| xargs <COMMAND>`
# 参数
- `-L <NUMBER>`: 从标准输入里读`NUMBER`行, 拼成一次给`COMMAND`执行
	- `eg. cmd | xargs -L 1 echo`: 假如`cmd`的结果为`a\nb\nc`, 则这个示例的运行结果为:<br>`a`<br>`b`<br>`c`
- `-i`: 指定`xargs`命令解析读取数据的占位符为`{}`
	- `eg. cmd | xargs -i echo "{}"`
- `-I <PLANCEHOLDER>`: 指定`xargs`命令解析读取数据的占位符, 不使用`-I/i`, 解析的字符默认拼在最后
	- `eg. cmd | xargs -I {} echo "{}"`
## 注意
- `-L`和`-I/i`不能一起用, `-I/i`会隐式开启`-L 1`
# 实例
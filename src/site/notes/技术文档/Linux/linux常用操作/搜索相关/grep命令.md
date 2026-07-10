---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/搜索相关/grep命令/","dg-note-properties":{}}
---

# 基本格式
- `grep [options] <pattern>`
# 常见参数
- `-v`: 反选匹配输出, 即不输出匹配的行
- `-i`: 忽略大小写匹配
- `-o`: 使用正则匹配
- `-r`: 递归搜索
- `--color=auto`: 设置匹配字符的颜色为`auto`
- `--include=<file type>`: 筛选从哪些文件里查找, `eg. *.h`
- `--exclude=<file type>`: 筛选不查找哪些文件, `eg. *.md`
- `-I, --binary-files=without-match`: 忽略二进制文件, 即不查找二进制文件的内容
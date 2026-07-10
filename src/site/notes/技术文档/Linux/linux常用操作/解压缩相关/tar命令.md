---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/解压缩相关/tar命令/","dg-note-properties":{}}
---

# 背景
- 仅归档文件: 即`.tar`后缀文件
	- 把多个文件归档成一个文件
- 仅压缩文件, `eg. .gz .xz`后缀文件
	- 只能压缩单个文件, 不能压缩目录
- 归档+压缩, `eg. .tar.gz .tar.xz`后缀文件
	- 先归档为一个文件, 再压缩
- 同时完成归档和压缩, `eg. zip`后缀文件
# 作用

# 参数
- `-c`: 创建归档文件
- `-x, --extract, --get <archive file>`: 表示从归档\[压缩]文件中提取文件
- `-v, --verbose`: 表示输出详细的执行信息
- `-t, --list <archive file>`: 查看归档\[压缩]文件的目录结构和文件
- `-f <archive file>, --file=<archive file>`: 表示使用归档文件
	- 如果是归档后的压缩文件, 会根据`eg. -z`参数或者内部自协商自动压缩/解压文件内容
- `-z, --gzip, --gunzip, --ungzip`: 表示通过gzip过滤归档文件, 即.gz文件
- `-C <DIR>, --directory=DIR`: 用于指定解压到指定目录
- `--strip-components=<NUM>`: 选择性解压指定目录下的内容
	- `eg. tar -xzvf  vscode-server.tar.gz --strip-components=1  -C .vscode-server/bin/8761a5560cfd65fdd19ce7e2bd18dab5c0a4d84e` : 只解压顶层目录下的内容, 不包括顶层目录
# 常用示例
## 归档
```shell
tar -czvf <ARCH FILE> <FILES>
```
## 解压
```shell
tar -xzvf <ARCH FILE>
```

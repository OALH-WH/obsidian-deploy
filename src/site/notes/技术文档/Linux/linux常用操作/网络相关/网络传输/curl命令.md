---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/网络传输/curl命令/","dg-note-properties":{}}
---

# 背景
- 重定向: HTTP协议中的一个重要机制, 它允许服务器告诉客户端：“你要的资源不在这个地址，我已经把它移到了另一个地址，请去那里获取
- 基于HTTP/HTTPS协议
# 基本格式
- `curl [options] [URL]`
**参数**
- `--proxy <your proxy>`: 指定访问URL的代理, `eg. http://192.168.1.100:7890`
- `-o <custom file name>`: 访问内容输出到指定文件
- `-O`: 使用远程文件名保存
- `-v`: 在访问过程中, 输出更详细的日志
- `-f`: 请求失败时, 不输出错误页面, 而返回错误码
- `-s`: 小写, 开启静默模式, 不显示进度信息和错误信息
- `-S`: 大写, 一般和`-s`配合使用, 用来在发生错误时仍显示错误信息, 方便调试
- `-L`: 跟随重定向, 很多软件下载链接会使用重定向(参考[[技术文档/Linux/linux常用操作/网络相关/网络传输/curl命令#背景\|#背景]]), 需要自动跟随到另外的地址获取
- `-u <username:password>`: 指定访问的用户密码
- `-X, --request <GET | PUT | ...>`: 指定请求方法, 如 `GET`、`POST`、`PUT`、`DELETE`、`PATCH` 等
- `-H, --header <field: value>`: 指定请求头信息
- `-d <payload>`: 指定请求体
# 实例
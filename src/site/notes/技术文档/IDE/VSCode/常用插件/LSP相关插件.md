---
{"dg-publish":true,"permalink":"/技术文档/IDE/VSCode/常用插件/LSP相关插件/","dg-note-properties":{}}
---

# clangd插件
- 用于使用宿主机的`clangd`语言服务器
## 依赖
- 宿主机需要安装`clangd`服务
## 配置
### settings.json
- `clangd.enable`: 使能插件
- `clangd.path`: `clangd`服务程序的路径
- `clangd.fallbackFlags`: 指定编译器选项
- `clangd.arguments`: 服务启动参数, 参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/编译器的使用/clang/clang_clang++\|clang_clang++]]和[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/语言服务器(LSP)/clangd服务\|clangd服务]]
## 调试输出
# C/C++ GNU Global插件
- 用于使用宿主机的`gtags`生成的静态索引实现跨文件的跳转
## 依赖
- 需要安装`gtags`, 参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/语言服务器(LSP)/gtags命令\|gtags命令]]
## 配置
### settings.json
- ``
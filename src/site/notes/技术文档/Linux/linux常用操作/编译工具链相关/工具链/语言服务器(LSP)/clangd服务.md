---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/语言服务器(LSP)/clangd服务/","dg-note-properties":{}}
---

# 背景
- `sysroot`: 编译依赖的系统库头文件和系统库在交叉编译工具链中的路径
	- 比如`stdio`, `unistd`这些都是Linux系统的系统库头文件
	- 像`libc`, `libc++`都是系统库
	- 参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/编译器的使用/GCC_G++#参数\|GCC_G++#参数]]
# 下载安装
## 包管理器
## 从源码
### 参考
- https://llvm.org/docs/CMake.html
### 下载
- `git clone https://github.com/llvm/llvm-project.git`
### 编译
- 
# 依赖
# 配置
## .clangd
### 参考
- [配置官方文档](https://clangd.llvm.org/config.html#compileflags)
- [[技术文档/资源文件/yaml格式\|yaml格式]]
### 基本格式
```yaml
CompileFlags:
	Add:
	Remove:
	Compiler: clang++
	CompilationDatabase: .
	Threads: 2
	Background: Build
```
### 字段解析
- `CompileFlags`: 添加`clang`编译器的选项, 参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/编译器的使用/clang/clang_clang++\|clang_clang++]]
	- `CompilationDatabase: .`: 表示就在当前目录查找`compile_commands.json`
	- `Compiler`: 如果和`clangd`服务启动选项`--query-driver`指定的一样, 则使用这个编译器来解析包含的路径
- `Index`
	- `Threads`: 指定使用的线程
	- `Background`:指定后台构建索引的策略
		- `Build`: 表示默认
		- `Skip`: 不使用后台策略
- `If`
	- `PathMatch`: 指定索引目录, 支持**正则匹配**
		- `eg. - driver/net/.*`
## compile_command.json
- 聚合多个项目自动生成的`compile_command.json`
- 必须是高版本才能支持
### 位置
### 基本格式
```json
[
    {

        "directory": "...",

        "file": "...",

        "include": "..."

    }
]
```
### 字段解析
- `directory`: 项目绝对路径
- `file`: 相对于`directory`的`compile_commands.json`路径, 也可以是绝对路径
- `include`: 自动生成的`compile_command.json`路径
	- 可以是**相对于聚合文件所在目录**填写**相对路径**
	- 可以是**绝对路径**
# 服务启动参数
会覆盖`.clangd`配置文件中的配置
- `-compile-commands-dir=<string>`: 指定`compile_commands.json`文件的同级目录
- `--query-driver=<string[,string2]>`: 指定实际使用的编译器路径, 可指定多个, 用于查找系统头文件路径
- ``
# 问题
## 找不到标准库头文件
### 原因
- `clangd`只能使用自己内置的`clang`引擎来解析代码, 而不是外部的编译器
- 如果是交叉编译, 可以在`.clangd`中手动指定架构和`sysroot`, 但一般clangd会自动从`compile_commands.json`中获取
	- 如何获取`sysroot`路径?
	- 如何获取架构?
## 报错unknow argument
### 原因
- compile_commands.json中存在gcc专属参数, clangd无法识别
### 解决
- 配置`.clangd`文件忽略报错参数
# 实例



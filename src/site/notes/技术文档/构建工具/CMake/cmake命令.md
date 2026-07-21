---
{"dg-publish":true,"permalink":"/技术文档/构建工具/CMake/cmake命令/","dg-note-properties":{}}
---

1. 查看所有环境变量
2. cmake -E environment

# 基本格式

**可选参数**
- `--build <build dir>`： 生成makefile，并构建所有目标（会执行make）
- `--target <target name>`： 编译指定目标 //可通过`cmake --build ./build --target help`查看, 一般参考[[技术文档/构建工具/CMake/CMake语法#三、 构建目标 (Target) 操作\|CMake语法#三、 构建目标 (Target) 操作]]
- `-B <build dir>`：指定构建目录，一般为build
- `-S <src dir>`：指定源代码路径, 源代码路径指的是**包含项目顶层 `CMakeLists.txt` 的目录**。这个目录通常包含你的所有源代码和头文件，但更重要的是，它是 CMake 解析整个项目的起点。
- `-G <generator-name>` //生成器列表可见--help
- `-E environment`: 查看所有环境变量
- `-D<VAR>`: 给变量赋值, 会被`CMakeLists.txt`文件覆盖, 一般用于构建配置阶段
	- 比如`--build`命令, 执行构建目标的时候, 不能用此参数
---
4. 

5. 常见生成器

6. Ninja

7. 优点

8. 小巧高效

9. MinGW Makefiles

10. Unix Makefiles

11. -D<变量名>=<值>：用来给变量赋值
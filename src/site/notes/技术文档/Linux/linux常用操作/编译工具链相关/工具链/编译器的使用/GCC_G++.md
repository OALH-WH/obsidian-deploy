---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/编译器的使用/GCC_G++/","dg-note-properties":{}}
---

# 背景
## `sysroot`
**基本概念**
虚拟的目标执行机器上的根目录

**核心目的**
- **架构隔离（防止冲突）**：确保链接器和编译器只看到适合目标 CPU（如 ARM、RISC-V）的头文件和库，而不是宿主机的（x86）文件。
- **依赖完整性**：嵌入式 Linux 开发板的文件系统（rootfs）往往被裁剪过。Sysroot 就是这份裁剪后文件系统的副本，确保程序链接时找到的库版本，与开发板上实际存在的库版本完全一致。
- **独立构建环境**：即使你在同一台电脑上编译多个不同项目的固件，每个项目都可以有自己的 Sysroot，互不干扰

**目录结构**
这个文件夹下通常会有:
- `usr`
	- `include`
	- `lib`
- `lib`
- `etc`
- `...`

**总结一句话**：**Sysroot 就是目标机器的文件系统骨架，用来欺骗编译器和链接器，让它们以为自己正在目标机器上直接编译**
# 参数
- `-c`: 编译成目标文件，即.o文件
- `-v`: 查看编译器信息
- `--print-file-name=<file name>`: 输出编译器内部配置中某个特定库文件或者目标文件的完整存储路径
- `--print-search-dirs`: 打印链接器将查找库的完整目录列表(**包括标准系统目录**)
{ #c9179c}

- `-O0`: 大写字母, 完全关闭代码优化, 防止编译器优化修改代码逻辑
- `-I`: 指定搜索的头文件目录
	- 头文件搜索路径(**按高优先级递减排序**)
		- 
- `-l`: 指定要链接的库名
	- 格式`eg. -lpthread`, 不需要加`lib`前缀和`.so/.a`后缀
	- 库文件搜索路径(**按高优先级递减排序**)
		- `-L`参数指定的目录
		- 环境变量`LIBRARY_PATH`指定的目录
		- 标准系统库目录中查找, 例如`eg. /lib /usr/lib /usr/local/lib`, 具体的参考下述方法
			- [[技术文档/Linux/linux常用操作/编译工具链相关/工具链/编译器的使用/GCC_G++#^c9179c\|查看编译器完整的搜索路径]]
			- 链接器搜索路径配合`grep`命令查看, 参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/链接器的使用/链接器#^4eb062\|链接器#^4eb062]]
- `-L`: 指定库文件的搜索目录
- `-std=<STANDARD>`: 指定使用的标准库版本, `eg. -std=c++20`
- `--print-sysroot`: 打印依赖的系统库/头文件路径
- `-Wall`: 开启常见的编译告警
- `-o`: 指定保存的文件
- `-E`: 
	- 使 GCC 在完成预处理后**停止**，不继续执行编译、汇编或链接。
	- 将预处理后的结果输出到**标准输出**（默认显示在屏幕上）。
	- 可以通过 `-o` 选项将结果保存到指定文件，例如：
```cpp
gcc -E source.c -o source.i
```
- `-isystem <dir>`: 指定系统头文件搜索路径
- `--sysroot`
- `-mfpu`
- `-mfloat-abi`

---
2. 

3. -Wall：启用常见的编译告警


5. -march=armv7-a: 告诉编译器CPU架构为armv7

6. -Wl,-dynamic-linker,<链接器路径> //编译出来的elf文件添加.interp段

7. `-O0`：完全关闭代码优化, 防止优化把变量生命周期打乱
8. -fno-omit-frame-pointer： 让栈回溯更完整
# 实例
## 查看GCC/G++最高支持的标准库版本
- `eg. arm-none-linux-gnueabihf-g++ -std=c++20 -E - < /dev/null`
	- 报错说明不支持, 不报错就是支持
## 查看GCC/G++使用的内核版本号
- `eg. arm-none-linux-gnueabihf-gcc -v 2>&1 | grep -i "headers"`
---
# 查看C使用的标准库信息
```shell
# 1. 查询标准C库 (libc) 的路径 (最常用)
arm-none-linux-gnueabihf-gcc -print-file-name=libc.so
```
## 查看C++使用的标准库信息
```shell
arm-none-linux-gnueabihf-g++ --print-file-name=libstdc++.so
```
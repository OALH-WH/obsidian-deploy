---
{"dg-publish":true,"permalink":"/技术文档/RTOS/Zephyr/元工具/west命令/","dg-note-properties":{}}
---

# 参数
## init
### 参数
- `-l`: 从本地包含了`west.yml`的`manifect`子目录初始化项目工作空间
## update
- 代码库拉取
### build
- 构建应用
### 参数
- `--board, -b <BOARD_TYPE>`: 必须指定, 指定开发板类型
	- `<BOARD_TYPE>`: 格式为`<board>[@<revision>][/<qualifier>]`
		- **board**：必填，如 `stm32h750b_dk`
		- **revision**：可选，硬件版本号，如 `@2` 表示第二版
		- **qualifier**：可选，进一步细分 SoC 或板级配置，如 `/stm32h750xx`
	- 通过官方文档查找, 参考<https://docs.zephyrproject.org/latest/boards/st/stm32h750b_dk/doc/index.html>
	- 也可以直接通过`zephyr/boards/your/board_type/board.yml`确认
- `--cmake-only`: 只完成`CMake`配置(包括处理并合并所有设备树文件), 不执行后续的编译, 汇编和链接

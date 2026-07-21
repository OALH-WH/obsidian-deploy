---
{"dg-publish":true,"permalink":"/技术文档/构建工具/make/make语法/","dg-note-properties":{}}
---

# Makefile 语法指南
## 0. 内置变量(可覆盖)
### `MAKE`
- make命令的名称, `eg. make`

## 1. 重要注意事项

### 1.1 解析顺序

Makefile语法会在shell解析之前解析。

### 1.2 目标之间的关系
每个目标都是在一个单独的子进程中执行

正常情况下环境变量无法传递, 如需传递需要通过[[#6.3 `export`]]全局声明


## 2. 文件类型

|扩展名|说明|
|---|---|
|`*.mk`|用来写makefile的片段|
|`Makefile`|主makefile文件|
|`makefile`|主makefile文件（小写）|

## 3. 变量类型

### 3.1 自动变量

自动变量在规则执行时自动计算值：

|变量|说明|
|---|---|
|`$@`|表示构建目标|
|`$*`|表示构建目标去掉后缀的部分|
|`$<`|表示第一个依赖文件或者依赖目标|
|`$^`|表示所有的依赖文件|
|`$?`|表示比目标文件更新的依赖文件|

### 3.2 环境变量

**格式：**

```makefile

<var name>=<var value> make
```

**作用：** 在make执行时传入环境变量
```shell
# 特点：
# 1. 优先级最低（被 Makefile 赋值和命令行赋值覆盖）
# 2. 会自动传递给子 make
```

### 3.3 参数变量

**格式：**

```bash

make <var name>=<var value>
```

**作用：** 在命令行中直接给变量赋值
```shell
# 特点：
# 1. 优先级最高（覆盖 Makefile 中的所有赋值）
# 2. 变量会传递给子 make（递归调用时）
# 3. 变量在 Makefile 中被视为"已定义"
```

### 3.4 目标特定变量
- 这个变量**只对指定的目标（及其所有依赖）生效**。
- 当 make 决定构建该目标时，这个变量值会临时覆盖全局同名变量，并传递给依赖的构建过程。

**基本格式**
```makefile
target ...: variable = value
target ...: variable := value
```

**示例**
`eg. my_target: my_var := 1`
## 4. 变量赋值操作符

赋值符前后必须加空格。
```shell
# 特点：
# 1. 优先级低于命令行赋值
# 2. 默认不会传递给子 make（除非使用 export）
# 3. 可以在 Makefile 中多次修改
```

### 4.1 `:=`（立即赋值）

**作用：** 和一般的赋值相同，即引用时和该变量赋值前后顺序相关，顺序不同结果不同

### 4.2 `?=`（条件赋值）

**作用：** 如果该变量已经被赋值则不会覆盖赋值

### 4.3 `=`（延迟赋值）

**作用：** 全部展开后，取最后一次的值给变量（引用时，跟该变量赋值前后顺序无关，即结果相同）

```makefile

CC = gcc
CC2 = $(CC)      # CC2的值会在展开时确定
CC = g++

# 这里 CC2 的值为 g++，而不是 gcc。
# 因为 CC2 的赋值是在 Makefile 全部展开后进行的，此时 CC 的值为 g++
```
### 4.4 `+=`（追加赋值）

**作用：** 将值添加到这个变量值之后，并在两个值之间添加空格

### 4.5 赋值方式之间的区别
| 赋值方式     | 定义位置      | 展开时机          | 优先级                | 传递性         |
| -------- | --------- | ------------- | ------------------ | ----------- |
| 立即赋值（:=） | Makefile中 | 定义时展开         | 中等（被命令行覆盖）         | 可通过export传递 |
| 条件赋值（?=） | Makefile中 | 定义时展开（如果赋值发生） | 较低（仅当变量未定义时赋值）     | 可通过export传递 |
| 延迟赋值（=）  | Makefile中 | 使用时展开         | 中等（被命令行覆盖）         | 可通过export传递 |
| 追加赋值（+=） | Makefile中 | 取决于原变量定义方式    | 中等（被命令行覆盖）         | 可通过export传递 |
| 环境变量     | Shell环境   | 导入到make时展开    | 低（被Makefile和命令行覆盖） | 自动传递给子make  |
| 参数变量     | 命令行       | 在命令行指定时展开     | 最高（覆盖其他所有）         | 自动传递给子make  |
|          |           |               |                    |             |
### 4.6 变量多次不同类型赋值的优先级

**...**

## 5. 内置函数

### 5.1 `foreach`

**基本格式：**

```makefile

$(foreach var,list,text)
```

**作用：** 将list中的每个元素赋给var，然后执行text表达式，返回由空格分隔的多个text的结果

### 5.2 `info`

**基本格式：**

```makefile

$(info text content)
```

**作用：** 输出文本内容，例如 `$(info test content)` 会输出 `test content`

### 5.3 `addprefix`

**基本格式：**

```makefile

$(addprefix <prefix>, <names...>)
```

**作用：** 在每个name前面加上prefix

**示例：**

```makefile

SRC := main.c utils.c math.c
SRC_PATH := src/

OBJ := $(addprefix $(SRC_PATH), $(SRC))
# OBJ = src/main.c src/utils.c src/math.c
```

### 5.4 `addsuffix`

**基本格式：**

```makefile

$(addsuffix <suffix>, <names...>)
```

**作用：** 在每个name后面加上suffix
### `5.5 shell`
**基本格式:** 
```makefile
var := $(shell pwd)
```
**作用:** 将命令的输出赋给`make`变量
## 6. 特殊指令

### 6.1 `.PHONY`
如果目标被声明为 `.PHONY`，Make 会认为它总是过时的，但在同一次 `make` 调用中，同一个伪目标也只会被执行一次（因为 Make 会记录其已被构建)

**格式：**

```makefile

.PHONY : <目标名>
```

**作用：** 声明伪目标，即使有同名文件存在，make也会执行该目标

### 6.2 `override`

**作用：** 保护变量不被命令行参数覆盖

**示例：**

```makefile

override myvar := content
override myvar += additional_content
```

### 6.3 `export`

**作用：** 可使变量传递给子`makefile`

**示例:**
```makefile
export myvar = content
```
## 7. 条件分支

### 7.1 `ifeq` / `ifneq`

```makefile

ifeq ($(CC), gcc)
    LIBS = $(LIBS_FOR_GCC)
else
    LIBS = $(NORMAL_LIBS)
endif

# 检查变量是否为空
ifneq ($(CC),)
    # CC不为空时执行
endif
```
## 8. 文件包含

### 8.1 `include`

**格式：**

```makefile

include <file-path>
```

**作用：** 在包含它的文件中完全展开被包含的文件

**注意：** 被包含的文件里可以使用包含它的文件中的变量，前提是变量的定义要在include命令之前

## 9. 基本语法

### 9.1 基本格式

```makefile

<target>: <depends>
    build cmd1
    build cmd2
    ...
```

### 9.2 解析说明

- **target：** 可以是文件名，也可以是声明的伪目标，可以有多个（以空格隔开）
    
- **depends：** 依赖文件集合，也可以是目标
    
- **命令前的@：** 作用为不打印命令，默认是先打印命令，再输出执行结果
    

## 10. GNU make扩展语法

### 10.1 双冒号规则

**背景：** 一般的同一个目标只能定义一次，多次定义会被合并成一个规则，以最后定义的为准

**格式：**

```makefile

target :: prerequisite
```

**特点：** 双冒号定义的所有相同目标都会执行，是独立存在的

### 10.2 静态模式规则

**格式：**

```makefile

targets : target-pattern : prereq-pattern
```

**说明：** 满足target-pattern表达式的目标需要依赖prereq-pattern匹配的文件

**注意：**

```makefile

$(addprefix $(DEST)/, $(MAIN_TARGET)): $(DEST)/% : $(SRC)/%.c
```

这种格式中的prereq-pattern中的`%`不是表示匹配所有.c文件，而是匹配和target-pattern中`%`匹配的值一样，而target-pattern是去target中匹配一个值

### 10.3 通配符 `%`

**作用：** 用作依赖和目标中的通配符

**实例：**

```makefile

%:
    # 用于匹配任意字符串，例如 make abcd 就会执行这里的逻辑
    @echo "Building target: $@"
```

## 11. 示例

### 11.1 通用模式匹配

```makefile

# 将src目录下的.c文件编译为obj目录下的.o文件
OBJ_DIR := obj
SRC_DIR := src

SRCS := $(wildcard $(SRC_DIR)/*.c)
OBJS := $(patsubst $(SRC_DIR)/%.c, $(OBJ_DIR)/%.o, $(SRCS))

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
    @mkdir -p $(OBJ_DIR)
    $(CC) -c $< -o $@

all: $(OBJS)
    @echo "Build completed"
```

### 11.2 使用伪目标

```makefile

.PHONY: clean all install

all: program

program: main.o utils.o
    $(CC) $^ -o $@

clean:
    rm -f *.o program
```

### 11.3 条件编译

```makefile

DEBUG ?= 0

ifeq ($(DEBUG), 1)
    CFLAGS += -g -DDEBUG
else
    CFLAGS += -O2
endif

program: main.c
    $(CC) $(CFLAGS) $< -o $@
```
这个Markdown文档整理了Makefile的核心语法和用法，可以作为快速参考手册使用。
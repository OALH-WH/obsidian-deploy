---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/z_交叉开发_不维护/makefile/","dg-note-properties":{}}
---

- 示例

```python
obj-m += test.o
test_str = $(PWD)


test:
	echo ${test_str}
all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean

```

- 内置变量

	- M：指定内核模块源码所在的目录

	- obj-m：指定了内核模块的目标文件

	- CXX：g++编译器

	- CC: gcc编译器

	- LD: 指定链接器的名称
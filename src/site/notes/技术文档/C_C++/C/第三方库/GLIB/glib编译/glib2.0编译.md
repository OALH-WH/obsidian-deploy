---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/第三方库/GLIB/glib编译/glib2.0编译/","dg-note-properties":{}}
---

# glib-2.0.0 编译指南

## 背景

本文档记录了在现代 Linux 系统（x86_64）上编译 glib-2.0.0 的过程。glib-2.0.0 是 2002 年发布的版本，代码非常古老，在现代编译器上会遇到兼容性问题。

## 环境

- 系统: x86_64-unknown-linux-gnu
- GCC: 现代版本（支持 C99/C11）
- 目标: 编译并安装 glib-2.0.0 到本地目录

## 编译步骤

### 1. 配置

```bash
cd /home/sino/work/venv/projects/uaonos/test/glib-2.0.0

# 使用本地安装目录，避免需要 root 权限
# 添加编译选项解决兼容性问题
CFLAGS="-g -O2 -fcommon" \
LDFLAGS="-Wl,--allow-multiple-definition" \
./configure --prefix=/home/sino/work/venv/projects/uaonos/test/glib-install
```

### 2. 编译

```bash
make -j4
```

### 3. 安装

```bash
make install
```

### 4. 验证

编译测试程序：

```bash
gcc test.c -o test \
    -I/home/sino/work/venv/projects/uaonos/test/glib-install/include/glib-2.0 \
    -I/home/sino/work/venv/projects/uaonos/test/glib-install/lib/glib-2.0/include \
    -L/home/sino/work/venv/projects/uaonos/test/glib-install/lib \
    -Wl,-rpath,/home/sino/work/venv/projects/uaonos/test/glib-install/lib \
    -lglib-2.0
```

## 遇到的问题及解决方案

### 问题一：多重定义错误

**错误信息：**

```
/usr/bin/ld: garray.lo: multiple definition of `g_bit_nth_lsf'; ...
```

**原因分析：**

这是因为 glib-2.0.0 代码中的 `gutils.h` 头文件使用了 `G_INLINE_FUNC` 宏定义了一些内联函数（如 `g_bit_nth_lsf`, `g_trash_stack_push` 等）。

在头文件中（第 225-313 行）：

```c
#if defined (G_CAN_INLINE) || defined (__G_UTILS_C__)
G_INLINE_FUNC gint
g_bit_nth_lsf (gulong mask, gint nth_bit)
{
    // 函数实现
}
...
#endif
```

问题在于：
1. `G_INLINE_FUNC` 在现代 GCC 下被定义为 `extern inline`（非静态内联）
2. 这导致这些函数在每个包含该头文件的 .c 文件中都会产生定义
3. 链接器在合并多个目标文件时发现重复定义

**尝试的解决方案：**

| 尝试 | 方法 | 结果 |
|------|------|------|
| 1 | 直接 configure 和 make | ❌ 失败 |
| 2 | 添加 `CFLAGS="-fcommon"` | ❌ 仍然失败 |
| 3 | 添加 `LDFLAGS="-Wl,--allow-multiple-definition"` | ✅ 成功！ |

### 问题二：权限问题

**错误信息：**

```
/usr/bin/install: cannot remove '/usr/local/bin/glib-gettextize': Permission denied
```

**原因：** 默认安装路径 `/usr/local` 需要 root 权限。

**解决方案：** 使用 `--prefix` 指定本地安装目录：

```bash
./configure --prefix=/home/sino/work/venv/projects/uaonos/test/glib-install
```

## 编译选项说明

### -fcommon

GCC 10+ 默认使用 `-fno-common`，会将未初始化的全局变量视为强定义，导致多重定义错误。`-fcommon` 恢复旧的行为，将它们视为弱定义。

### -Wl,--allow-multiple-definition

链接器选项，允许在最终链接的可执行文件或共享库中存在多重定义（使用第一个定义）。

## 安装后的文件结构

```
/home/sino/work/venv/projects/uaonos/test/glib-install/
├── include/
│   └── glib-2.0/
│       ├── glib.h
│       ├── glib-object.h
│       ├── gmodule.h
│       ├── gobject/
│       └── glib/
│           ├── garray.h
│           ├── ghash.h
│           └── ... (40+ 头文件)
├── lib/
│   ├── libglib-2.0.so.0.0.0    (主库，约 1.4MB)
│   ├── libgmodule-2.0.so.0.0.0
│   ├── libgobject-2.0.so.0.0.0
│   ├── libgthread-2.0.so.0.0.0
│   └── pkgconfig/
└── ...
```

## 参考资料

1. **GCC 文档**: 关于 `-fcommon` 和 `-fno-common` 选项
   - https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html

2. **ld 文档**: 关于 `--allow-multiple-definition` 选项
   - https://sourceware.org/binutils/docs/ld/Options.html

3. **glib 源码**:
   - `glib/gutils.h` - 包含问题代码的头文件
   - `configure.in` - 配置脚本
   - `glib/Makefile.am` - 构建配置

4. **glib ChangeLog**: 了解 G_INLINE_FUNC 和 G_CAN_INLINE 宏的历史

## 测试代码示例

```c
#include <glib.h>
#include <stdio.h>

int main() {
    printf("GLib version: %d.%d.%d\n", 
           glib_major_version, glib_minor_version, glib_micro_version);
    
    GList *list = NULL;
    list = g_list_append(list, "hello");
    list = g_list_append(list, "world");
    
    printf("List length: %d\n", g_list_length(list));
    printf("First item: %s\n", (char*)g_list_first(list)->data);
    
    g_list_free(list);
    return 0;
}
```

运行结果：

```
GLib version: 2.0.0
List length: 2
First item: hello
```

## 总结

编译古老的 glib-2.0.0 的主要挑战在于现代 GCC 的默认行为变化。通过添加合适的编译和链接选项（`-fcommon` 和 `--allow-multiple-definition`），可以成功编译这个 2002 年的代码库。

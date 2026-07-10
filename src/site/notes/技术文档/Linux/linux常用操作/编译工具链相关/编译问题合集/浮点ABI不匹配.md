---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/编译问题合集/浮点ABI不匹配/","dg-note-properties":{}}
---

# 背景
## ABI
全称`Application Binary Interface`, 表示应用二进制接口
即二进制程序之间的通信协议, 当这个协议对不上时, 链接器就会拒绝合并它们

`ABI` 定义了编译后的二进制文件（`.o`、`.a`、`.so`）之间如何互相调用。它规定了：
- **函数调用约定**：参数从哪几个寄存器传递？由谁清理堆栈？
- **数据类型大小与对齐**：`int`、`long` 占几个字节？
- **目标文件格式**：ELF 文件的结构。

### 浮点ABI
| ABI 类型            | 编译选项                 | 特点                                                |
| ----------------- | -------------------- | ------------------------------------------------- |
| **软浮点 (Soft)**    | `-mfloat-abi=soft`   | 完全用软件模拟浮点运算，**不使用**硬件 FPU，参数通过**通用寄存器**传递。        |
| **软硬兼容 (Softfp)** | `-mfloat-abi=softfp` | 使用硬件 FPU 指令加速运算，但参数仍通过**通用寄存器**传递。                |
| **硬浮点 (Hard)**    | `-mfloat-abi=hard`   | 使用硬件 FPU，参数通过**专用的 VFP 寄存器**（如 `s0`、`d0`）传递，性能最佳。 |


# 实例
---
## 为什么会出现浮点ABI不匹配

你的错误信息是：

> `cmTC_bc414 uses VFP register arguments, CMakeFiles/...testCXXCompiler.cxx.o does not`

这句话翻译过来就是：

> **链接器**想把目标文件合并成可执行文件，但可执行文件要求使用 VFP 寄存器传参（硬浮点），而你的 `.o` 目标文件却没有启用这个特性。

**根本原因**：你的 **Sysroot**（即 `/opt/.../cortexa7t2hf-neon-vfp4-...`）是为 **硬浮点（Hard）** 编译的（路径中的 `hf` 就是证据），里面的库（如 `libstdc++.so`）都期望调用者使用 VFP 寄存器传参。然而，你的 CMake 在编译 `testCXXCompiler.cxx` 时，**没有传递 `-mfloat-abi=hard`**，导致编译器默认使用了软浮点（或软硬兼容），生成的目标文件不包含 VFP 寄存器信息。

---

## 如何排查 ABI 是否匹配？（诊断方法）

在解决之前，建议你先用以下命令验证一下，做到心中有数：
- **查看目标文件（`.o`）的 ABI 属性**：
```bash
readelf -A your_object_file.o
```

输出中如果有 `Tag_ABI_VFP_args: VFP registers`，表示该文件是硬浮点；如果没有这一行或值为 `0`，则不是硬浮点。
- **查看 Sysroot 中库的 ABI**：
```bash
readelf -A /opt/st/.../sysroots/.../usr/lib/libstdc++.so
```
你会看到它明确标注了 `Tag_ABI_VFP_args: VFP registers`，说明要求硬浮点。
- **查看编译器的默认 ABI**：
```bash
arm-ost-linux-gnueabi-g++ -dumpspecs | grep float-abi
```
如果输出为空或指向 `soft`，说明你不指定参数时默认是错的。

---

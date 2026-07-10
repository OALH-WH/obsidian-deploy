---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/二进制程序相关/ldd命令/","dg-note-properties":{}}
---

# 作用
- 查看可执行程序依赖哪些动态库
- 动态分析, 会执行程序
# 使用
## 缺点
- 会执行程序, 不可对不可信的二进制程序执行ldd命令
# 类似命令
- [[技术文档/Linux/linux常用操作/二进制程序相关/objdump命令\|objdump命令]]
- [[技术文档/Linux/linux常用操作/二进制程序相关/readelf命令\|readelf命令]]
## 内容解析
- 示例1
```shell
root@uaonos-sino:~# ldd /etc/sonic/wuhang/appd
        linux-vdso.so.1 (0x0000007fa9912000)
        libnl-3.so.200 => /lib/aarch64-linux-gnu/libnl-3.so.200 (0x0000007fa9658000)
        libnl-route-3.so.200 => /lib/aarch64-linux-gnu/libnl-route-3.so.200 (0x0000007fa95c6000)
        libswsscommon.so.0 => /lib/aarch64-linux-gnu/libswsscommon.so.0 (0x0000007fa951b000)
        libpthread.so.0 => /lib/aarch64-linux-gnu/libpthread.so.0 (0x0000007fa94ec000)...
        
# 拆解
# libnl-3.so.200 => /lib/aarch64-linux-gnu/libnl-3.so.200 (0x0000007fa9658000) 表示找到库libnl-3.so.200, 库路径为/lib/aarch64-linux-gnu/libnl-3.so.20, 在进程中虚拟地址空间的加载地址为0x0000007fa9658000
```
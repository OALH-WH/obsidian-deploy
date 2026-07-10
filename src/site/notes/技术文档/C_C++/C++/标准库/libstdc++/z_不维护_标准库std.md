---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/z_不维护_标准库std/","dg-note-properties":{}}
---

1. <atomic>：原子库

1. 提供原子类型atomic<template type>

1. <string>

1. 常用类

1. string

1. 构造函数

1. (size, char) //长度为size的每个字符为char

1. 常用API

1. data

1. 作用：获取存储字符串的指针

1. resize

1. 作用：指定存储字符串的空间大小

1. <sstream>

1. ostringstream：用于字符串解析

1. 常用API

1. <fstream>

1. 作用：用于文件输入/输出流

1. 常用类

1. ifstream

1. 构建方法

1. ifstream var_name(file_name, open_mode)

1. file_name: string|char*

1. open_mode: ios_base::in | ios_base::out...

1. 常用API

1. <tuple>

1. 常用API

1. forward_as_tuple： 将一组参数完美转发到tuple中

1. 常用API

1. format: 类似于python的print格式化输出

1. forward：它可以将一个参数的左右值特性原封不动地转发给其他函数
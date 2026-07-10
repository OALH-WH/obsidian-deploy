---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/语法/c和c++混编/","dg-note-properties":{}}
---

# 常见方法
## 方法1: 头文件声明C方法
- 头文件中声明c函数需要定义如下

```cpp
#ifdef __cplusplus
extern "C" {
#endif

extern int testClassFunc(void);

#ifdef __cplusplus
}
#endif
```
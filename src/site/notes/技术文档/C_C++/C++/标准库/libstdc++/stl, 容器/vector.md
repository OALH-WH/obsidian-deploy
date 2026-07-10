---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/stl, 容器/vector/","dg-note-properties":{}}
---

# 参考
- https://cplusplus.com/reference/vector/vector/
# 依赖
- `#include <vector>`
- `using namespace std`
# 成员函数
## erase
- `iterator erase (const_iterator position);iterator erase (const_iterator first, const_iterator last);`
### 作用
- 删除某一个元素, 或者一个范围内的元素
- 保留的元素前移
### 注意
- 会导致迭代器失效
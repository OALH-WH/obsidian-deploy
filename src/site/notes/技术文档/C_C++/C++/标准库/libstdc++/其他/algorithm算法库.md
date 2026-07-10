---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/其他/algorithm算法库/","dg-note-properties":{}}
---

# 参考
- https://cplusplus.com/reference/algorithm/
# 依赖
- `#include <algorithm>`
- `using namespace std`
# 函数
## remove
- `template <class ForwardIterator, class T>  ForwardIterator remove (ForwardIterator first, ForwardIterator last, const T& val);`
### 作用
- 它只是**将需要保留的元素向前移动**，覆盖掉那些“要被删除”的元素，然后返回一个指向**新逻辑末尾**的迭代器
	- `eg. vector<int> v{1,2,3,4}; auto new_end = std::remove(v.begin(), v.end(), 2);`
	- `v`现在可能是`{1,3,4,?}`, 总长度仍是4, 函数返回的`new_end`指向第4个元素 
- 总元素长度不变
### 实例
#### 配合成员函数erase来实现删除元素
- 好处: 只用移动一次元素
```cpp
std::vector<int> v = {1, 2, 3, 2, 5};
v.erase(std::remove(v.begin(), v.end(), 2), v.end());
// 结果：v 为 {1, 3, 5}
```
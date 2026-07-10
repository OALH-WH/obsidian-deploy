---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/其他/utility库/","dg-note-properties":{}}
---

# 函数 
## move
- 返回一个左值引用
## forward
- 转发一个函数实参
**常见实例**
```cpp
void bar(int&)  { std::cout << "左值\n"; }
void bar(int&&) { std::cout << "右值\n"; }

template<typename T>
void foo(T&& arg) {
    bar(arg);                      // 永远调用 bar(int&), 因为数据类型为万能引用的arg形参本身就是一个左值, 如果不使用std::forward, 在调用bar函数时就会当作左值传递, 无法持续移动数据, 而是变成了拷贝数据, 损失了性能
    // bar(std::forward<T>(arg));  // 保留原始类别
}

int main() {
    int x = 1;
    foo(x);   // 输出 "左值"
    foo(2);   // 也输出 "左值" —— 丢失了右值信息！
}
```
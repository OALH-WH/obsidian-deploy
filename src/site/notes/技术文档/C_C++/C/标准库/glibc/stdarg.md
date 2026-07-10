---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/标准库/glibc/stdarg/","dg-note-properties":{}}
---

# 可变参数
```cpp
#include <cstdarg>
#include <iostream>

// 需要提供参数个数
int sum(int n, ...) {
    int total = 0;
    va_list args;
    va_start(args, n);
    for (int i = 0; i < n; ++i) {
        total += va_arg(args, int);
    }
    va_end(args);
    return total;
}

int main() {
    std::cout << sum(5, 1, 2, 3, 4, 5) << std::endl; // 输出: 15
    return 0;
}
```
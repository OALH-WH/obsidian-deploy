---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C_C++语法/","dg-note-properties":{}}
---

1. C++

1. 原理

1. 函数重载是通过函数签名（包括函数名和参数列表，不包括修饰符和返回值）来区分的

1. 关键字

1. explicit

1. 作用：防止构造函数进行隐式转换

1. 隐式转换示例

```cpp
class MyClass {
public:
    MyClass(int value) {
        // 构造函数
    }
};

void function(MyClass obj) {
    // 函数体
}

int main() {
    function(5); // 隐式转换：int -> MyClass
    return 0;
}
```

1. 
---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/stl, 容器/set/","dg-note-properties":{}}
---

# 背景
# 依赖
## 头文件
- `#include <set>`
# 常见使用
## 自定义复杂类型作为元素
### 注意
- 需要提供两个关键组件
	- 哈希函数
	- 相等比较函数
### 实例
- ```cpp
#include <unordered_set>
#include <string>
#include <iostream>
#include <functional>

struct Person {
    std::string name;
    int age;
    double salary;
    
    // 1. 相等比较操作符（必须）
    bool operator==(const Person& other) const {
        return name == other.name && age == other.age;
    }
};

// 2. 自定义哈希函数
struct PersonHash {
    std::size_t operator()(const Person& p) const {
        // 使用 std::hash 组合多个字段
        std::size_t h1 = std::hash<std::string>{}(p.name);
        std::size_t h2 = std::hash<int>{}(p.age);
        
        // 简单组合方法：异或（注意：异或对称，可能冲突多）
        // return h1 ^ h2;
        
        // 更好的组合方法：使用标准库的 hash_combine
        // 或者使用 boost::hash_combine
        return h1 ^ (h2 << 1);
    }
};

int main() {
    // 使用自定义哈希函数
    std::unordered_set<Person, PersonHash> people;
    
    people.insert({"Alice", 30, 50000.0});
    people.insert({"Bob", 25, 45000.0});
    people.insert({"Alice", 30, 55000.0});  // 不会插入，因为 name 和 age 相同
    
    std::cout << "Size: " << people.size() << std::endl;  // 输出: 2
    
    // 查找元素
    Person search{"Alice", 30, 0};
    if (people.find(search) != people.end()) {
        std::cout << "Found Alice, 30" << std::endl;
    }
    
    // 遍历（无序！）
    for (const auto& p : people) {
        std::cout << p.name << ", " << p.age << std::endl;
        // 输出顺序不确定，可能是随机的
    }
    
    return 0;
}
  ```

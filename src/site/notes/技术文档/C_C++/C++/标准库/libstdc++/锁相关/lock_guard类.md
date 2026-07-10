---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/标准库/libstdc++/锁相关/lock_guard类/","dg-note-properties":{}}
---

# 背景
- 用于上锁
- 在析构实例时, 自动释放锁
# 常见实例
## mutex上锁及析构自动解锁
```cpp
std::lock_guard<std::mutex> lock(s_firmware_upgrade_state_mutex);
```
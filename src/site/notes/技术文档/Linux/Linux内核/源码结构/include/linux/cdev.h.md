---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/cdev.h/","dg-note-properties":{}}
---


# struct cdev
```cpp
struct cdev {

    struct kobject kobj;

    struct module *owner;

    const struct file_operations *ops;

    struct list_head list;

    dev_t dev;

    unsigned int count;

} __randomize_layout;
```

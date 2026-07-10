---
{"dg-publish":true,"permalink":"/技术文档/Python/语法/Python语法/","dg-note-properties":{}}
---

1. 例子

1. k, v, *_ = ['key', 'value', 'extra']

1. 含义

1. k会得到第一个元素

1. v会得到第二个元素

1. *_会得到剩余的元素，表示不关心这些元素

1. 装饰器相关

1. 根本原理

1. 相当于把被装饰的函数作为实参传递到装饰器中，实际执行的是装饰器定义的函数

1. 语法相关

1. 合并多个dict

1. dict1 | dict2 | dict3

1. new_dict = {**dict1, **dict2,...}

1. 输出相关

1. 格式控制符

1. e：表示科学计数法输出 // "{:.2e}"

1. f: 表示浮点数输出,总共占6个字符，小数占3个，整数部分不足补零 // "{:06.3f}"

1. d: 表示浮点数输出总共占4个字符，不足补0 // "{:04d}"

1. 方法相关

1. isinstance():判断这个对象是否是某个类型的实例

1. arg1：对象

1. arg2：类型元组或者单个类型

1. 示例：isinstance(a, int)

1. any(): 判断一个可迭代对象中是否至少包含一个True

1. arg1：可迭代对象

1. return：至少包含一个True返回True，否则返回False

1. 类相关

1. super函数

1. 

1. __str__函数

1. 作用：当用类似于print方法打印类的时候，被调用

1. 示例

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"Person(name={self.name}, age={self.age})"
    
    def __repr__(self):
        return f"Person('{self.name}', {self.age})"
    
# 创建一个 Person 对象
p = Person("Alice", 30)

# 打印对象（调用 __str__）
print(str(p))  # 输出: Person(name=Alice, age=30)

# 直接在解释器中输入对象（调用 __repr__）
print(repr(p))  # 输出: Person('Alice', 30)
```

1. __enter__函数

1. 作用：通常于with语句一起使用，它定义了进入一个上下文时应该执行的操作。简单来说是在with块开始时被调用

1. 例子

```python
class MyContext:
    def __enter__(self):
        print("Entering the context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with MyContext() as context:
    print("Inside the context")

```

1. 模块相关

1. __all__变量

1. 作用：当使用from <module> import * 导入模块时，只有在__all__中列出的名称是可以被导入的，一般定义在__init__.py函数

1. 示例

```python
__all__ = ['a', 'b']
```
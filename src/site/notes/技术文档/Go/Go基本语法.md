---
{"dg-publish":true,"permalink":"/技术文档/Go/Go基本语法/","dg-note-properties":{}}
---

1. 特性

1. go有强大的垃圾回收功能，会自动分配变量是存储在栈还是堆里，因此在函数之外使用通过局部变量的地址访问是不会报错的，go会自动分配到堆空间，并且无需手动释放

1. 通过指针访问结构体成员字段时，可以通过类似于C的*取值访问，但也可以通过指针直接访问，eg. channel.Index //channel为结构体指针类型

1. 数据类型

1. 数组：长度固定，编译时确定

1. 切片：长度动态分配，指向一个底层的数组，长度不够时，复制数据到新的数组中，类似于c++的vector容器

1. 通道

1. 映射

1. 关键字

1. nil

1. defer：把语句放到此函数返回之前执行

1. range

1. 数组or切片，返回索引和元素值

1. _: 表示得到的值不用管

1. iota：常量计数器，只能配合常量表达式用

1. =和:=

1. =：用于已声明的变量赋值

1. := ：用于声明并且初始化，不能在已声明的变量上使用，会报错

1. interface

1. 定义

1. 用来描述一组抽象方法

1. 任何实现了这组抽象方法的任意方法的物件都能被此interface 变量持有

1. 支持嵌入interface

1. 空interface：类似于void *可以存储任何型别的值

1. 示例var a interface {}

1. 如何判断存储的是哪个型别

1. eg. value, ok :=element.(int) or switch value := element.(int)

1. 断言

1. app, ok := objectInstance.Interface().(appInterface) //断言为这个实例的接口对象的类型是appInterface,如果不是则ok为false,app为appInterface这个接口类型值的零值(nil)

1. type

1. 定义

1. 用来自定义类型(不会拥有源类型的方法)

1. 示例：type a b

1. 用来起别名(会拥有源类型的方法)

1. 示例: type a=b

1. 组合类型（会拥有源类型的方法）

1. 示例：type a struct {b}

1. 源类型接口方法会保留

1. 示例：

1. 衍生

1. struct

1. interface

1. 

1. 序列化and反序列化

1. 序列化：将go结构类型转换称其他格式内容

1. 反序列化：将其他格式内容如json转换成go结构类型

1. 通道

1. 声明： var ch chan int

1. 初始化：ch := make(chan int, 3)

1. 发送: ch<-3

1. 接收: <-ch

1. 关闭: close(ch)

1. 容器

1. map

1. 定义eg. var a map[string]string

1. 标签

1. 用于编码和解码成对应配置文件(.yang, .xml, .json文件中的key)

1. 例如`json: name`, 即会在编码为json时把字段的名称改为key=name

1. 反射

1. 常用套件

1. reflect: Go变量->interface{}->反射对象

1. 传递参数是指针类型，要通过Elem函数获取指针中存储的值

1. 常用方法

1. ValueOf

1. TypeOf

1. New

1. Elem

1. Indirect

1. 常用函数

1. 数组=append(数组，元素值)：追加一个元素

1. delete(数组/切片/映射，key/index)

1. make:用于创建切片，映射，通道，来分配和初始化内存

1. 示例

1. 方法：

1. 可变参数:函数体中使用variable_name...表示打包成参数列表，可用来传递给其他函数，

1. func (variable_name ...variable_data_type) {}

1. 值方法

1. 示例

```
func (variable_name variable_data_type) function_name() [return_type]{
   /* 函数体*/
}
```

1. 指针方法

1. 示例

```
func (variable_name *variable_data_type) function_name() [return_type]{
   /* 函数体*/
}
```

1. 
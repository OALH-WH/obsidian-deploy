---
{"dg-publish":true,"permalink":"/技术文档/C++编程规范/","dg-note-properties":{}}
---

- quick_exit()：它们不同之处为：在退出程序时不会执行任何析构，也不会执行atexit()所绑定的任何handlers，如果下昂在执行quick_exit()来中断时执行某handler（比如刷新log），可以把它绑定到_at_quick_exit(),如果想在exit()中用也可以绑定上去。

- 为什么析构函数要声明成virtual？

	- 因为，如果delete一个基类的指针时，如果它指向的是一个子类的对象，那么析构函数不为虚就会导致无法调用子类析构函数，从而导致资源泄露。 当然，另一种做法是将基类析构函数设为protected.

	- 只有在有其他成员函数存在virtual函数时，才考虑引用虚函数表，因为虚函数表会造成性能损失。

	- 当把析构函数声明为protected时，由于在基类和子类类外调用析构函数会产生错误，也可以避免内存泄露的问题存在。

- 接口

![](WEBRESOURCEcc2396b2cf272bb4dcbdbed3193a45aaimage.png)

- 右值引用

	- std::move()把一个左值转换为一个右值引用

		- 拷贝构造会转换成移动构造

- 类型转换

	- 用static_cast替换c风格的值转换，或者某个类指针需要明确的向上转换为父指针

	- 用const_cast去掉const限定符

	- 用reinterpret_cast指针类型和整型或其他指针之间进行不安全的相互转换

- 关键字mutable、volatile的作用

	- mutable：如果需要在const成员方法中修改一个成员变量的值，那么需要将这个成员变量修饰为mutable。即用mutable修饰的成员变量不受const成员方法的限制。

	- volatile：一个定义为volatile的变量是说这变量可能会被意想不到地改变，这样，编译器就不会去假设这个变量的值了。精确地说就是，优化器在用到这个变量时必须每次都小心地重新读取这个变量的值，而不是使用保存在寄存器里的备份。
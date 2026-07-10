---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/第三方库/Qt/QT/QML/旧的/QML和C++_Python交互/","dg-note-properties":{}}
---

1. cpp

1. 头文件

1. #include <QQmlContext>

1. 通过engine.rootContext()->setContextProperty("myObject", &myObject);函数把对象实例注册到qml的上下文中，使qml也可以用c++的类方法，信号等等

1. python
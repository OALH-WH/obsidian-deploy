---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/第三方库/Qt/QT/QML/旧的/多QML文件模块化/","dg-note-properties":{}}
---

1. 静态包含

1. 通过import包含指定路径下的QML文件，例如import "./Myqml.qml" as Myqml//包含当前目录下Myqml组件

1. Myqml组件就是对应着Myqml.qml的TOP组件

1. 动态包含

1. 通过Loader组件的source属性动态加载、显示组件

1. 此Loader组件的item属性就表示的另一个文件的TOP组件，即item的值就是另一个文件的TOP组件的id

1. 作为动态加载其他模块时，不需要asynchronous属性

1. 信号和槽

1. 
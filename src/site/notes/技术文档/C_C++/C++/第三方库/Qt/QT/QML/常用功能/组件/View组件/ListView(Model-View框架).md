---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/第三方库/Qt/QT/QML/常用功能/组件/View组件/ListView(Model-View框架)/","dg-note-properties":{}}
---

1. 两个个主体，一个作用 //源自Qt的Model-View-Delegate框架--->源自MVC(Model-View-Control)设计思想

1. 作用：显示一个条目列表

1. Model：数据来源

1. Delegate：每个数据的表现形式

1. View显示所有的数据

1. 使用

1. ListView组件

1. delegate：表示每条数据的显示样式，可以通过Component组件定义，使用ListElement组件中的定义的变量来显示

1. model：ListModel //数据源列表

1. 方法

1. append

1. insert

1. remove

1. ListElement组件 //表示一个数据源，给变量定义值

1. 变量之间用, 分隔
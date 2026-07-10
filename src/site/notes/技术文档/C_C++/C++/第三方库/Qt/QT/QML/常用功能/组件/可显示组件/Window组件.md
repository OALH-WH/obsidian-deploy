---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/第三方库/Qt/QT/QML/常用功能/组件/可显示组件/Window组件/","dg-note-properties":{}}
---

1. Window

1. 头文件依赖 //import

1. QtQuick

1. 实例

1. 去掉标题栏和系统边框 //无装饰窗口

1. 设置属性flags: Qt.FramelessWindowHint

1. 常用信号处理

1. onClosing

1. 注意

1. 只有Window组件有

1. 触发条件

1. 鼠标点击系统边框上的X

1. ...

1. 基本示例

```cpp
Window {
    width: 640
    height: 480
    visible: true
    title: qsTr("Hello World")
}
```

1. 基本属性

1. width：窗口宽度

1. height：窗口高度

1. visible：窗口是否显示

1. title：窗口标题

1. x/y:窗口位置

1. minimumWidth/Height

1. maximumWidth/Height

1. opacity：透明度

1. color: 颜色

1. 注意

1. 直接降低透明度会让整个窗口变透明

1. 可以创建一个完全覆盖此窗口的子窗口,改变子窗口的颜色将不会影响兄弟/父组件的透明度

1. 示例

1. eg.1 color: Qt.rgba(Math.random(), Math.random(), Math.random(), 1); //随机颜色, 最后一个参数表示透明度, 1表示不透明

1. eg.2 color: "#800000ff"
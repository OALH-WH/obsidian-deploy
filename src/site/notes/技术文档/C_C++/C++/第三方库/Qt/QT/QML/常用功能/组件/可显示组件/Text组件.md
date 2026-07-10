---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C++/第三方库/Qt/QT/QML/常用功能/组件/可显示组件/Text组件/","dg-note-properties":{}}
---

1. 注意

1. 当开启了字体自动适应组件大小,字体还是很小, 通常是需要开启自动换行

1. 常用属性

1. wrapMode //换行模式

1. 示例

1. 设置自动换行

1. eg. wrapMode: Text.WordWrap

1. horizontalAlignment //设置字体垂直对齐

1. 示例

1. 设置字体跟组件垂直居中对齐

1. eg. horizontalAlignment:  Text.AlignHCenter

1. verticalAlignment ....

1. 示例

1. eg. verticalAlignment:  Text.AlignVCenter

1. fontSizeMode

1. 注意

1. 要结合font.pixelSize属性 //最大大小 和minimumPixelSize属性 //最小大小

1. 示例

1. eg.1 fontSizeMode: Text.Fit //根据组件大小调整字体大小
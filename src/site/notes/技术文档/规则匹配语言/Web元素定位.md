---
{"dg-publish":true,"permalink":"/技术文档/规则匹配语言/Web元素定位/","dg-note-properties":{}}
---

1. 单一定位

1. id：页面中元素唯一标识符，可能有的会动态变化，下一次进入页面，可能和上一次不一样

1. name：不一定唯一，可能会有重复

1. class name：class一般是用来给元素进行分组的，并对这一级元素设置相同的样式，所以存在多个元素共用一个class，不一定是唯一值

1. tag name：不一定唯一，例如dev，a，body等等

1. link：超链接文本，不一定唯一

1. partial_link：匹配超链接文本的一部分

1. 多样式定位

1. css

1. xpath

1. 基本语法

1. /：根节点

1. //：选择匹配的所有位置

1. .：当前节点

1. ..：父节点

1. @：选择属性

1. [node num]：选取所有node子元素

1. [@attr]：选取带有attr属性的所有元素

1. 函数

1. 表示文本内容

1. text()

1. 精确匹配

1. text() = 'content'

1. 包含匹配

1. contains(text(), 'content')

1. 前缀匹配

1. starts-with(text(), 'prefix')

1. 后缀匹配

1. ends-with(text(), 'suffix')

1. 表否定

1. not()
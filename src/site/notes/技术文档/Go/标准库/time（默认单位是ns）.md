---
{"dg-publish":true,"permalink":"/技术文档/Go/标准库/time（默认单位是ns）/","dg-note-properties":{}}
---

1. 全局函数

1. Now：返回当前时间戳

1. Sleep：rotine睡眠时间，单位默认ns

1. 类型

1. Duration：表示时间的持续长度

1. Time

1. 方法

1. Add：添加指定时间

1. Round：用来调整时间的精度，参数为精度，即时间跳变的最小单位

1. eg.arg=5 * time.Nanosecond， 即最小单位为5ns，返回存储时间相对于指定精度的最近的时间点，即返回的时间点是5ns的倍数，例如time=7ns ret=5ns， time=3ns， ret=0ns

1. Sub：用于计算两个time.TIme对象之间的时间差，返回一个Duration对象

1. 注意

1. 返回值可能为负值，如果方法所属对象的时间点小于参数指定时间点
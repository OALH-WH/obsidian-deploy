---
{"dg-publish":true,"permalink":"/技术文档/Go/内存问题的调试和排查/通过pprof查看内存统计信息/","dg-note-properties":{}}
---

1. 背景

1. 可能发生内存泄漏的原因

1. goroutine, 即协程没用被关闭, 或者没有添加超时控制, 让gorouting一直处于阻塞状态, 不能被GC, garbage collect, 即垃圾回收

1. 暂时性内存泄漏 //string相比于slice少了一个容量的cap字段, 由于新生成的对象和老的string或者slice共用一个内存空间,就会导致老的资源得不到释放

1. 获取长字符串中的一段导致长字符串未释放

1. 获取长slice中的一段导致长slice未释放

1. 再长slice新建slice导致泄漏

1. ...

1. 永久性内存泄漏

1. gorouting泄漏

1. time.Ticker未关闭导致泄漏

1. Finalizer导致泄漏

1. Dferring Function Call导致泄漏

1. 命令行

1. 实例

1. 对比两个时间点的两份heap文件

1. 步骤

1. go tool pprof -diff_base=heap1.pb.gz heap2.pb.gz

1. top //找到怀疑的函数, eg. github.com/gorilla/mux.newRouteRegexp

1. 查看方式

1. list github.com/gorilla/mux.newRouteRegexp //展示每一行源代码的内存增长

1. tree //查看完整调用栈

1. 信息解析

1. allocs/heap //采样样本数量, 表示当前被采样到的样本个数, 即调用栈个数

1. 注意

1. 区别

1. heap只采集当前仍然存在的对象, 即一个对象在采集时被GC了就采集不到了

1. alloc会采集分配过的对象, 不管有没有被GC, 只要分配过就能采集到

1. 每个调用栈都是记录了一次或者多次分配内存, 最开头的数字就是此调用栈分配内存的次数

1. 行数据解析

1. 7表示当前活跃的对象个数 //当前仍然存在于堆上, 尚未被GC回收的对象数量和总字节数

1. 5536表示当前活跃的对象占用字节数

1. 110表示所有的对象个数 //累计分配过的对象数量和总字节数, 不管后来有没有释放

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Go/%E5%86%85%E5%AD%98%E9%97%AE%E9%A2%98%E7%9A%84%E8%B0%83%E8%AF%95%E5%92%8C%E6%8E%92%E6%9F%A5/images/WEBRESOURCE8b6f64baf13dcca257b90d9c902c5f83image.png)

1. 字段解析

1. NumGC

1. 表示从开始监测到目前为止, 垃圾回收运行过的次数

1. Alloc 

1. 当前仍在使用的堆内存字节

1. Sys

1. Go runtime向系统申请的总内存, 大致接近RSS

1. 

1. gorouting

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Go/%E5%86%85%E5%AD%98%E9%97%AE%E9%A2%98%E7%9A%84%E8%B0%83%E8%AF%95%E5%92%8C%E6%8E%92%E6%9F%A5/images/WEBRESOURCE33529810623b663dfa403640a86dfab4image.png)
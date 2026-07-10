---
{"dg-publish":true,"permalink":"/技术文档/Go/标准库/pprof/","dg-note-properties":{}}
---

1. 使用方法

```cpp
import _ "net/http/pprof"

func main() {
    go func() {
        glog.Info(http.ListenAndServe(":7070", nil))
    }() //启动一个协程监听7070端口, 可以通过访问http://127.0.0.1:6069/debug/pprof/来查看内存统计信息
}

```
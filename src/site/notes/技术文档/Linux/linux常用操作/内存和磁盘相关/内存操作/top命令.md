---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/内存操作/top命令/","dg-note-properties":{}}
---

# 作用
查看系统资源占用

默认根据`%CPU`降序排序
# 基本格式
`top [options]`

**参数**
- `-o, --sort-override =FIELD`: 指定排序字段
	- `eg. top -o RES`
- `-e, --scale-task-mem =SCALE`: 指定资源单位, `eg. k,m,g,t,p,e`
- `-E, --scale-summary-mem =SCALE`: 指定资源单位, `eg. k,m,g,t,p,e`

# 数据解析
**HEAD**
```shell
%Cpu(s):  5.0 us, 10.0 sy,  0.0 ni, 80.0 id,  5.0 wa,  0.0 hi,  0.0 si,  0.0 st
```
- `sy` 占 10%，略高 → 内核可能在做频繁的系统调用或 I/O 操作
- `wa` 占 5% → 磁盘有轻微等待，可结合 `iostat` 进一步分析
- `id` 80% → CPU 整体不忙
- 
**FIELD**
```shell
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
1234 mysql     20   0 2.0g   800m   45m S  15.0  5.2   120:30.45 mysqld
```
- `VIRT=2.0g` 虚存很高，但 `RES=800m` 表示实际占用 800MB 物理内存
- `RES=800m`
- `%CPU=15.0` 表示 mysqld 占用了一个 CPU 核心 15% 的时间
- `TIME+` 较大，说明它是一个长期运行且密集计算的服务
- 状态 `S`（睡眠）表示此刻等待事件，但累计 CPU 时间多，说明它间歇忙碌
# 实例
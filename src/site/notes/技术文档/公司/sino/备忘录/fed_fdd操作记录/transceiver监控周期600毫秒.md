---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/备忘录/fed_fdd操作记录/transceiver监控周期600毫秒/","dg-note-properties":{}}
---

# FDD RAISE和FDD ENABLE全部清0关闭
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 168 0 && /host/wuhang/transceiver_cmd l1 -r 0 0x30 168
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2725 us
Average Time: 2725 us
---------------------------------------------
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 1224 us
Average Time: 1224 us
---------------------------------------------
168-168: 00 

---------------------------------------------
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 160 0 0  && /host/wuhang/transceiver_cmd l1 -r 0 0x30 160 -l 2
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 1822 us
Average Time: 1822 us
---------------------------------------------
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 1292 us
Average Time: 1292 us
---------------------------------------------
160-161: 00 00 

---------------------------------------------
```
# 开启监控
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -m -r 0 0x33 132 -l 2
Monitor read bank[0] page[0x33] addr[132] len[2] start...
------------------------------------------------
Monitor read bank[0] page[0x33] addr[132] len[2] value[ 0x00 00 ]
fec pre ber [0x9261]
fdd raise [0x0000]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x00]

```
# 设置FDD RAISE阈值为0x8F FF
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 160 0x8f 0xff && /host/wuhang/transceiver_cmd l1 -r 0 0x30 160 -l 2
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2934 us
Average Time: 2934 us
---------------------------------------------
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 1291 us
Average Time: 1291 us
---------------------------------------------
160-161: 8f ff 

---------------------------------------------
```
## 设置FDD ENABLE
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 168 1 && /host/wuhang/transceiver_cmd l1 -r 0 0x30 168
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2776 us
Average Time: 2776 us
---------------------------------------------
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 1302 us
Average Time: 1302 us
---------------------------------------------
168-168: 01 

---------------------------------------------
```
## transceiver_cmd性能监控
- 值从0变为1
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -m -r 0 0x33 132 -l 2
Monitor read bank[0] page[0x33] addr[132] len[2] start...
------------------------------------------------
Monitor read bank[0] page[0x33] addr[132] len[2] value[ 0x00 00 ]
fec pre ber [0x9261]
fdd raise [0x0000]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x00]
------------------------------------------------
[2026-01-09 11:13:29] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x925a]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]

```
# 设置FDD RAISE阈值为0x97 FF
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 160 0x97 0xff
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2856 us
Average Time: 2856 us
---------------------------------------------
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -r 0 0x30 160 -l 2
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2346 us
Average Time: 2346 us
---------------------------------------------
160-161: 97 ff 

---------------------------------------------
```
## transceiver_cmd性能监控
```shell
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -m -r 0 0x33 132 -l 2
Monitor read bank[0] page[0x33] addr[132] len[2] start...
------------------------------------------------
Monitor read bank[0] page[0x33] addr[132] len[2] value[ 0x00 00 ]
fec pre ber [0x9261]
fdd raise [0x0000]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x00]
------------------------------------------------
[2026-01-09 11:13:29] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x925a]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:14:35] Monitor read bank[0] page[0x33] addr[132] value[0x01] to [0x00]
fec pre ber [0x929a]
fdd raise [0x97ff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]

```
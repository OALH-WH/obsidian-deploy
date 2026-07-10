---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/备忘录/fed_fdd操作记录/transceiver监控周期400ms/","dg-note-properties":{}}
---

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
## 设置FDD ENABLE
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -r 0 0x30 168
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2251 us
Average Time: 2251 us
---------------------------------------------
168-168: 01 

---------------------------------------------
```
## transceiver_cmd性能监控
```shell
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -m -r 0 0x33 132 -l 2
Monitor read bank[0] page[0x33] addr[132] len[2] start...
------------------------------------------------
Monitor read bank[0] page[0x33] addr[132] len[2] value[ 0x00 00 ]
fec pre ber [0x9277]
fdd raise [0x97ff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]

```
# 设置FDD RAISE阈值为0x8F FF
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -w 0 0x30 160 0x8f 0xff
Operation   : WRITE
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2870 us
Average Time: 2870 us
---------------------------------------------
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -r 0 0x30 160 -l 2
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA0
Len         : 2 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2341 us
Average Time: 2341 us
---------------------------------------------
160-161: 8f ff 

---------------------------------------------
```
## 设置FDD ENABLE
```
root@uaonos-sino:~# /host/wuhang/transceiver_cmd l1 -r 0 0x30 168
Operation   : READ
Bank        : 0x00
Page        : 0x30
Register    : 0xA8
Len         : 1 
Timeout     : 0 sec
Count       : 1
Elapsed Time: 2251 us
Average Time: 2251 us
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
fec pre ber [0x9277]
fdd raise [0x97ff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:05] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x925b]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:07] Monitor read bank[0] page[0x33] addr[132] value[0x01] to [0x00]
fec pre ber [0x9267]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:07] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x92ae]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:09] Monitor read bank[0] page[0x33] addr[132] value[0x01] to [0x00]
fec pre ber [0x92b2]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:10] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x92a7]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:11] Monitor read bank[0] page[0x33] addr[132] value[0x01] to [0x00]
fec pre ber [0x9295]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:12] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x92b9]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:14] Monitor read bank[0] page[0x33] addr[132] value[0x01] to [0x00]
fec pre ber [0x9297]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------
[2026-01-09 11:06:14] Monitor read bank[0] page[0x33] addr[132] value[0x00] to [0x01]
fec pre ber [0x92b4]
fdd raise [0x8fff]
fdd clear [0x0000]
fed raise [0x0000]
fed clear [0x0000]
fed enable [0x00] fdd enable [0x01]
------------------------------------------------

```
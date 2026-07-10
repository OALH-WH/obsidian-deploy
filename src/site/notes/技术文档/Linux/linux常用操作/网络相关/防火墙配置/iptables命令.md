---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/防火墙配置/iptables命令/","dg-note-properties":{}}
---

# iptables 命令大全

## 一、基础命令

### 查看规则

```bash
# 查看 filter 表所有规则（默认表）
iptables -L -n -v

# 查看指定表
iptables -t nat -L -n -v
iptables -t mangle -L -n -v
iptables -t raw -L -n -v

# 带行号显示（便于删除/修改）
iptables -L -n -v --line-numbers

# 查看指定链
iptables -L INPUT -n -v
```

### 清空规则

```bash
# 清空指定表的所有规则
iptables -F
iptables -t nat -F
iptables -t mangle -F

# 清空计数器
iptables -Z
iptables -t nat -Z

# 删除用户自定义链
iptables -X
```

---

## 二、规则管理

### 添加规则

```bash
# 追加规则到链末尾
iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT

# 插入规则到指定位置
iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT

# 在链开头插入
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
```

### 删除规则

```bash
# 按行号删除
iptables -D INPUT 3

# 按规则内容删除
iptables -D INPUT -s 192.168.1.100 -j DROP

# 删除 nat 表规则
iptables -t nat -D POSTROUTING 2
```

### 修改规则

```bash
# 替换指定行规则
iptables -R INPUT 1 -p tcp --dport 443 -j ACCEPT
```

---

## 三、常用规则示例

### 允许/拒绝 IP

```bash
# 允许单个 IP
iptables -A INPUT -s 192.168.1.100 -j ACCEPT

# 拒绝单个 IP
iptables -A INPUT -s 10.0.0.5 -j DROP

# 允许网段
iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT

# 拒绝网段
iptables -A INPUT -s 172.16.0.0/16 -j DROP
```

### 端口管理

```bash
# 允许单个端口
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# 允许端口范围
iptables -A INPUT -p tcp --dport 8000:9000 -j ACCEPT

# 拒绝端口
iptables -A INPUT -p tcp --dport 3306 -j DROP
```

### 协议管理

```bash
# TCP 协议
iptables -A INPUT -p tcp -j ACCEPT

# UDP 协议
iptables -A INPUT -p udp --dport 53 -j ACCEPT

# ICMP (ping)
iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

### 连接状态

```bash
# 允许已建立的连接
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# 允许新连接
iptables -A INPUT -m state --state NEW -p tcp --dport 22 -j ACCEPT

# 拒绝无效连接
iptables -A INPUT -m state --state INVALID -j DROP
```

---

## 四、NAT 规则

### SNAT（源地址转换）

```bash
# 修改出站数据包的源地址
iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j SNAT --to-source 203.0.113.1

# 动态 SNAT（MASQUERADE，适合动态 IP）
iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
```

### DNAT（目的地址转换）

```bash
# 端口转发：本地 8080 -> 内网 192.168.1.100:80
iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.100:80

# SSH 转发：本地 2222 -> 内网 192.168.1.100:22
iptables -t nat -A PREROUTING -p tcp --dport 2222 -j DNAT --to-destination 192.168.1.100:22

# 转发到多个地址（负载均衡）
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:80
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.101:80
```

---

## 五、自定义链

```bash
# 创建自定义链
iptables -N MY_CHAIN

# 跳转到自定义链
iptables -A INPUT -p tcp --dport 80 -j MY_CHAIN

# 在自定义链中添加规则
iptables -A MY_CHAIN -s 192.168.1.0/24 -j ACCEPT
iptables -A MY_CHAIN -j DROP

# 删除自定义链（需先清空且无引用）
iptables -X MY_CHAIN
```

---

## 六、日志记录

```bash
# 记录被拒绝的连接
iptables -A INPUT -j LOG --log-prefix "IPTables-Dropped: " --log-level 4

# 记录特定端口访问
iptables -A INPUT -p tcp --dport 22 -j LOG --log-prefix "SSH-Access: "

# 查看日志
tail -f /var/log/messages | grep IPTables
journalctl -f | grep iptables
```

---

## 七、保存和恢复

### CentOS/RHEL

```bash
# 保存规则
service iptables save
# 或
iptables-save > /etc/sysconfig/iptables

# 恢复规则
iptables-restore < /etc/sysconfig/iptables
```

### Ubuntu/Debian

```bash
# 安装 iptables-persistent
apt-get install iptables-persistent

# 保存规则
iptables-save > /etc/iptables/rules.v4
ip6tables-save > /etc/iptables/rules.v6

# 恢复规则
iptables-restore < /etc/iptables/rules.v4
```

### 通用方法

```bash
# 导出规则
iptables-save > ~/iptables-backup.rules

# 恢复规则
iptables-restore < ~/iptables-backup.rules
```

---

## 八、安全基线配置

```bash
# 清空现有规则
iptables -F
iptables -t nat -F
iptables -t mangle -F
iptables -X

# 设置默认策略（先允许，测试好后再改为 DROP）
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# 允许回环接口
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# 允许已建立的连接
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# 允许 SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# 允许 HTTP/HTTPS
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# 允许 ping
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

# 防止 SYN 洪水攻击
iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT

# 保存规则
iptables-save > /etc/iptables/rules.v4
```

---

## 九、故障排查

```bash
# 查看规则详情
iptables -L -n -v --line-numbers

# 查看 NAT 规则
iptables -t nat -L -n -v

# 查看连接跟踪
cat /proc/net/nf_conntrack
conntrack -L

# 测试规则
iptables -A INPUT -p tcp --dport 8080 -j LOG --log-prefix "TEST: "
tail -f /var/log/messages | grep TEST

# 临时允许所有（调试用）
iptables -P INPUT ACCEPT
```

---

## 十、常用端口参考

| 端口 | 服务 | 命令示例 |
|------|------|----------|
| 22 | SSH | `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` |
| 80 | HTTP | `iptables -A INPUT -p tcp --dport 80 -j ACCEPT` |
| 443 | HTTPS | `iptables -A INPUT -p tcp --dport 443 -j ACCEPT` |
| 3306 | MySQL | `iptables -A INPUT -p tcp --dport 3306 -s 192.168.1.0/24 -j ACCEPT` |
| 5432 | PostgreSQL | `iptables -A INPUT -p tcp --dport 5432 -j ACCEPT` |
| 6379 | Redis | `iptables -A INPUT -p tcp --dport 6379 -s 127.0.0.1 -j ACCEPT` |
| 53 | DNS | `iptables -A INPUT -p udp --dport 53 -j ACCEPT` |
| 25 | SMTP | `iptables -A INPUT -p tcp --dport 25 -j ACCEPT` |

---

## 十一、注意事项

1. **生产环境谨慎操作** - 错误的规则可能导致无法远程连接
2. **先允许 SSH** - 设置 DROP 策略前先允许 22 端口
3. **保存规则** - 重启后规则会丢失，记得保存
4. **测试后再上线** - 新规则先在测试环境验证
5. **备份规则** - 修改前备份现有规则
6. **使用 -n 参数** - 避免 DNS 解析延迟

---

## 十二、快速参考卡

```bash
# 查看
iptables -L -n -v --line-numbers

# 添加
iptables -A INPUT -p tcp --dport PORT -j ACCEPT

# 删除
iptables -D INPUT 行号

# 清空
iptables -F

# 保存
iptables-save > /etc/iptables/rules.v4

# 恢复
iptables-restore < /etc/iptables/rules.v4
```

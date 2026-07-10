---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/服务相关/linux进程管理/","dg-note-properties":{}}
---

1. supervisorctl

1. 安装

1. sudo apt-get install supervisor

1. 配置文件

1. 语法

1. 注释用;开头

1. /etc/supervisor/supervisord.conf

1. 使用

1. 通过[include]这个sectiion来引入其他配置文件(一般放在/etc/supervisor/conf.d目录下，后缀为.conf)

1. 示例

```shell
; supervisor config file

[unix_http_server]
file=/var/run/supervisor.sock   ; (the path to the socket file)
chmod=0700                       ; sockef file mode (default 0700)

[supervisord]
logfile=/var/log/supervisor/supervisord.log ; (main log file;default $CWD/supervisord.log)
pidfile=/var/run/supervisord.pid ; (supervisord pidfile;default supervisord.pid)
childlogdir=/var/log/supervisor            ; ('AUTO' child log dir, default $TEMP)

; the below section must remain in the config file for RPC
; (supervisorctl/web interface) to work, additional interfaces may be
; added by defining them in separate rpcinterface: sections
[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///var/run/supervisor.sock ; use a unix:// URL  for a unix socket

; The [include] section can just contain the "files" setting.  This
; setting can list multiple files (separated by whitespace or
; newlines).  It can also contain wildcards.  The filenames are
; interpreted as relative to this file.  Included files *cannot*
; include files themselves.

[include]
files = /etc/supervisor/conf.d/*.conf
```

1. /etc/supervisor/conf.d

1. 示例

```shell
[program:my_program]
command=/path/to/my_program/start_script.sh
directory=/path/to/my_program
autostart=true
autorestart=true
startsecs=10
user=my_user
stdout_logfile=/var/log/supervisor/my_program_stdout.log
stderr_logfile=/var/log/supervisor/my_program_stderr.log
```

1. API

1. 更新配置文件

1. supervisorctl -c /etc/supervisord.conf reload:重新载入配置文件

1. supervisorctl -c /etc/supervisord.conf update：更新配置文件，不会全部重启

1. 查看守护进程的状态

1. supervisorctl status

1. 重启进程

1. supervisorctl restart <program name>：重启指定进程

1. supervisorctl restart all：重启所有进程

1. 使用流程

1. 安装supervisor

1. 通过配置文件配置supervisor

1. 默认启动/加载特定的配置文件启动supervisord守护进程

1. 示例： sudo  supervisord  -c  /path/to/supervisor.conf

1. 通过supervisorctl命令来管理

1. 注意：如果是加载特定的配置文件启动，supervisorctl也要加上相对应的路径来管理（配置文件默认路径：/etc/supervisor/supervisord.conf）
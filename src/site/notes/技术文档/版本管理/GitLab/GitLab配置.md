---
{"dg-publish":true,"permalink":"/技术文档/版本管理/GitLab/GitLab配置/","dg-note-properties":{}}
---

# 管理员相关
## 初始管理员账号

| 账号     | 密码                                      |
| ------ | --------------------------------------- |
| `root` | `cat /etc/gitlab/initial_root_password` |
# 配置

## /etc/gitlab/gitlab.rb

#### external_url
用于描述`gitlab`中显示的网址链接
用于描述访问`gitlab`的协议和端口:
- 如果包含`https`, 则使用`nginx`代理, 并且将所有`http`流量重定向为`https`, 强制使用`ssl`, 不指定端口默认使用`443`端口
- 如果包含`http`, 则不使用代理直接访问, 不指定端口默认使用`80`端口
这个配置可以被其他配置覆盖, 比如[[#`nginx['listen_port']`]]和[[#`nginx['listen_https']`]]以及[[#`nginx['redirect_http_to_https']`]]

### NGINX相关
参考<https://docs.gitlab.cn/docs/omnibus/settings/nginx/>
#### `nginx['redirect_http_to_https']`
设置`nginx`是否开启`http`流量重定向为`https`
其他类似的参考
```shell
registry_nginx['redirect_http_to_https'] = false
mattermost_nginx['redirect_http_to_https'] = false
```

**值**
- `true`
- `false`

#### `nginx['listen_port']`
设置`nginx`监听端口

**值**
- `port number`: `eg. 80`
#### `nginx['listen_https']`
设置`nginx`是否监听`http`

**值**
- `true`
- `false`

#### `nginx['proxy_set_headers']`
设置`nginx`代理头, 参考[[技术文档/代理/反向代理/nginx/代理头配置\|代理头配置]]


## Rails相关(Gitlab后端)



# 实例
## 需求显示的完整链接和实际链接不一致

**步骤**
1. [[技术文档/版本管理/GitLab/GitLab配置#external_url\|#external_url]]设置为要显示的链接
2. 如果启用`nginx`
	1. 如果监听的是`https`流量, 修改[[#`nginx['redirect_http_to_https']`]]来决定是否重定向`http`流量
	2. 修改[[#`nginx[listen_port]`]]和[[#`nginx[listen_https]`]]为实际链接
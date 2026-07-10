---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/第三方库/GLIB/IO相关/","dg-note-properties":{}}
---

1. 网络IO

1. 

1. 文件IO

1. GSource回调

1. 实例

1. 网络socket创建source，并设置回调, 挂载到指定的主循环中

1. g_socket_create_source(self->udp_socket, G_IO_IN, NULL); //创建socket的IN方向的源

1. g_source_set_callback

1. g_source_attach
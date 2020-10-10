---
title: nginx - 配置
date: 2020-10-10 13:54:39
tags:
  - nginx
  - 软件
---

## server

### http

普通 http 代理配置，应用可以正确识别来源 IP 、请求地址、302跳转

<!-- more -->

域名不需要端口的配置:

```
server {
    listen       80;
    server_name  xx.com;
    location / {
            proxy_pass                           http://127.0.0.1:8080;
            proxy_set_header Host                $host
            proxy_set_header X-Forwarded-For     $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto   $scheme;
            proxy_set_header X-Forwarded-Port    $server_port;
    }
}
```
需要端口的配置:

```
server {
    listen       8080;
    server_name  xx.com;
    location / {
            proxy_pass                           http://127.0.0.1:8080;
            proxy_set_header Host                $host:$server_port;
            proxy_set_header X-Forwarded-For     $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto   $scheme;
            proxy_set_header X-Forwarded-Port    $server_port;
    }
}
```
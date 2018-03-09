---
layout: post
title: 利用Nginx来实现ssh隧道转发
tagline: "another short description here"
image: /assets/patterns/swirl_pattern.png
header:
  image: /assets/patterns/asanoha-400px.png
tags: ["nginx", "ssh"]
keywords: nginx, ssh
ref: about-nginx-ssh-proxy
lang: zh
---

# 1. 前言

公司服务器没有外网流量，访问服务器都是通过阿里云的负载均衡LSB转发请求，这就导致了无法直接使用ssh远程操作服务器，每次登陆阿里云控制台又太麻烦。

# 2. 基本思路

Nginx从1.9.0开始，新增加了一个stream模块，可以用来转发TCP。


# 3. 步骤

假设有服务器A和B，A无法通过外网访问，B可以且安装了Nginx。

首先登陆A服务器，编辑sshd的配置文件`/etc/ssh/sshd_config`，将`GatewayPorts no`改为`GatewayPorts yes`，重启sshd。

登陆B服务器，在配置nginx时增加 `--with-stream`，编辑nginx的配置文件`/usr/local/nginx/conf/nginx.conf`，添加如下配置：

```
stream {
    server {
        listen 60001;
        proxy_pass xxx.xxx.xxx.xxx:22; #A服务器的内网地址，22为sshd的默认端口
    }
}
```

重启Nginx。

到此，ssh代理就配置好了，远程访问有两种方式：

1. 这种方式命令简单一点，但是登陆上后显示的主机名是B的
```
ssh user@服务器B的地址 -p 60001
```

2. 这种是标准的ssh通过代理连接的命令
```
ssh -R 60001:服务器B的地址:22 user@服务器A的地址
```
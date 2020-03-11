---
title: 运维日志 2020/03/11
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---


## 使用ngnix分发服务


- 打开nginx配置文件 `/usr/local/nginx/conf/nginx.conf`

- 在http闭包中 添加以下配置 : 将发往blog.existorlive.cn的请求转向jekyll ,   将发往www.existorlive.cn的请求转向tomcat

```
   server{
        listen 80;
        server_name blog.existorlive.cn;
        location / {
            proxy_pass http://localhost:4000;
        }

    }

    server{
        listen 80;
        server_name www.existorlive.cn;
        location / {
            proxy_pass http://localhost:8080;
        }

    }

```

-  重启ngnix服务

```
cd /usr/local/nginx/sbin

./ngnix -s top

./ngnix

```
 

## 修改安全组 

> 修改安全组：当前仅放开 80 443 22 等端口 支持http，https 和 ssh


## 使用systemctl

```
You are looking for the traditional init scripts in /etc/rc.d/init.d,
and they are gone?

Here's an explanation on what's going on:

You are running a systemd-based OS where traditional init scripts have
been replaced by native systemd services files. Service files provide
very similar functionality to init scripts. To make use of service
files simply invoke "systemctl", which will output a list of all
currently running services (and other units). Use "systemctl
list-unit-files" to get a listing of all known unit files, including
stopped, disabled and masked ones. Use "systemctl start
foobar.service" and "systemctl stop foobar.service" to start or stop a
service, respectively. For further details, please refer to
systemctl(1).

Note that traditional init scripts continue to function on a systemd
system. An init script /etc/rc.d/init.d/foobar is implicitly mapped
into a service unit foobar.service during system initialization.

Thank you!

Further reading:
        man:systemctl(1)
        man:systemd(1)
        http://0pointer.de/blog/projects/systemd-for-admins-3.html
        http://www.freedesktop.org/wiki/Software/systemd/Incompatibilities
```
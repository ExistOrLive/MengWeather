---
title: 运维日志 2020/07/20
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
--- 

## 1. 以systemctl 启动nginx

### 1. 建立服务文件

```sh
vim /usr/lib/systemd/system/nginx.service 
```
文件内容
```sh
[Unit]
Description=nginx - high performance web server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop

[Install]
WantedBy=multi-user.target

### 文件解释
[Unit]:服务的说明
Description:描述服务
After:描述服务类别

[Service]服务运行参数的设置
Type=forking是后台运行的形式
ExecStart为服务的具体运行命令
ExecReload为重启命令
ExecStop为停止命令
PrivateTmp=True表示给服务分配独立的临时空间
注意：启动、重启、停止命令全部要求使用绝对路径

[Install]服务安装的相关设置，可设置为多用户

```

### 2. 使nginx.service文件生效

```sh
systemctl daemon-reload
```

### 3. 使用Systemctl命令启动，关闭，重启Nginx

```sh
# 设置或取消开机自启动
systemctl enable nginx.service 
systemctl disable nginx.service

# 启动，关闭，重启
systemctl start nginx.service

systemctl disable nginx.service

systemctl restart nginx.service

# 查看服务当前状态
systemctl status nginx.service

# 查看所有已启动的服务
systemctl list-units --type=service

#显示启动失败的服务
systemctl --failed 

#查询服务是否开机启动
systemctl is-enabled servicename.service

```

--- 

## 2. 以systemctl 启动 tomcat

### 1. 建立服务文件

```sh
vim /usr/lib/systemd/system/tomcat.service 
```
文件内容

```sh
[Unit]
Description=Tomcat
After=network.target

[Service]
User=zhumeng
Type=forking
ExecStart=/opt/apache-tomcat-8.5.51/bin/catalina.sh start
ExecReload=/opt/apache-tomcat-8.5.51/bin/catalina.sh restart
ExecStop=/opt/apache-tomcat-8.5.51/bin/catalina.sh stop

[Install]
WantedBy=multi-user.target
```

### 2. 使tomcat.service文件生效

```sh
systemctl daemon-reload
```

### 3. 使用Systemctl命令启动，关闭，重启tomcat

```sh
# 设置或取消开机自启动
systemctl enable tomcat.service 
systemctl disable tomcat.service

# 启动，关闭，重启
systemctl start tomcat.service

systemctl disable tomcat.service

systemctl restart tomcat.service

# 查看服务当前状态
systemctl status tomcat.service
```
---


## 3. 安装code-server

[code-server](https://github.com/cdr/code-server)

### 1. 下载code-server

```sh
curl -fOL https://github.com/cdr/code-server/releases/download/v3.7.2/code-server-3.7.2-amd64.rpm
sudo rpm -i code-server-3.7.2-amd64.rpm
sudo systemctl enable --now code-server@$USER
```

### 2. 修改配置 /home/zhumeng/.config/code-server/config.yaml













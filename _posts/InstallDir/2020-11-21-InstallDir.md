# Install Dir

## 1. Nginx

- 安装目录`/usr/local/nginx/`

- 用户： `root`

- 启动，关闭，重启
  
```sh
/usr/local/nginx/sbin/nginx

/usr/local/nginx/sbin/nginx -s reload

/usr/local/nginx/sbin/nginx -s stop
```
- 使用Systemctl启动，关闭，重启

```sh
# 配置请查看/usr/lib/systemd/system/nginx.service 

systemctl start nginx.service

systemctl disable nginx.service

systemctl restart nginx.service
```

## 2. tomcat

- 安装目录`/opt/apache-tomcat-8.5.51`

- 用户： `zhumeng`

- 启动，关闭，重启

```sh
/opt/apache-tomcat-8.5.51/startup.sh
/opt/apache-tomcat-8.5.51/shutdown.sh
```

- 使用Systemctl启动，关闭，重启

```sh
# 配置请查看/usr/lib/systemd/system/tomcat.service 

systemctl start tomcat.service

systemctl disable tomcat.service

systemctl restart tomcat.service

```

## 3. jekyll 


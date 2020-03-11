---
title: 运维日志 2020/03/10
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## 安装ngnix


1. 从[ngnix官网][1]选择版本 1.6.1

2. 使用wget 命令下载 

```
  wget http://nginx.org/download/nginx-1.16.1.tar.gz

```

3. 解压缩

```

tar -xvf nginx-1.16.1.tar.gz

```

4. 进入解压缩后的目录编译安装

```

./configure

make

make install

```

5. 编译安装后，目录在 /usr/local/ngnix， 进入 /usr/local/ngnix/sbin 启动服务

```
nginx
```

#### Tip 

- 编译安装需要事先安装 gcc ，可以通过 yum 安装

- ngnix 依赖 pcre ， openssl， zlib ，可以通过yum安装




[1]: http://nginx.org/

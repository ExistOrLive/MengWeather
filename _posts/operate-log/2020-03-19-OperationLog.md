---
title: 运维日志 2020/03/19
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## Docker 安装

> Docker CE 支持64位版本CentOS 7，并且要求内核版本不低于3.10 

1. 查询系统版本  `uname -a` `cat /etc/redhat-release`

    ![][1]

2. 如果有旧版本Docker，需要卸载

   ```sh
   sudo yum remove docker \ 
                   docker-client \
                   docker-client-lastest \ 
                   docker-common \
                   docker-latest \
                   docker-latest-logrorate \
                   docker-logrorate \
                   docker-selinux \
                   docker-engine-selinux \
                   docker-engine
   ```

3. 安装依赖包
   
   ```sh
   sudo yum install -y yum-utils \
                       device-mapper-persistent-data \
                       lvm2

   ```

4. 添加Docker源

   ```sh

   sudo yum-config-manager --add-repo https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo     # 国内源

   # sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo # 官方源
   ```

5. 安装docker

   ```sh
   sudo yum install docker-ce  #repo中默认只开启stable仓库
   ```

6. 启动并加入开机启动
  
   ```sh
   sudo systemctl start docker

   sudo systemctl enable docker

   ```

7. 将zhumeng 加入 docker 用户组

   ```
   sudo usermod -aG docker zhumeng
   ```

8. 退出后重新登录并测试
  
   ```
   docker run hello-world
   ```



   [Get Docker Engine - Community for CentOS][2]
   
   [Docke入门: Centos7安装Docker][3]


## 安装ELK
   
1. 拉取Elasticsearch 镜像

   ```sh
   docker pull docker.elastic.co/elasticsearch/elasticsearch:7.6.1
   ```

2. 


  [使用Docker安装Elasticsearch][4]

[1]: /assets/images/OperationLog/System-Version.png

[2]: https://docs.docker.com/install/linux/docker-ce/centos/

[3]: https://my.oschina.net/u/3398895/blog/2872963

[4]: https://www.elastic.co/guide/en/elasticsearch/reference/7.6/docker.html

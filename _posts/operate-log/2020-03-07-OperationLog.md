---
title: 运维日志 2020/03/07
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

# Operation Log

## 安装 java

- 环境变量配置

```sh
# java environment
JAVA_HOME=/etc/alternatives/java_sdk_openjdk
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH
```




## 安装RVM

- 通过命令安装

```sh

gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

\curl -sSL https://get.rvm.io | bash -s stable --rails

```

- 配置环境变量

```shell
source /etc/profile.d/rvm.sh
```
- 添加用户群组
  
  将需要使用rvm的用户添加到rvm group


[RVM 官网][1]

## 安装git

```shell
yum install git
```

[git 官网][2]

## Maven 

- 在[https://maven.apache.org/][5]中下载最新的maven


- 在/usr/local/maven/目录下解压

```sh
tar -xf apache-maven-3.6.3_bin.tar.gz
```


- /etc/profile 环境变量配置 

```sh
# maven environment
MAVEN_HOME=/usr/local/maven/apache-maven-3.6.3
PATH=${MAVEN_HOME}/bin:${PATH}
```

- 检验安装

```
mvn -
```


## Jenkins







[1]: http://rvm.io/

[2]: https://git-scm.com/download/linux

[3]: https://jenkins.io/zh/doc/

[4]: https://www.cnblogs.com/116970u/p/11211963.html

[5]: https://maven.apache.org/download.cgi
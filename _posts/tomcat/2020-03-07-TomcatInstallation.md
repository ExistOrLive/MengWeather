---
title: Tomcat 安装教程
tags: 教程
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

# tomcat安装过程

(1)从网上下载tomcat安装包

        https://tomcat.apache.org/

(2)通过scp上传tomcat压缩包
  
      scp  [本地文件路径]  [远端路径]

(3) 上传到/home/zhumeng/resource文件夹下

(4) 利用tar 命令解压至 /usr/local/tomcat
   
     tar -zxvf [压缩包] 目标文件夹 

(5) 执行startup.sh 
    启动tomcat 

(6) 将8080端口添加到云服务的安全组

(7)
     lsof -i : 端口号
     查看端口号下绑定的程序
    
     iptables  管理防火墙配置
     
      iptables -L -n 查看防火请配置
      
      iptables -I INPUT -p 协议 --dport 端口 -j ACCEPT  设置输入流量的配置

    
   
参考资料：
https://www.cnblogs.com/xdp-gacl/p/4097608.html


另外的便捷安装方法
    
    gem install tomcat  一键式安装tomcat和java环境，但是版本较低，不推荐
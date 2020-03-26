---
title: 运维日志 2020/03/25
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## 配置SSL证书 

1.  从[腾讯云][2]申请SSL证书

    ![][1]

2. 下载证书并上传至云服务器

3. 根据[文档][3]配置nginx和tomcat


## Tomcat SSL配置 

1. 将 www.existorlive.com.jks 证书文件 拷贝至 `/usr/local/tomcat/apache-tomcat-8.5.51/conf/`目录下

    ![][4]

2. 修改server.xml ，在 `<Connector port="8080"/>` 添加 `<Connector port="8443"/>`

    ```xml
  
   <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
   <!-- 开放8443端口支持https keystoreFile 证书文件地址  keystorePass 证书秘钥-->
   <Connector port="8443" protocol="HTTP/1.1"
               SSLEnabled="true"
               maxThreads="150"
               scheme="https"
               secure="true"
               clientAuth="false"
               keystoreFile="conf/www.existorlive.cn.jks"     
               keystorePass="********"/>

    ```

3. 修改web.xml ，配置HTTP 自动跳转 HTTPS 的安全配置
   
    ```xml 

    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!-- 添加以下配置-->

    <login-config>
        <!-- Authorization setting for SSL -->
       <auth-method>CLIENT-CERT</auth-method>
       <realm-name>Client Cert Users-only Area</realm-name>
    </login-config>
    <security-constraint>
       <!-- Authorization setting for SSL -->
       <web-resource-collection>
          <web-resource-name>SSL</web-resource-name>
          <url-pattern>/*</url-pattern>
       </web-resource-collection>
       <user-data-constraint>
           <transport-guarantee>CONFIDENTIAL</transport-guarantee>
       </user-data-constraint>
    </security-constraint>

    ```

4. 重启tomcat

## nginx ssl 配置


1.  将 `1_www.existorlive.cn_bundle.crt` 证书文件 和 `2_www.existorlive.cn.key秘钥文件` 拷贝至 `/usr/local/nginx/conf/`目录下

    ![][5]

2. 修改ngnix.conf
   
   ```yaml

    # 修改80端口配置 ，将80端口的http请求重定向至https的443端口

    server{
        listen 80;
        server_name www.existorlive.cn;
        return 301 https://$host$request_uri;
    }


    # 配置443端口，支持https，将https转发到tomcat得8443端口
    
    server {
        listen       443 ssl;
        server_name  www.existorlive.cn;

        ssl_certificate     1_www.existorlive.cn_bundle.crt;
        ssl_certificate_key  2_www.existorlive.cn.key;

        ssl_session_timeout 5m;
        #请按照以下协议配置
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
        ssl_prefer_server_ciphers on;

        location / {
             proxy_pass https://localhost:8443;
        }
    }

   ```

3. 重启ngnix





   
   



[1]: /assets/images/OperationLog/SSLCerOnTencentCloud.png

[2]: https://console.cloud.tencent.com/ssl

[3]: https://cloud.tencent.com/document/product/400/4143

[4]: /assets/images/OperationLog/tomcat_ssl_cer.png

[5]: /assets/images/OperationLog/nginx_ssl_cer.png

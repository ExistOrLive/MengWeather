---
title: 运维日志 2020/03/13
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## 设置ngnix首页

1. fork [BlackrockDigital/startbootstrap-creative][1]静态首页主题 至 [ExistOrLive/startbootstrap-creative][2]


2. 在 /home/zhumeng/github 目录下 clone [ExistOrLive/startbootstrap-creative][2]


3. 修改配置文件 /usr/local/ngnix/ngnix.conf
    
   - 设置ngnix工作进程所有者与启动进程一致，即root  ： user root;
     
         > ngnix 启动后会创建两个进程，work process默认情况下用户为nobody，无法访问/home/zhumeng/github 

        ![][3]

   - 在server 中将根目录设置为/home/zhumeng/github/startbootstrap-creative
      
    


      ```
         user root;                          # ngnix的启动者为root ，这里将工作进程 也设置为root ， 默认为nobody（无法访问/home/zhumeng/github ）


         server {
            listen       80;
            server_name  localhost;

            #charset koi8-r;

            #access_log  logs/host.access.log  main;

            location / {
                root   /home/zhumeng/github/startbootstrap-creative;                #  将首页的根目录设置为/home/zhumeng/github/startbootstrap-creative
                index  index.html index.htm;
            }

            #error_page  404              /404.html;

            # redirect server error pages to the static page /50x.html
            #
            error_page   500 502 503 504  /50x.html;
            location = /50x.html {
                root   html;
            }

            # proxy the PHP scripts to Apache listening on 127.0.0.1:80
            #
            #location ~ \.php$ {
            #    proxy_pass   http://127.0.0.1;
            #}

            # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
            #
            #location ~ \.php$ {
            #    root           html;
            #    fastcgi_pass   127.0.0.1:9000;
            #    fastcgi_index  index.php;
            #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
            #    include        fastcgi_params;
            #}

            # deny access to .htaccess files, if Apache's document root
            # concurs with nginx's one
            #
            #location ~ /\.ht {
            #    deny  all;
            #}
         }
     ```

4. 重启ngnix


## 设置tomcat首页

1. 修改server.xml, 在<Host>tag中添加context，指向/home/zhumeng/github/startbootstrap-creative

    ```xml
     <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">

        <Context path="" docBase="/home/zhumeng/github/startbootstrap-creative"/>    <!-- 添加context，指向/home/zhumeng/github/startbootstrap-creative-->
        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

     </Host>
    ```

2. 重启tomcat











[1]: https://github.com/BlackrockDigital/startbootstrap-creative
[2]: https://github.com/ExistOrLive/startbootstrap-creative
[3]: /assets/images/OperationLog/ngnix_process.png

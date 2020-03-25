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

2. 修改server.xml

```xml
/**
  <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />


```



   
   



[1]: /assets/images/OperationLog/SSLCerOnTencentCloud.png

[2]: https://console.cloud.tencent.com/ssl

[3]: https://cloud.tencent.com/document/product/400/4143
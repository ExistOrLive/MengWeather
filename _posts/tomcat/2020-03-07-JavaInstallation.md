1、 从官网下载JDK
        https://www.cnblogs.com/zeze/p/5902124.html

2、将下载的JDK上传至/home/zhumeng/resource
    
   利用ftp客户端上传jdk  sftp协议（基于ssh） 

3、将压缩包解压至/usr/local/java中
    tar -zxvf [压缩包] 目标文件夹    

4、在/etc/profile 添加环境变量
   
   JAVA_HOME=/usr/local/java/jdk1.8.0_161
   CLASSPATH=$JAVA_HOME/lib/
   PATH=$PATH:$JAVA_HOME/bin
   export PATH JAVA_HOME CLASSPATH

5、重启系统，使得全局变量 JAVA_HOME 和 CLASSPATH 生效



参考文档：

https://www.cnblogs.com/zeze/p/5902124.html 
Apache 安装过程：

一、使用make编译安装apache

(1) 在apache官网下载apache的安装包：

http://mirrors.hust.edu.cn/apache//httpd/httpd-2.4.33.tar.gz

(2)将apache安装包复制到/usr/local/src,并解压
  
    ./configure --prefix=/usr/local/apache     #安装在/usr/local/下 命名为apache
    make
    make install
   
   此时可能会提示缺少apr apr-util pcre依赖
   
(3) 下载相应的apr apr-util pcre 安装包 ，复制到/usr/local/src,并解压

   编译安装
   ./configure --prefix=/usr/local/***     #安装在/usr/local/***下
    make
    make install

(4)再次编译安装apache，添加所需的选项

./configure --prefix=/usr/local/apache --sysconfdir=/etc/httpd --enable-so --enable-rewirte --enable-ssl --enable-cgi --enable-cgid --enable-modules=most --enable-mods-shared=most --enable-mpms-shared=all --with-apr=/usr/local/apr --with-apr-util=/usr/local/apr-util
解释：
--enable-so：支持动态共享模块，如果支持php将不能与apache一起工作。必须要有
--enable-ssl：启用ssl功能，如果不启用将无法使用https
--enable-mpms-shared=all：prefork、worker、event
--with-mpm=event：event为默认
 --enable-rewrite：支持URL重写
--enable-cgi :支持cgi
--enable-cgid:httpd使用event或者worker得启用被线程方式访问
--enable-modules=most :启用大多数模块
--enable-mods-shared=most:启用大多数共享模块

make 

make install

(5)接下来步骤参考一下链接

   https://www.linuxidc.com/Linux/2016-04/130079.html
   

二、通过yum管理工具安装
   
    yum install httpd 一键式安装
    
    相关文件分散于；
    /etc/logrotate.d/httpd
    /etc/httpd                // 配置文件
    /etc/sysconfig/httpd
    /etc/rc.d/init.d/httpd
    /var/log/httpd
    /var/lock/subsys/httpd
    /var/run/httpd     
    /usr/sbin/httpd           //二进制文件
    /usr/lib64/httpd          // 库文件
    /var/www/html/wordpress   // 工作路径
    
    管理apache服务：
    /usr/sbin/apachectl  在系统用户可执行文件中
    
    启动服务
    apachectl start
    关闭服务
    apachectl stop
    重启服务
    apachectl restart
    
    
     
    
    
    
    
    

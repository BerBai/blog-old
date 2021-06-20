---
layout:     post
title:      WNMP 配置
subtitle:   win10 + nginx + php7 + mysql
date:       2019-03-03
author:     白
header-img: img/post-bg-php.jpg
catalog: true
tags:
    - PHP
---


## 1.首先需要的应用程序包。

PHP: <a href='https://windows.php.net/download' target='_blank'>VC15 x64 Non Thread Safe (2019-Feb-06 02:14:41)</a>（nginx 下 php 是以 FastCGI 的方式运行，所以我们下载非线程安全也就是nts的php包）

Nginx: <a href = 'http://nginx.org/en/download.html' target='_blank'>nginx/Windows-1.14.2</a> （下载 stable version）

MySql：<a href='https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.15-winx64.zip' target='_blank'>mysql-8.0.15-winx64.zip</a>

MySql8.xx 的可以参考这个贴 <a href='https://blog.csdn.net/qq_37350706/article/details/81707862' target='_blank'>MySQL 8.0.15安装教程(windows 64位)</a>

附一个用了比较久的 MySql 界面管理器

免费的 Navicat Premium 非商业版许可证：<a href = 'https://www.navicat.com.cn/sponsorship/education/student' target = '_blank'>学术伙伴计划 - 学生</a> 有一个教育邮箱就可以申请

## 2.安装与配置。

### 1）php安装与配置。

将下载好的 php 包文件解压到某一个目录下，例如我的是：D:\wnmp。把解压后的文件目录改为 php7，将里面的 php.ini-production 文件复制一份并改名为 php.ini，用文本编辑器将它打开。

```ini
;将里面的
; On windows:

extension_dir = "./txt"
;改为

; On windows:

extension_dir = "D:/wnmp/php7/ext"
```

将下面两个扩展前面的“;”去掉。（因为 php7 不支持 mysql 扩展了，所以这里只有 mysqli 和 pdo 扩展)

```ini
;extension=mysqli 

;extension=pdo_mysql

;extension=openssl
```

最后让PHP支持 nginx，将下面一行前面的“;”去掉。

```ini
;cgi.fix_pathinfo=1
```

### 2）nginx 安装与配置。

先在 D:/wnmp 目录下新建一个 www 文件夹，作为服务器的根目录。

将下载好的 nginx 包文件解压到D:\wnmp目录下，重命名为 nginx。打开 nginx\conf 下的 nginx.conf 文件来配置 nginx。

```conf
#将一下代码

location/ {
    root html;
    index index.html index.htm;
}

#改为

location/ {
root D:/wnmp/www; #将站点的根目录定位到 D:/wnmp/www

index index.html index.htm;
}  

#再将一下代码

# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
#location ~ \.php$ {
# root html;
# fastcgi_pass 127.0.0.1:9000;
# fastcgi_index index.php;
# fastcgi_param SCRIPT_FILENAME /scripts$fastcgi_script_name;
# include fastcgi_params;
#}

#改为
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#

location ~ \.php$ {
    root           D:/wnmp/www;
    fastcgi_pass   localhost:9000;
    fastcgi_index  index.php;
    
    # 这里$document_root指的是上面定义好的nginx根目录：D:/wnmp/www

    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
#保存好配置即可。
```

## 3.启动。

手动启动 php 和 nginx 来跑一下。

### 1）命令行php目录下键入 php-cgi.exe -b 127.0.0.1:9000 -c D:/wnmp/php7/php.ini（输入以后没有反应，但是不能关掉命令行）

### 2）命令行nginx目录下 start nginx

### 3）在www目录下新建一个 phpinfo.php 文件

```
<?php 
    phpinfo();
?>
```

### 4）浏览器中输入 <a href='http://localhost/phpinfo.php' target='_blank'>localhost/phpinfo.php</a> 或者 <a href='http://127.0.0.1/phpinfo.php' target='_blank'>127.0.0.1/phpinfo.php</a>，出现下面内容则说明php在nginx中运行成功了。

![成功啦](http://ww1.sinaimg.cn/large/006KCUaNgy1g0og4i2gzfj30qi0gl77i.jpg)
 

本文参考 [http://www.cnblogs.com/huayangmeng/archive/2011/06/15/2081337.html](http://www.cnblogs.com/huayangmeng/archive/2011/06/15/2081337.html)
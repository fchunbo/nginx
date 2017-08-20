# Nginx的日志管理
在nginx中，nginx日志管理是通过在nginx.conf文件中配置的。默认的日志是存放在nginx的安装目录下logs/access.log文件中。从nginx.cong配置文件可以看出，配置访问日志使用的是`access_log  logs/access.log  main`，配置error_log，使用的`error_log`配置项，nginx.cong文件的片段如下：

```

#error_log  logs/error.log; #指定错误日志文件的位置
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid; #指定nginx.pid文件的位置

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;#全局的默认的访问日志的位置及日志格式
```
## 1.虚拟主机的日志配置
上面说的日志配置都是全局的，可以在某个虚拟主机下配置日志。比如之前基于域名的主机配置中，配置访问日志及日志的格式：
```
#基于域名的虚拟主机配置
    server{
        listen 80;
        server_name z.com;

        location / {
                root z.com;#这里是相对路径，相对于nginx的安装目录
                index index.html;

        }

        access_log logs/z.com.access.log main;
    }
```
其中`access_log logs/z.com.access.log main;`这样就配置了好了某个虚拟主机的访问日志了。其中日志的格式为`main`.main日志格式如下：
```
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                     '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"'
```
这样配置好，使用
```
kill -HUP `cat /usr/local/nginx/logs/nginx.pid`
```
命令就可以重新加载配置文件了。
这样访问 [http://z.com]() 就可以在logs下面找到z.com.access.log文件了。
```
[root@localhost nginx]# cd logs/
[root@localhost logs]# ll
total 24
-rw-r--r--. 1 root root 8583 Aug 19 23:34 access.log
-rw-r--r--. 1 root root 2610 Aug 19 23:34 error.log
-rw-r--r--. 1 root root    6 Aug 19 21:53 nginx.pid
-rw-r--r--. 1 root root  598 Aug 19 23:34 z.com.access.log
```

查看z.com.access.log日志文件的内容如下：
```
[root@localhost logs]# cat z.com.access.log 
192.168.60.1 - - [19/Aug/2017:23:34:54 -0400] "GET / HTTP/1.1" 200 148 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
192.168.60.1 - - [19/Aug/2017:23:34:56 -0400] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
192.168.60.1 - - [19/Aug/2017:23:34:57 -0400] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
192.168.60.1 - - [19/Aug/2017:23:34:57 -0400] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
192.168.60.1 - - [19/Aug/2017:23:35:24 -0400] "GET / HTTP/1.1" 200 148 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
192.168.60.1 - - [19/Aug/2017:23:39:56 -0400] "GET / HTTP/1.1" 200 148 "-" "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko" "-"
```
这就是访问z.com的日志。

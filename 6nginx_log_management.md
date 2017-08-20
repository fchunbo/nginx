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

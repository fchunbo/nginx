# 虚拟主机配置

### 1.默认的nginx.conf文件
首先给出nginx的默认的配置文件如下：
```
#user  nobody;
worker_processes  1;#worker_process的数量，一般设置为cpu数 * 核数

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid; #指定pid文件的位置


events {
worker_connections  1024;
}
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
    #指一个work_process同时允许的连接数
}


http {#这是配置http服务器的主要段
    include       mime.types;
    default_type  application/octet-stream;


    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    server { #这是虚拟主机配置的地方
        listen 80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

            root   html;#注意这里是相对目录，相对于nginx的安装目录
            index  index.html index.htm;
        }

        #error_page  404              /404.html;
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
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

        # pass the PHP scripts to FastCGI server listening on 127.0.0.#定位把特殊路径或文件再次定位，如image目录单独处理
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


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

### 2.基于域名的虚拟主机配置
```
   #基于域名的虚拟主机配置
    server{
        listen 80;
        server_name z.com;

        location / {
                root z.com;#这里是相对路径，相对于nginx的安装目录
                index index.html;

        }
    }
```
效果如下：

![alt 基于域名的虚拟主机配置](/images/nginx_domain_virtual.png)

### 3.基于端口的虚拟主机配置
```
   #基于端口的虚拟主机配置
   server{
        listen 2022;
        server_name z.com;

        location / {
                root /var/www/html;#注意这里是绝对路径
                index index.html;
        }
   }
```
效果如下：

![alt 基于端口的虚拟主机配置](/images/nginx_port_virtual.png)

### 4.基于IP的虚拟主机配置

```
    #基于ip的虚拟主机配置
    server{
        listen 80;
        server_name 192.168.60.164;

        location /{
                root html/ip;#也是相对路径
                index index.html;
        }
    }
```

效果如下：
![alt 基于ip的虚拟主机配置](/images/nginx_ip_virtual.png)



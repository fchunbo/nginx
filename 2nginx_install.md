# Nginx编译安装

## 1.下载Nginx
下载nginx的地址为：[http://nginx.org/download/nginx-1.12.1.tar.gz](http://nginx.org/download/nginx-1.12.1.tar.gz)

## 2.编译安装nginx
### 2.1 解压nginx-1.12.1.tar.gz
使用`tar -zxvf nginx-1.12.1.tar.gz` 将nginx解压到当前的目录中。
### 2.2 安装nginx
进入到nginx的home目录中，使用如下命令：

```
./configure --prefix=/usr/local/nginx

```
可能会出现如下的错误信息：

```
./configure: error: the HTTP gzip module requires the zlib library.
You can either disable the module by using --without-http_gzip_module
option, or install the zlib library into the system, or build the zlib library
statically from the source with nginx by using --with-zlib=<path> option.

```
注意：这里提示的是需要安装zlib库，因为nginx的http_gzip_module需要改库。
然而使用`yum install -y zlib`安装zlib库时，出现如下信息：
```
[root@localhost nginx-1.12.1]# yum install -y zlib
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: centos.ustc.edu.cn
 * extras: mirrors.cqu.edu.cn
 * updates: centos.ustc.edu.cn
Package zlib-1.2.7-17.el7.x86_64 already installed and latest version
Nothing to do
```
表明，zlib库已经安装了，但为什么安装nginx提示要安装zlib库呢？这是因为还需要安装对应的zlib-devel库。使用`yum install -y zlib-devel`安装zlib-devel即可。

    注意：安装nginx很可能会首先出现要求安装pcre库，使用上述同样的方法，即可解决。
    
`./configure --prefix=/usr/local/nginx`后，就可以使用`make && make install`来安装nginx.

nginx安装目录信息如下：
```
  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx modules path: "/usr/local/nginx/modules"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"
```

在`/usr/local/nginx`目录下有如下目录：
```
drwxr-xr-x. 2 root root 4096 Aug 19 10:36 conf #配置文件
drwxr-xr-x. 2 root root   40 Aug 19 10:36 html #网页文件
drwxr-xr-x. 2 root root    6 Aug 19 10:36 logs #日志文件
drwxr-xr-x. 2 root root   19 Aug 19 10:36 sbin #主要的二进制文件
```


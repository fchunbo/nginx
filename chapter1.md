# Nginx编译安装

## 1.下载Nginx
下载nginx的地址为：[http://nginx.org/download/nginx-1.12.1.tar.gz](http://nginx.org/download/nginx-1.12.1.tar.gz)

## 2.编译安装nginx
### 2.1 解压nginx-1.12.1.tar.gz
使用`tar -zxvf nginx-1.12.1.tar.gz` 将nginx解压到当前的目录中。
### 2.2 安装nginx
进入到nginx的home目录中，使用如下命令：

```java
./configure --prefix=/usr/local/nginx

```
可能会出现如下的错误信息：

```java
./configure: error: the HTTP gzip module requires the zlib library.
You can either disable the module by using --without-http_gzip_module
option, or install the zlib library into the system, or build the zlib library
statically from the source with nginx by using --with-zlib=<path> option.

```
注意：这里提示的是需要安装zlib库，因为nginx的http_gzip_module需要改库
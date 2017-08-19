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

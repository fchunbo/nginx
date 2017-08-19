# Nginx的启动及信号量控制

### 1.Nginx的启动
Nginx的启动是很简单的，在Nginx的安装目录下的`sbin`目录中，只有一个`nginx`的启动文件，只需要执行该启动文件即可。
```
[root@localhost sbin]# pwd
/usr/local/nginx/sbin
[root@localhost sbin]# ls
nginx
```
只需要执行`./nginx`就可以启动nginx。

#### 1.1 Nginx启动参数
在启动nginx的时候可以带上如下参数：

|参数|解释|
|-|-|
|-c </path/to/config> |为 Nginx 指定一个配置文件，来代替缺省的|



### 2.Nginx的信号量控制

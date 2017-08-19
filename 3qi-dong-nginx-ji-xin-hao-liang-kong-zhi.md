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
|-c [path to config] |为 Nginx 指定一个配置文件，来代替缺省的|
|-v |显示nginx版本号|
|-V |显示Nginx版本号、编译器版本和配置参数|
|-t [path to config]|不运行，而仅仅测试配置文件。nginx 将检查配置文件的语法的正确性，并尝试打开配置文件中所引用到的文件|

### 2.Nginx的信号量控制
Nginx的启停等操作有两种操作方式，一是使用参数形式，使用`-s`参数执行信号；二是使用`kill`
#### 2.1 nginx的信号控制方式一


## Nginx的工作原理
使用命令查看nginx的是否启动，使用如下的命令：
```
 ps -aux | grep nginx
```
得到的结果如下：
```
[root@localhost logs]# ps -aux | grep nginx
root      95857  0.0  0.0  20480   524 ?        Ss   11:21   0:00 nginx: master process ./nginx
nobody    95858  0.0  0.1  23008  1240 ?        S    11:21   0:00 nginx: worker process
root      96771  0.0  0.0 112648   968 pts/4    R+   12:14   0:00 grep --color=auto nginx
```
可以看出nginx启动了两个进程，一个是master process ，另一个是worker process。

Nginx的工作原理是：master process进程是不接收web请求的，其作用是用于管理worker process进程；而接受web请求的是worker process。master process只有一个，worker process 有多个。
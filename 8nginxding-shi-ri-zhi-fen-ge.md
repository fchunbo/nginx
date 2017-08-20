# Nginx定时日志分割

现在的需求是将日志按天进行分割，也就是备份每天的日志，这里使用Linux定时任务来完成。

首先编写Linux的shell脚本，脚本如下:
```shell
#!/bin/bash
LOGPATH=/usr/local/nginx/logs/z.com.access.log #指定日志文件的位置
BASE_LOG_PATH=/data/$(date -d yesterday +%Y%m) #按月创建对应的dir

mkdir -p $BASE_LOG_PATH
mv $LOGPATH $BASE_LOG_PATH/$(date -d yesterday +%Y%m%d%H%M).z.com.access.log

touch $LOGPATH #备份之后，重新创建日志文件
kill -USR1 `cat /usr/local/nginx/logs/nginx.pid` #这里是重新打开日志
```
这里需要说明一下，Linux日志文件备份之后，需要新建日志文件才行。

然后，使用`crontab -e`命令编辑定时任务：
```shell
*/1 * * * * sh /data/runLog.sh
```
表示的是，每分钟执行一次日志分割，这里定时的时间可以自己设置。
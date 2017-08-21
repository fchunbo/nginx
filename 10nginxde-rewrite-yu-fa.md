#Nginx的Rewrite的语法
nginx的重写的指令如下：
```
    if (条件) {} 设定条件,再进行重写 注意if后的空格不能省
    set #设置变量
    return #返回状态码
    break #跳出rewrite，循环重定向的时候，需要使用break来跳出rewrite
    rewrite #重写
```
例子如下：
```
location / {
            #禁用某个IP
            #if ($remote_addr = 192.168.60.1){
            #   return 403;
            #}
            
            #进行正则匹配重写uri
            #if ($http_user_agent ~* msie){
            #   rewrite ^.*$ /ie.html;
            #   break;
            #}

            #判断指定的文件是否存在
            if (!-e $document_root$fastcgi_script_name){
                rewrite ^.*$ /404.html;
                break;
            }
            root   html;
            index  index.html index.htm;
        }
```
语法格式如下：
```
if  语法格式
if 空格 (条件) {
    重写模式
}

条件又怎么写?
答:3种写法
1: “=”来判断相等, 用于字符串比较
2: “~” 用正则来匹配(此处的正则区分大小写)
   ~* 不区分大小写的正则
3: -f -d -e来判断是否为文件,为目录,是否存在.

```
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
            
            #if ($http_user_agent ~* msie){
            #   rewrite ^.*$ /ie.html;
            #   break;
            #}

            if (!-e $document_root$fastcgi_script_name){
                rewrite ^.*$ /404.html;
                break;
            }
            root   html;
            index  index.html index.htm;
        }
```

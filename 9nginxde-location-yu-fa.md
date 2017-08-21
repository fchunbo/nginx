# Location的语法
location位于虚拟主机server模块中的，根据uri定位对应的资源的处理方式。location的语法有如下三种：
```
location = patt{}  [精准匹配]
location patt{}    [一般匹配]
location ~patt{}   [正则匹配]
```
如果工作呢？在同一个虚拟主机中，看有没有精准匹配，如果有精准匹配成功，那么就停止匹配，如：
```
 location = patt{
   configA
 }
```
如果`$uri` = patt 匹配成功，那么就使用configA。

对于访问主目录，即http://xxx.com/ 时，有如下配置：
```
location = / {
              root   /var/www/html/;
             index  index.htm index.html;
        }
         
 location / {
             root   /usr/local/nginx/html;
            index  index.html index.htm;
  }

```


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

对于访问主目录比较特别，即访问http://xxx.com/ 时，有如下配置：
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

其定位流程如下：
* 首先精准匹配到 `/` ,得到index页为`/index.htm`
* nginx进行转发到`/index.htm`,此时根目录为`/usr/local/nginx/html`
* 经过内部转发后得到的资源是`index.htm`，在`/usr/local/nginx/html`中是不存在该资源的，最后报404错误。

如果将精准匹配的`index`修改为：
```
location = / {
             root   /var/www/html/;
             index  index.html index.htm;
        }

```
当再次访问主目录的时候，访问的就是nginx的欢迎页面，也就是经过内部转发，访问的是`/usr/local/nginx/html/index/html`.
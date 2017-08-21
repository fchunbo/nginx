# Location的语法
location位于虚拟主机server模块中的，根据uri定位对应的资源的处理方式。location的语法有如下三种：
```
location = patt{}  [精准匹配]
location patt{}    [一般匹配]
location ~patt{}   [正则匹配]
```
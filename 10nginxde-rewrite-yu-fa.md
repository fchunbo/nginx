#Nginx的Rewrite的语法
nginx的重写的指令如下：
```
    if (条件) {} 设定条件,再进行重写 注意if后的空格不能省
    set #设置变量
    return #返回状态码
    break #跳出rewrite，循环重定向的时候，需要使用break来跳出rewrite
    rewrite #重写
```


# 开启mysql日志记录查询sql语句
每当找不到数据报错的原因，每当获取数据错误时候，都要找寻之前执行过得`SQL`语句，来定位错误的原因。`MySQL`的日志记录了执行过得`SQL`语句，那么怎么设置开启呢？

# 查看`MySQL`的`LOG`功能
查看是否已经开启实时`SQL`语句记录

```sql
SHOW VARIABLES LIKE "general_log%";
```

如下`general_log`值为`OFF`说明没有开启：

![mysql_log.png](https://blog.eson.site/wp-content/uploads/2019/01/mysql_log.png)

# 设置`MySQL`的`LOG`功能
> 临时开启

打开实时记录`SQL`语句功能，并指定自定义的`log`路径：

```sql
SET GLOBAL general_log = 'ON';
SET GLOBAL general_log_file = 'EsonAliyun.log';
```

重启`mysql`服务，记录`SQL`日志就开启了。

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:13[/hermit]

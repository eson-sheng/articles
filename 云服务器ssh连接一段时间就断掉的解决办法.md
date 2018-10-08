# 云服务器ssh连接一段时间就断掉的解决办法

- 使用 `vim  /etc/ssh/sshd_config` 编辑如下两行：
找到下面两行
```shell
# ClientAliveInterval 0
# ClientAliveCountMax 3
```
去掉注释，改成
```shell
# 客户端每隔多少秒向服务发送一个心跳数据
ClientAliveInterval 30
# 客户端多少秒没有相应，服务器自动断掉连接
ClientAliveCountMax 1800
```

------------

- 重启sshd服务
```shell
$ service sshd restart
```

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:26[/hermit]
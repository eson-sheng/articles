**生成ssh密钥**
```shell
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 
```
**复制剪贴板**
```shell
$ pbcopy < ~/.ssh/id_rsa.pub 
```
**云服务免密登录**
```shell
$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@YOUR.HOST
```

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:17[/hermit]
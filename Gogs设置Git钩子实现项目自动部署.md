# Gogs设置Git钩子实现项目自动部署
> [GogsWebHook - PHP便捷小工具](https://github.com/eson-sheng/gogs-hook)

“小顾更新一下代码！小顾更新一下代码！！小顾更新一下代码！！！” 
耳边不听响起催促的声音，仿佛想原地爆炸 ~ 
小伙伴们，废话不多说。给大家推荐一个实用的代码更新工具，可接收gogs推送钩子把代码拉取到指定分支上最新节点。

## 如何设置gogs的Web钩子？
- 如图点击设置：
![gogs-set-web-hook](https://api.eson.site/oss/?path=blogUploads/2021/02/b24700240975f16fa7ddbac1b23d7b74.png)
- 设置推送链接：
![gogs-web-hook](https://api.eson.site/oss/?path=blogUploads/2021/02/066cb11cb471d3ed8984c53e8653bb6d.png)

## 如何部署接收推送实现自动部署？

- 部署接口项目
项目地址：[gogs-hook - https://github.com/eson-sheng/gogs-hook](https://github.com/eson-sheng/gogs-hook)

```
git clone git@github.com:eson-sheng/gogs-hook.git
```

- 部署nginx服务配置示例： 

```
server {
  charset utf-8,gbk;
  client_max_body_size 128M;
  listen [端口];
  server_name [域名IP];

  include enable-php.conf;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

  root   /home/www/gogs-hook;
  index  index.php;

  access_log  /home/wwwlogs/gogs-hook.log;
  error_log   /home/wwwlogs/gogs-hook.error.log;
}
```

- **这一步很关键**：设置www用户ssh-key权限免密拉取代码
确保运行php的用户组有权限操作git仓库，**请手动切换到该用户组执行第一下拉取 `git pull`**。

```
# su www
error: This account is currently not available.
# usermod -s /bin/bash www
# su www
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 
$ less ~/.ssh/id_rsa.pub
...
```

- 点击测试推送，如图大功造成。
![gogs-hook](https://api.eson.site/oss/?path=blogUploads/2021/02/79f33e550acc5ea9afce6e97a83287ed.png)

------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~

[hermit auto='1' loop='0' unexpand='1' fullheight='0']remote#:36[/hermit]
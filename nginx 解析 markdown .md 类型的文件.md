# nginx 解析 markdown .md 类型的文件

## 方案A：修改`nginx`的类型配置文件，如下：

- 找到`nginx`配置目录中的`mime.types`文件
```shell
vim /usr/local/nginx/conf/mime.types
```
- 在`types{}`中添加类型：
```conf
text/markdown   md;
```
- 重新载入`nginx`服务
```shell
nginx -s reload
```

## 方案B：利用`nginx`转发`PHP`解析，如下：
> 项目地址：GitHub - [git@github.com:eson-sheng/MARKDOWN_FOR_PHP.git](https://github.com/eson-sheng/MARKDOWN_FOR_PHP)

- 克隆项目到`nginx`服务目录
```shell
git clone git@github.com:eson-sheng/MARKDOWN_FOR_PHP.git
```
- 修改`nginx`配置，将md文件转发给`./MARKDOWN_FOR_PHP/md.php`解析
```shell
    location ~ \.md$ {
        rewrite .* /MARKDOWN_FOR_PHP/md.php?file=$request_filename last;
    }
```
- 重新载入`nginx`服务
```shell
nginx -s reload
```

### 效果图显示，如下：
![nginx解析md](https://blog.eson.site/wp-content/uploads/2019/01/WechatIMG522.png)


------------


Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:22[/hermit]
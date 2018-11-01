### 为解决路由问题 ： http://localhost/index.php/index/index 的配置。
>下面提供的是最新版本的配置文件，适用于最新版的 nginx。
实测已经解决了这个问题。

```nginx
server {
    listen 80;
    server_name    mydomain.vm    www.mydomain.vm;
    access_log    /app/logs/nginx/mydomain_access.log;
    error_log    /app/logs/nginx/mydomain_error.log;
    set        $root    /app/www/mydomain.vm/public;
    location ~ .*\.(gif|jpg|jpeg|bmp|png|ico|txt|js|css)$
    {
        root $root;
    }
    location / {
        root    $root;
        index    index.html index.php;
        if ( -f $request_filename) {
            break;
        }
        if ( !-e $request_filename) {
            rewrite ^(.*)$ /index.php/$1 last;
            break;
        }
    }
    location ~ .+\.php($|/) {
        fastcgi_pass    unix:/run/php/php7.0-fpm.sock;
        fastcgi_split_path_info ^((?U).+.php)(/?.+)$;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME $root$fastcgi_script_name;
        include       fastcgi_params;
    }
}
```
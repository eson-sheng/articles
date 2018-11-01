### 如果装有`composer`直接运行

```php
composer require --prefer-dist yiisoft/yii2-redis
```

### 本地安装如下说明：

下载yii2-redis扩展包[https://github.com/yiisoft/yii2-redis](https://github.com/yiisoft/yii2-redis)并解压，将解压后的文件移至`vebdor/yiisoft`命名为`yii2-redis`，打开`vebdor/yiisoft`下的`extensions.php`

添加如下代码：
```php
'yiisoft/yii2-redis' => 
    array (
        'name' => 'yiisoft/yii2-redis',
        'version' => '2.0.5.0',
        'alias' => 
    array (
        '@yii/redis' => $vendorDir . '/yiisoft/yii2-redis',
    ),
),
```

最后在config文件下的web.php中添加如下配置项：

```php
'redis' =>[
    'class' => 'yii\redis\Connection',
    'hostname' => 'localhost',  //你的redis地址
    'port' => 6379, //端口
    'database' => 0,
]
```

接下来就可以进行对redis的操作了。
```php
$var = Yii::$app->redis->keys("*");
```
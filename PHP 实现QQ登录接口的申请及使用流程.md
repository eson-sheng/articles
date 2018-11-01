**第三方登录，就是使用大家比较熟悉的比如QQ、微信、微博等第三方软件登录自己的网站，这可以免去注册账号、快速留住用户的目的，免去了相对复杂的注册流程。下边就给大家讲一下怎么使用PHP开发QQ登录的功能。**

 - 进入QQ互联官网进行登录(可以使用自己的QQ或者重新注册一个QQ号作为咱们项目的单独QQ进行管理)，地址：[https://connect.qq.com/](https://connect.qq.com/)
 - 点击“应用管理”进入QQ互联管理中心，在这里进行相关应用的创建，分为 网站应用 和 移动应用。选择自己想要的应用进行资料的填写(审核需要等待大概7天左右)，审核通过你将获得`APP ID`和`APP Key`，请拿小本本记上！请拿小本本记上！请拿小本本记上！(重要的事情说三遍!!!)
 - 审核通过获得相关接口：`get_user_info`。
 - 下载QQ互联相关的demo [http://wiki.connect.qq.com/sdk%E4%B8%8B%E8%BD%BD](http://wiki.connect.qq.com/sdk%E4%B8%8B%E8%BD%BD) 我下载的是 `PHP SDK v2.1`
 - 仔细观察`sdk`我们会发现它包含有`4`个文件夹、`2`个文件，其中最主要的是`API`文件夹，其余的我觉得都可以忽略不看(你看也没事)，按照这篇文档一步一步往下进行，你就可以实现登录的功能。
 ![http://blog.eson.site/wp-content/uploads/2018/02/1519053980845-300x210.jpg](http://blog.eson.site/wp-content/uploads/2018/02/1519053980845-300x210.jpg)
 - 将`API`文件夹拷贝到你的项目里，至于拷贝到项目的哪个文件夹，只要你能引入就行，看你心情来就可以，前期准备做好，接下来就是写代码了。
 - 打开你拷贝到项目里的`API`文件夹，其中有一个`comm`文件夹，再次打开`comm`你就能看到一个叫 `inc.php `的家伙，打开它！将上文记在你小本本上的`APPID`和`APPKEY`填写到相关位置，大概形式是这样的:
 
```php
 <?php die(‘forbidden’); ?>
{“appid”:”你的appid”,”appkey”:”你的appkey”,”callback”:”你的网站回调域”,”scope”:”get_user_info”}
```

 - 代码如下:

```php
<?php 

namespace wechat\controllers;

use wechat\common\BaseController;

require(__DIR__ . '/../tools/API/qqConnectAPI.php'); //引入QQ互联SDK,这是按照我自己项目的路径引入的。
 
class QqloginController extends BaseController
{
    //登录方法
    public function actionQqlogin()
    {
        $qc = new \QC();
        $qc->qq_login();
    }
    //这个方法是当你通过QQ登录成功以后想要跳转回来的地址，比如你想登录成功以后跳转到百度，那你把下文的$url改为百度链接即可！
    public function actionCallback()
    {
        header("Content-type: text/html; charset=utf-8");
        // 
        //  这里请根据你的项目开发需求(比如获取登录用户的昵称、头像、年龄等等)，进行相关代码的开发，具体数据获取方法，请查阅QQ互联文档
        //  $qc = new \QC();
        //  $access_token = $qc->qq_callback();
        //  $openid = $qc->get_openid();
        $url = "http://wechat.xxx.cn/index.php?r=cms/home";
        header("Location:".$url);
        exit();
    }
}
```

至此呢你的整个流程就走完了，简单吧！！！整个功能流程类似下图：

![http://blog.eson.site/wp-content/uploads/2018/02/1519054065081-300x166.jpg](http://blog.eson.site/wp-content/uploads/2018/02/1519054065081-300x166.jpg)

**如果你在开发过程中遇到如下问题:**

```php
file_get_contents(): Unable to find the wrapper “https” – did you forget to enable it when you configured PHP?
```

出现这个错误的原因很简单，php配置中的加密模块并没有打开.  
解决方案：
- （windows）`php.ini`配置文件，定位到下图蓝色所示的位置，把`extension=php_openssl.dll` 前面的; 分号去掉去掉以后重新启动`Apache`或者`nginx`服务器，再访问，就不会有这个错误了。
- `linux`下的`PHP`，就必须安装`openssl`模块，安装好了以后就可以访问了。

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:3[/hermit]
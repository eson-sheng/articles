> 本次把我使用第三方新浪微博登录接口的经验来跟大家分享一下，希望对大家有所帮助，尤其对没是使用过新浪微博登录接口的用户。

使用新浪微博登录接口也需要得到新浪微博的认可，所以也需要 微博开发平台 实现四步骤就行了，`开发者注册->创建应用->完善应用资料->提交审核`。等提交审核完成后就可以开发这一块了。以下是具体步骤。

## 准备工作
登录 新浪微博开发平台[http://open.weibo.com/](http://open.weibo.com/)，若果没有微博账号的可以注册一个新浪微博。登录成功后就进行资料填写和身份认证，这个自己去摸索下，等认证成功后。
可以添加新网站（也就是你要使用微博登录的那个网站）[http://open.weibo.com/webmaster/add](http://open.weibo.com/webmaster/add)，按照指定项填写完成后，可以在菜单栏 我的应用 中看到你刚刚提交的网站，当然不是这么简单的就可以了，你可以清楚的看到“未提交审核”，微博开发平台规定，未审核成功的网站只允许使用测试账号（需要手动添加测试账号），只有审核成功的才能上线使用。咱们先看一下我们已经获取到了`app key`和`app secret`，这相当于我们使用微博登录接口的账号。那接下来开始开发吧。

## 开发代码
先下载`php SDK`文档，下载地址[https://github.com/xiaosier/libweibo](https://github.com/xiaosier/libweibo)，如果没有的话，就在[http://open.weibo.com/wiki/SDK](http://open.weibo.com/wiki/SDK)里面找`php SDK`进行下载。
下载完成后只保留`saetv2.ex.class.php`这个文件（当然你要有兴趣的情况下可以研究下其它文件，基本上都是演示文件）。

#### a.通过以下php代码跳转到微博登录页面
```php
require_once("./Login/weibo/saetv2.ex.class.php");
$callback_url = "http://www.abc.com/weibo_callback.php";//回调地址,必须是提交网站域名下的某一个url
$obj = new SaeTOAuthV2($client_id, $client_secret);//$client_id就是App Key  $client_secret就是App Secret
$weibo_login_url = $obj->getAuthorizeURL($callback_url);
header("Location:".$weibo_login_url);
```

#### b.通过以下代码获取`openid`和`access_token`以及用户详细信息。然后可以把这三个数据存入到 第三方用户数据表`other_user`里（这根据开发要求随意）。
```php
require_once("./Login/weibo/saetv2.ex.class.php");
$obj = new SaeTOAuthV2($client_id, $client_secret);//$client_id就是App Key  $client_secret就是App Secret
$code = $_GET['code'];
$callback_url = "http://www.abc.com/weibo_callback.php";//回调地址,必须是提交网站域名下的某一个url
$keys["code"] = $code;
$keys["redirect_uri"] = $callback_url;
$a = $obj->getAccessToken($keys);//$a是一个数组，里面有uid（用户的编号）和access_token.
$info = file_get_contents("https://api.weibo.com/2/users/show.json?access_token={$a['access_token']}&uid={$a['uid']}");
```

#### c.如果你的网站有自己的账号表`user`，那么你可以在`other_user`表里加一个字段`userId`，通过`userId`关联你自己网站里的用户表`user`。当从新浪微博登录页面登录成功后回跳到`weibo_callback.php`时，可以在这个文件里设置`$_SESSION[‘other_userId’]`（目的是记住是哪个第三方用户）,也就是`other_user的id`；设置后跳转到账号绑定页面，然后开始绑定你网站的用户，绑定完成后，把被绑定的网站用户`user`的`id`存入`other_usre`表`$_SESSION[‘other_userId’]`用户的`userId`。下回用户可以直接通过登录qq就可以找到绑定的那个`user`用户了，从而成功登录你的网站了
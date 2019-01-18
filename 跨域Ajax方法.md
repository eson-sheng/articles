# 经典`Ajax`示例：

- `XMLHttpRequest`原生方式
```javascript
var request = new XMLHttpRequest();
request.open("POST", "index.php");
var data = "parameter1" + encodeURIComponent(parameter_one) + "&parameter2" + encodeURIComponent(parameter_two);
request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
request.send(data);
request.onreadystatechange = function() {
    if (request.readyState===4) {
        if (request.status===200) {
            var ret = request.responseText;
            //做有意义的事

        } else {
            alert("发生错误：" + request.status);
        }
    }
}
```

- `jQuery`
```javascript
$.ajax({
    type:"POST",
    url:'index.php',
    dataType:"json",
    data:{
        "parameter1":parameter_one,
        "parameter2":parameter_two
    },
    success:function(ret){
        //做有意义的事

    },
    error:function(jqXHR){
        if (jqXHR.status!=200) {
            alert("发生错误：" + jqXHR.status);
        }
    }
});
```
# 跨域`Ajax`方案：

## 方案A：`JSONP`

- 前端请求页面：
```javascript
$.ajax({
    type:"POST",
    url:'http://127.0.0.1/test/Ajax_jsonp/service.php',
    dataType:"jsonp",
    jsonp:"jsonp",
    data:{
        "parameter1":parameter_one,
        "parameter2":parameter_two
    },
    success:function(ret){
        //做有意义的事
        alert(JSON.stringify(ret));
        console.log(ret);
    },
    error:function(jqXHR){
        if (jqXHR.status!=200) {
            alert("发生错误：" + jqXHR.status);
        }
    }
});
```

- 后端响应页面：
**注意后端响应是`GET`**

```php
<?php 
if (!empty($_GET['jsonp'])) {
    $jsonp = $_GET['jsonp'];
    $ret = json_encode($_GET);
    echo "{$jsonp}({$ret})";
}
```

## 方案B：`XHR2`服务端添加响应头信息（IE10以下不支持）
```php
header("Access-Control-Allow-Origin:*");//允许所有来源访问
header("Access-Control-Allow-Method:POST,GET");//允许访问的方式
```

## 终极方案：后端代理
curl

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:14[/hermit]
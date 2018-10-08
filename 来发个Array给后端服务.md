## 来发个Array给后端服务
> 用FormData来创建  
表单发送给后端服务 - 示例 ^_^

**小伙伴啊！想要这样的数据给后端怎么来做呢？**
**如图：**
![image](https://blog.eson.site/wp-content/uploads/2018/06/FormData.jpeg)   

#### 来看代码示例：
```
<?php 
if (!empty($_POST)) {
    echo "<pre>";
    print_r($_POST);
    echo "</pre>";
}
if (!empty($_FILES)) {
    echo "<pre> files";
    print_r($_FILES);
    echo "</pre>";
}
 ?>
<!DOCTYPE html>
<html>
<head>
    <title>test post for array</title>
</head>
<body>
    <!-- <form action="" method="POST" enctype="multipart/form-data"> -->
    <div id="inputs">
        <input type="text" name="path[]" id="path_1" required placeholder="path" value="./a/lalala1.md">
        <input type="text" name="path[]" id="path_2" required placeholder="path" value="./a/lalala2.md">
        <input type="text" name="path[]" id="path_3" required placeholder="path" value="./a/lalala3.md">
        <input type="text" name="path[]" id="path_4" required placeholder="path" value="./a/lalala4.md">
        <input type="text" name="path[]" id="path_5" required placeholder="path" value="./a/lalala5.md">
    <!-- <input type="submit" name="sub" id="sub" value="发送"> -->
    <button id="send">发送</button>
    </div>
    <!-- </form> -->
</body>
<script type="text/javascript" src="http://lib.sinaapp.com/js/jquery/1.9.1/jquery-1.9.1.min.js"></script>
<script type="text/javascript">
$(function(){
    $("#send").click(function(){
        var formData = new FormData();
        $("#inputs input").each(function(){
            formData.append('path[]', $(this).val());
            // formData.append('path[]', $(this)[0].files[0]); // 如果是文件
        });
        $.ajax({
            url: '',
            type: 'POST',
            cache: false,
            data: formData,
            processData: false,
            contentType: false
        }).done(function(res) {
            console.log(res);
        }).fail(function(res) {
            console.log(res);
        });
    });
});
</script>
</html>
```
如果你们有更好的方案欢迎留言啊~我是Eosn，端午安康~

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:10[/hermit]

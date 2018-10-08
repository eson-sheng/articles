> # PHP中检查文件是否存在函数
file_exists() `bool file_exists ( string $filename )`
is_file() `bool is_file ( string $filename )`

从字面上看，判断一个文件是否存在理应使用 file_exists()函数,但file_exists()函数除了可以判断文件是否存在外，还可以判断目录是否存在，正因为file_exists()函数既可以判断文件也可判断目录是否存在，所以导致file_exists()函数函数的执行效率非常低，远远不及is_file()函数，is_file判断给定文件名是否存在，该函数只能判断文件是否存在，不能判断目录是否存在。

下面我们来通过程序验证一下file_exists与is_file的效率：

分别执行1000次，记录所需时间。

------------

文件存在(当前目录)
is_file:0.4570ms
file_exists:2.0640ms

文件存在(绝对路径3层/www/hx/a/)
is_file:0.4909ms
file_exists:3.3500ms

文件存在(绝对路径5层/www/hx/a/b/c/)
is_file:0.4961ms
file_exists:4.2100ms

文件不存在(当前目录)
is_file:2.0170ms
file_exists:1.9848ms

文件不存在(绝对路径5层/www/hx/a/b/c/)
is_file:4.1909ms
file_exists:4.1502ms

目录存在
file_exists:2.9271ms
is_dir:0.4601ms
目录不存在
file_exists:2.9719ms
is_dir:2.9359ms

is_file($file)
file_exists($file)
当$file是目录时，is_file返回false，file_exists返回true

------------

最终结论：
>**如果要判断目录是否存在，请用独立函数 is_dir(directory)** 
>**如果要判断文件是否存在，请用独立函数 is_file(filepath)** 

> **is_file 只判断文件是否存在； 
file_exists 判断文件是否存在或者是目录是否存在； 
is_dir 判断目录是否存在；** 

查看手册，虽然这两个函数的结果都会被缓存，但是is_file却快了N倍。 
还有一个值得注意的： 
> **文件存在的情况下，is_file比file_exists要快N倍； 
文件不存在的情况下，is_file比file_exists要慢；** 

结论是，file_exits函数并不会因为该文件是否真的存在而影响速度，但是is_file影响就大了。

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:14[/hermit]
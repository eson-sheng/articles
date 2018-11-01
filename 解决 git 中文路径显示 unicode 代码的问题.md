> 当被修改的文件中带有中文字符时，中文字符会被转换为`unicode`代码，看不出原来的文件名。

这时，只要配置：

```shell
git config --global core.quotepath false
```
或者
```shell
git config --system core.quotepath false
```

`git`就不会就不会对路径进行转换，显示原来完整的中文路径名。
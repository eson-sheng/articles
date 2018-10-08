# 装不了`PHP`的扩展，`make install`失败
```
RudonMacBook:igbinary-master rudon$ make install
Installing shared extensions:     /usr/lib/php/extensions/no-debug-non-zts-20131226/
cp: /usr/lib/php/extensions/no-debug-non-zts-20131226/#INST@12567#: Operation not permitted
make: *** [install-modules] Error 1

cp: /usr/lib/php/extensions/no-debug-non-zts-20121212/#INST@17000#: Operation not permitted
```
### 原因:
原来是`MacOSX 10.11 El Capitan`（或更高）新添加了一个新的安全机制叫系统完整性保护`System Integrity Protection (SIP)`，所以对于目录`/System` `/sbin` `/usr`
不包含(`/usr/local/`)仅仅供系统使用，其它用户或者程序无法直接使用，而我们的`/usr/lib/php/extensions/`刚好在受保护范围内
### 解决方法:
#### 禁掉SIP保护机制，步骤是：
- 重启系统
- 按住`Command + R`（重新亮屏之后就开始按，象征地按几秒再松开，出现苹果标志，ok）
- 菜单“实用工具” ==>> “终端” ==>> 输入
```shell
$ csrutil disable
```
执行后会输出：`Successfully disabled System Integrity Protection. Please restart the machine for the changes to take effect.`
- 再次重启系统
- 禁止掉`SIP`后，就可以顺利的安装了，当然装完了以后你可以重新打开`SIP`，方法同上，只是命令是
```shell
$ csrutil enable
```

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:25[/hermit]
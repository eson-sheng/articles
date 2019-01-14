# `MacOS`上的`ShadowSocks`代理共享给其他设备
> [下载`Privoxy 3.0.26 64 bit.pkg`软件包](http://180.76.119.50:444/download/MacOS%E8%BD%AF%E4%BB%B6/Privoxy%203.0.26%2064%20bit.pkg)

这个方法可以在同一个局域网中让多个设备连接已经代理`ShadowSocks`的电脑，不用再每个设备上安装`ShadowSocks`，但是被共享的设备代理方式是全局的。废话不多说，一起来看教程吧！

- 先打开`MacOS`的`ShadowSocks`代理，还不知道`ShadowSocks`的小伙伴请看这里：[https://shadowsocks.org/](https://shadowsocks.org/)

- 下载`Privoxy`软件包，我使用的是`Privoxy 3.0.26 64 bit.pkg`这个版本。
> [http://www.privoxy.org](http://www.privoxy.org)

![privoxy](https://blog.eson.site/wp-content/uploads/2019/01/privoxy.jpg)

- 安装`Privoxy`完成后,打开访达`Finder`使用`Commend+Shift+G`快捷键前往文件夹：
```shell
/usr/local/etc/privoxy
```

- 进入文件夹后找到`config`配置文件，使用编辑器打开：
![privoxy_config](https://blog.eson.site/wp-content/uploads/2019/01/privoxy_config.jpg)

- 搜索`forward-socks5t`找到如图所示的一行代码，去掉`#`井号注释，将端口改为`1080`(如果你的 Shadowsocks 端口是其它的，请改为其它)
![forward-socks5t](https://blog.eson.site/wp-content/uploads/2019/01/forward-socks5t.png)
![forward-socks5t-1080](https://blog.eson.site/wp-content/uploads/2019/01/forward-socks5t-1080.jpg)

- 再搜索`listen-address`找到如图所示的的一行代码，去掉`#`井号注释，把`127.0.0.1`改为`0.0.0.0`，端口号改成一个未占用的端口（比如`1188`、`6789`）
![listen-address](https://blog.eson.site/wp-content/uploads/2019/01/listen-address.png)
![listen-address-1188](https://blog.eson.site/wp-content/uploads/2019/01/listen-address-1188.jpg)

- 两处配置修改完成后保存退出。然后想把`Privoxy`添加到开机启动中：

```shell
# 添加开机启动:
ln -sfv /usr/local/opt/privoxy/*.plist ~/Library/LaunchAgents
# 开启 Privoxy:
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.privoxy.plist
# 如果不需要用 launchctl 就直接运行:
privoxy /usr/local/etc/privoxy/config
```

- 手动启动和关闭方式：
```shell
# 进入 Privoxy 开启关闭脚本的文件
cd /Applications/Privoxy
# 开启 Privoxy:
sudo ./startPrivoxy.sh
# 关闭 Privoxy:
sudo ./stopPrivoxy.sh
```

- 最后就是拿出移动端手机或者平板，进入网络设置界面：
设置 > 无线局域网 > 链接点击i
![WechatIMG461](https://blog.eson.site/wp-content/uploads/2019/01/WechatIMG461-576x1024.png)

- `HTTP`代理开启设置为手动，把`macOS`的`IP`地址和刚才在`listen-address`配置端口号填到这里：
打开终端，查看`macOS`的`IP`
```shell
$ ifconfig en0 inet
```
看到`inet 192.168.xxx.xxx`就是`macOS`的`IP`
```
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    inet 192.168.xxx.xxx netmask 0xffffff00 broadcast 192.168.xxx.xxx
```
![WechatIMG462](https://blog.eson.site/wp-content/uploads/2019/01/WechatIMG462-576x1024.jpeg)

- 打开网络新世界！
![WechatIMG463](https://blog.eson.site/wp-content/uploads/2019/01/WechatIMG463-576x1024.jpeg)

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:25[/hermit]

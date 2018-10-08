# 云服务器 Ubuntu 命令行下，安装中文环境。

英文版的`Ubuntu`服务器，在打开含有中文字符文件时会乱码，有需要给`Ubuntu Server`装中文环境。  

------------

- 安装之前，执行 
```shell
echo $LANG 
```
屏幕显示：
`en_US.UTF-8` 
说明现在是英语环境，需要切换到中文环境。  

------------

- 安装中文语言包
```shell
$ apt-get update && apt-get install language-pack-zh-hans
```

------------

- 使用 `vim /etc/default/locale` 把原来英语 US 的都换成如下的内容，并且注意配置**文件中不能有多余的空格：** 
```shell
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh"
LC_NUMERIC="zh_CN"
LC_TIME="zh_CN"
LC_MONETARY="zh_CN"
LC_PAPER="zh_CN"
LC_NAME="zh_CN"
LC_ADDRESS="zh_CN"
LC_TELEPHONE="zh_CN"
LC_MEASUREMENT="zh_CN"
LC_IDENTIFICATION="zh_CN"
LC_ALL="zh_CN.UTF-8"
```

------------

- 再使用 `vim /etc/environment` 原来有一行 `PATH=...` 不要动这一行另起一行，复制粘贴以下内容，并且注意配置**文件中不能有多余的空格：** 
```shell
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh"
LC_NUMERIC="zh_CN"
LC_TIME="zh_CN"
LC_MONETARY="zh_CN"
LC_PAPER="zh_CN"
LC_NAME="zh_CN"
LC_ADDRESS="zh_CN"
LC_TELEPHONE="zh_CN"
LC_MEASUREMENT="zh_CN"
LC_IDENTIFICATION="zh_CN"
LC_ALL="zh_CN.UTF-8"
```

------------

- 重启机器 
```shell
$ reboot
```

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:24[/hermit]
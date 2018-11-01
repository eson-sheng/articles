之前安装系统的时候没有注意，一下就安装成英文系统了。在PuTTY的SSH下面可以显示中文，看着长串的英文实在有些不舒服，决定更改成中文。

直接修改 /etc/default/locale 是不行的，因为没有安装语言包。（汗。。。）

**1、安装中文语言包**

`sudo apt-get install language-pack-zh-hans`**2、修改 /etc/default/locale 文件**

```
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh"
```

（一般这样就可以生效了。如果没有生效，需要继续执行下面的操作）

**3、编辑/etc/environment，添加或改成：**

```
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh:en_US:en"
```

**4、编辑/var/lib/locales/supported.d/local：**

```
en_US.UTF-8 UTF-8
en_GB.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_CN.GBK GBK
zh_CN GB2312
```

**5、执行命令，生成语言文件**

```
locale-gen
```

**5、执行命令，查看环境变量的语言选项。**

`locale`
### Mac系统如何显示隐藏文件？
> 两条命令就搞定

- 在终端（Terminal）输入如下命令，即可显示隐藏文件和文件夹：
```
defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder
```

- 如需再次隐藏原本隐藏的文件和文件夹，可以输入如下命令：
```
defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder
```

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:8[/hermit]
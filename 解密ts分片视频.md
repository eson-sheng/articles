# 解密ts分片视频

新的一年，来了。
和往常一样，又是一段养生朋克的日子，等待着那笔早该入手的间歇性资本主义安慰。
算了，怀揣着不安的心倒不如打开电脑来看剧，那一刻我愿与这个世界为敌......
什么？网站上的剧居然下载不了~ 秒按 `option+command+i` 打开调试器查看，我去 `blob: https://` 是什么鬼。。。
再看`Netword`选项`XHR`一堆`ts`文件请求，我点进去下载下来居然是一小段视频片段啊！
仿佛这个世界又一次成为了我的敌人... 废话不多说，一起开始撸代码做工具下载小视频吧 ！~ 

## `FFmpeg`如何加密视频
### 1.获取加密用16字节key，并查看其值。

```sh
$ openssl rand 16 > enc.key
$ xxd enc.key
```
![查看enc.key的值](https://blog.eson.site/wp-content/uploads/2020/01/hls1.png)
如图查看`enc.key`的值为`000b92f10d9f69ab44c4956f22270f7a`

### 2.获取加密用iv并查看其值。

```sh
$ openssl rand -hex 16 > enc.iv.txt
$ xxd enc.iv.txt
```
![查看偏移量enc.iv.txt的值](https://blog.eson.site/wp-content/uploads/2020/01/hls2.png)
如图查看偏移量enc.iv.txt的值为`62b27e3171bb3c0613e4fb0985e00b83`

### 3.生成`hls_key_info_file`其内容形式如下:
```
Key URI
Path to key file
IV (optional)
```
![hls_key_info_file](https://blog.eson.site/wp-content/uploads/2020/01/hls3.png)
`vim enc.keyinfo`
```
https://localhost/enc.key
enc.key
62b27e3171bb3c0613e4fb0985e00b83
```
`:wq`
**注意：第三行的哈希值`62b27e3171bb3c0613e4fb0985e00b83`默认是`32个0`不写也可以。**

### 4.使用`FFmpeg`切片视频为加密的`hls`视频
>eg: `ffmpeg -i PRTD-24.mp4 -hls_time 10 -hls_key_info_file enc.keyinfo PRTD-24.m3u8`

```sh
$ ffmpeg -i [filename.mp4] -hls_time 10 -hls_key_info_file enc.keyinfo [filename.m3u8]
```

![hls](https://blog.eson.site/wp-content/uploads/2020/01/hls4.png)
如图执行完成后有：`PRTD-24.m3u8` `PRTD-240.ts` `PRTD-241.ts` `PRTD-242.ts` 这些文件，其中`.m3u8`是索引文件，一般都是通过这个文件来爬去网站上的所有分片视频，`.ts`是加密的分片视频文件。

## 解密视频
> 使用`openssl`解密`ts`视频，其中参数`-iv`默认是`32个0`如果设置了就用哈希值，参数大写的`-K`是秘钥的值。
eg: `openssl aes-128-cbc -d -in PRTD-240.ts -out 0.ts -nosalt -iv 62b27e3171bb3c0613e4fb0985e00b83 -K 000b92f10d9f69ab44c4956f22270f7a`

```sh
$ openssl aes-128-cbc -d -in test0.ts -out 0.ts -nosalt -iv 00000000000000000000000000000000 -K 000b92f10d9f69ab44c4956f22270f7a
```

![hls](https://blog.eson.site/wp-content/uploads/2020/01/hls5.png)
如图对每个加密的`ts`文件执行后就是解密的`ts`视频文件了，再用`FFmpeg`合并解密后的分片视频就是原视频了。

```sh
$ ffmpeg -i "concat:0.ts|1.ts|2.ts" -acodec copy -vcodec copy -absf aac_adtstoasc output.mp4
```

## 工具使用git仓库下载
>  简单的m3u8下载工具，可以下载未加密的ts分片视频自动用FFmpeg合并。
[git@github.com:eson-sheng/download-m3u8-to-mp4.git](https://github.com/eson-sheng/download-m3u8-to-mp4)

工具使用很简单：主要是找到`.m3u8`文件的地址。
打开命令行输入 `php php download_m3u8.php --url https://xxx/index.m3u8` 就开始下载视频啦 ~


上文中说的例举视频我已经放入仓库中的`demo`文件里，供大家参考学习哦`^_^`。

------------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:32[/hermit]
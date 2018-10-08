## 版本控制`git`搞不懂该怎么练习呢？
> ——本地模拟`git`多人协作 

***糟糕！拉取远程代码又冲突了...我该怎么修改历史节点啊...我们同时修改一个文件怎么又出这么多幺蛾子呢！？。。。***

这个时候要是能在本地模拟出多个用户就好了 ！

#### 模拟`git`在本地，不需要远程的服务器：

---

`$ mkdir git` *//建立练习用的文件夹*  
`$ cd git` *//进入这个文件夹*  
`$ mkdir server` *//建立个git服务文件夹*  
`$ cd server` *//进入这个git服务文件夹*  
`$ git init --bare ` *//初始化一个裸仓库,就相当于项目中的.git文件夹*  如图：
![image](https://blog.eson.site/wp-content/uploads/2018/06/git%E8%A3%B8%E4%BB%93%E5%BA%93.jpg)
`$ cd ../` *//去上级目录，此时在git练习目录*  
`$ git clone ./server u1` *//建立一个用户目录u1*  
`$ git clone ./server u2` *//建立一个用户目录u2*...可以看心情建立更多人...  

---

此时，就建立好了一个以本地为远端服务的git版本控制。  
文件夹`./git/u1`和`./git/u2`分别为两个用户。  
对于`./git/server`文件夹为这两个用户的远端服务(大本营)，进入`u1`就可以写项目了：添加`git add `、提交 `git commit`、推送`git push`...等操作,然后进入`u2`就可以：拉取`git fetch`，更新`git pull` ...  
这样就可以模拟多人协作的git版本控制了。

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:7[/hermit]